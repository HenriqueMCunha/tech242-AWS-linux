# Apache Automated Proxy

- [Apache Automated Proxy](#apache-automated-proxy)
  - [Set up an APache Web Server](#set-up-an-apache-web-server)
  - [Configure Apache Web Server Reverse Proxy](#configure-apache-web-server-reverse-proxy)
    - [Tried to create a virutal host configuration file but unsuccessfully](#tried-to-create-a-virutal-host-configuration-file-but-unsuccessfully)
    - [Instead reconfigured existing 000-default.conf file](#instead-reconfigured-existing-000-defaultconf-file)
      - [Reconfigured by overwriting current 000-default.conf file](#reconfigured-by-overwriting-current-000-defaultconf-file)

## Set up an APache Web Server

## Configure Apache Web Server Reverse Proxy

### Tried to create a virutal host configuration file but unsuccessfully

```

#!/bin/bash

# update & upgrade
echo "UPDATING..."
sudo apt update -y
echo "DONE!"
echo "UPGRADING..."
sudo DEBIAN_FRONTEND=noninteractive apt upgrade -y
echo "DONE!"

# install apache web server

sudo DEBIAN_FRONTEND=noninteractive apt install apache2 -y

# start and enable apache web server and reload source

sudo systemctl start apache2
sudo systemctl enable apache2

# configure apache to port 5000
# get apache mods
sudo a2enmod proxy
sudo a2enmod proxy_http
sudo a2enmod proxy_html

# creating config file
BACKEND_HOST=$(curl ifconfig.me)

# Check if the virtual host configuration file already exists
if [ -f /etc/apache2/sites-available/${BACKEND_HOST}.conf ]; then
  # Overwrite the existing file
  echo "Overwriting existing virtual host configuration file..."
  sudo cat << EOF > /etc/apache2/sites-available/${BACKEND_HOST}.conf

<VirtualHost *:80>
  ServerName ${BACKEND_HOST}

  # Proxy incoming HTTP requests to the backend server
  ProxyPass / http://${BACKEND_HOST}:5000/
  ProxyPassReverse / http://${BACKEND_HOST}:5000/

  # Allow Apache2 to handle and process the request (enables mod_proxy_html)
  ProxyHTMLEnable On
</VirtualHost>
EOF
else
  echo "Virtual host configuration file does not exist. Creating new file..."

  # Create the virtual host configuration file
  sudo cat << EOF > /etc/apache2/sites-available/$BACKEND_HOST.conf

<VirtualHost *:80>
  ServerName ${BACKEND_HOST}

  # Proxy incoming HTTP requests to the backend server
  ProxyPass / http://${BACKEND_HOST}:5000/
  ProxyPassReverse / http://${BACKEND_HOST}:5000/

  # Allow Apache2 to handle and process the request (enables mod_proxy_html)
  ProxyHTMLEnable On
</VirtualHost>
EOF
fi

#enable virtual host
sudo a2ensite ${BACKEND_HOST}.conf
#Restart apache2
sudo systemctl reload apache2
# make and move into new directory
sudo mkdir /home/ec2-user
cd /home/ec2-user

# install maven
echo "INSTALLING MAVEN..."
sudo DEBIAN_FRONTEND=noninteractive apt install maven -y
echo "DONE!"
# check maven is installed
echo "CHECKING MAVEN VERSION..."
mvn -version
echo "DONE!"
# Install JDK (Java) 17
echo "INSTALLING JDK 17..."
sudo DEBIAN_FRONTEND=noninteractive apt install openjdk-17-jdk -y
echo "DONE!"
# check java is installed
echo "CHECKING JAVA VERSION..."
java -version
echo "DONE!"
# copy the app code to this VM
echo "CLONING REPOSITORY..."
git clone https://HenriqueMCunha@github.com/HenriqueMCunha/tech242-jsonvoorhees-app.git repo
echo "DONE!"
# move to springapi
echo "MOVING TO SPRINGAPI DIRECTORY..."
cd ~/repo/springapi
echo "DONE!"
#stop program
echo "STOPPING PROGRAM..."
mvn spring-boot:stop
echo "DONE"

# start program
echo "STARTING PROGRAM..."
mvn spring-boot:start
echo "DONE!"
```

### Instead reconfigured existing 000-default.conf file

#### Reconfigured by overwriting current 000-default.conf file 

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

cd repo/
echo "cd Into app Done!"
cd springapi/
echo "cd into springapi Done!"
# run the application
mvn spring-boot:start
echo "The App is Running!"


```
