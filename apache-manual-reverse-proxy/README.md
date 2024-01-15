# Apache Manual Proxy

- [Apache Manual Proxy](#apache-manual-proxy)
  - [Set up an APache Web Server](#set-up-an-apache-web-server)
  - [Configure Apache Web Server Reverse Proxy](#configure-apache-web-server-reverse-proxy)
    - [Update and Upgrade Virtual Machine](#update-and-upgrade-virtual-machine)
    - [Install apache web server](#install-apache-web-server)
    - [Start and enable apache web server and reload source](#start-and-enable-apache-web-server-and-reload-source)


## Set up an APache Web Server

## Configure Apache Web Server Reverse Proxy


### Update and Upgrade Virtual Machine

```
sudo apt update -y
sudo DEBIAN_FRONTEND=noninteractive apt upgrade -y
```
### Install apache web server

```
sudo DEBIAN_FRONTEND=noninteractive apt install apache2 -y
```
### Start and enable apache web server and reload source

```
sudo systemctl start apache2
sudo systemctl enable apache2

sudo a2enmod proxy
sudo a2enmod proxy_http
sudo a2enmod proxy_html

sudo nano /etc/apache2/sites-available/json.com.conf

<VirtualHost *:80>
  ServerName json.com

  # Proxy incoming HTTP requests to the backend server
  ProxyPass / http://3.250.126.232:5000/
  # ProxyPassReverse / http://3.250.126.232:5000/

  # Allow Apache2 to handle and process the request (enables mod_proxy_html)
  ProxyHTMLEnable On
</VirtualHost>

sudo a2ensite json.com.conf

sudo systemctl restart apache2

```
