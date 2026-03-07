# DVWA Installation on Raspberry Pi

## Operating System

Using Raspberry Pi Imager:

- OS: Raspberry Pi OS (32-bit)
- Hostname: dvwa-pi
- Username: user
- Enable SSH
- Configure Wi-Fi (SSID and password)

Write the image to the SD card and boot the Raspberry Pi.

Connect to the Raspberry Pi using SSH:

```bash
ssh user@<raspberry-ip>

Update the system
sudo apt update && sudo apt upgrade -y

Install dependencies (LAMP stack)
sudo apt install apache2 mariadb-server php php-mysqli php-gd libapache2-mod-php git -y

Restart Apache:
sudo systemctl restart apache2

Download DVWA
cd /var/www/html
sudo git clone https://github.com/digininja/DVWA.git

Set permissions
sudo chown -R www-data:www-data /var/www/html/DVWA
sudo chmod -R 755 /var/www/html/DVWA

Configure DVWA
Edit the configuration file:
cd /var/www/html/DVWA/config
sudo cp config.inc.php.dist config.inc.php
sudo mysql
CREATE DATABASE dvwa;
CREATE USER 'dvwa'@'localhost' IDENTIFIED BY 'p@ssw0rd';
GRANT ALL PRIVILEGES ON dvwa.* TO 'dvwa'@'localhost';
FLUSH PRIVILEGES;
EXIT;

Initialize DVWA
Open your browser and go to:
http://<raspberry-ip>/DVWA/setup.php

Click Create / Reset Database.
DVWA should now be ready to use.

Access DVWA
http://<raspberry-ip>/DVWA/

Default credentials:
admin / password

SECURITY NOTES
DVWA is intentionally vulnerable.
Use it only in an isolated lab environment.
