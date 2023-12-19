# Using `sed` command to automate Apache Reverse Proxy

Previously, my solution to was to overwrite or create a new virtual host configuration file.

```
# Install Apache
sudo DEBIAN_FRONTEND=noninteractive apt install apache2 -y

sudo systemctl start apache2
sudo systemctl enable apache2

# Enable necessary Apache modules
sudo a2enmod proxy
sudo a2enmod proxy_http

# Create a virtual host configuration file
VHOST_CONF="/etc/apache2/sites-available/000-default.conf"
cat <<EOF | sudo tee "$VHOST_CONF"> /dev/null
<VirtualHost *:80>

    ProxyPass / http://localhost:5000/
    ProxyPassReverse / http://localhost:5000/

    ErrorLog \${APACHE_LOG_DIR}/error.log
    CustomLog \${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
EOF
sudo systemctl restart apache2
```
## Using `sed` command 

### Fist Try

```
# Create a virtual host configuration file
if ! grep -q "ProxyPass / http://localhost:5000/" /etc/apache2/sites-available/000-default.conf; then
  sudo sed -i "/DocumentRoot \/var\/www\/html/ a\ProxyPreserveHost On\nProxyPass \/ http:\/\/localhost:5000\/\nProxyPassReverse \/ http:\/\/localhost:5000\/" /etc/apache2/sites-available/000-default.conf
fi
```

This way works, but we don't have a way to confirm whether 

### Updated command

Another way to do this is to instead edit the current configuration file by fist checking if it already has the necessary part that we are looking for in the file:

```
if grep -q 'ProxyPass / http://localhost:5000/' /etc/apache2/sites-available/000-default.conf; then
    # The string exists, so nothing to do
    echo "Reverse proxy already configured."
```

If `ProxyPass / http://localhost:5000/` is present on the file, the the terminal will display that the reverse proxy has already been configured.
If it can't find it it will proceed to write the necessary lines on to the file after `DocumentRoot /var/www/html/` :

```
else
    echo "Configuring reverse proxy..."
    sudo sed -i '/DocumentRoot \/var\/www\/html/ a\ProxyPreserveHost On\nProxyPass \/ http:\/\/localhost:5000\/\nProxyPassReverse \/ http:\/\/localhost:5000\/\n' /etc/apache2/sites-available/000-default.conf
fi
```

* Having `/DocumentRoot \/var\/www\/html/ a\` shows that what comes next will be put AFTER this code snippet.
* `\ProxyPreserveHost On` will be the fist line to be written.
* `\nProxyPass \/ http:\/\/localhost:5000\/` will be the second line to be written.
* `\n` marks a new line.
* `\nProxyPassReverse \/ http:\/\/localhost:5000\/\n` will be the third line written. 
* The `sed` command reads forward slashes in a particular way when in Strings so it is necessary to include a backslash before every forward slash with the exception of the first two which separate the pattern.
* `/etc/apache2/sites-available/000-default.conf` will specify the path of the file.


## Complete Automated Scipt

```
#!/bin/bash
cd
sudo apt update -y
echo "Update Done!"
echo ""
sudo DEBIAN_FRONTEND=noninteractive apt upgrade -y
echo "Update Done!"
echo ""
# install maven
sudo DEBIAN_FRONTEND=noninteractive apt install maven -y
echo "Maven Install Done!"
echo ""
# check maven is installed
mvn -v
echo "Maven Check Done!"
echo ""
# install JDK (java) 17
sudo DEBIAN_FRONTEND=noninteractive apt install openjdk-17-jdk -y
echo "Installed JDK Done!"
echo ""
# check JDK 17 is installed
java -version
echo "Java Check Done!"
echo ""
# copy the app code to this VM
sudo DEBIAN_FRONTEND=noninteractive apt install git -y
echo "Git Install Done!"
rm -rf repo
git clone https://HenriqueMCunha@github.com/HenriqueMCunha/tech242-jsonvoorhees-app.git repo
echo "Git Clone Done!"

# Install Apache
sudo DEBIAN_FRONTEND=noninteractive apt install apache2 -y

sudo systemctl start apache2
sudo systemctl enable apache2

# Enable necessary Apache modules
sudo a2enmod proxy
sudo a2enmod proxy_http

# Create a virtual host configuration file
if grep -q 'ProxyPass / http://localhost:5000/' /etc/apache2/sites-available/000-default.conf; then
    # The string exists, so nothing to do
    echo "Reverse proxy already configured."
else
    echo "Configuring reverse proxy..."
    sudo sed -i '/DocumentRoot \/var\/www\/html/ a\ProxyPreserveHost On\nProxyPass \/ http:\/\/localhost:5000\/\nProxyPassReverse \/ http:\/\/localhost:5000\/\n' /etc/apache2/sites-available/000-default.conf
fi


sudo systemctl reload apache2

cd repo/
echo "cd Into app Done!"
cd springapi/
echo "cd into springapi Done!"
# run the application
mvn spring-boot:start
echo "The App is Running!"

```


### Launching an Instance from AMI

When launching an instance from AMI, all we have to do is make sure that we are moving into the correct repository and starting the application:

```
#!/bin/bash

cd repo/springapi

mvn spring-boot:start
```