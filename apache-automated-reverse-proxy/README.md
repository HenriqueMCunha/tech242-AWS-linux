# Apache Automated Proxy

## Set up an APache Web Server

## Configure Apache Web Server Reverse Proxy
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
