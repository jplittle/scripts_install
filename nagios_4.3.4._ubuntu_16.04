#!/bin/bash
sudo apt-get update;
sudo apt-get install tree;
sudo apt-get install autoconf gcc libc6 make wget unzip apache2 php libapache2-mod-php7.0 libgd2-xpm-dev -y;
cd /tmp;
wget -O nagioscore.tar.gz https://github.com/NagiosEnterprises/nagioscore/archive/nagios-4.3.4.tar.gz;
tar xzf nagioscore.tar.gz;
cd /tmp/nagioscore-nagios-4.3.4;
sudo ./configure --with-httpd-conf=/etc/apache2/sites-enabled;
sudo make all;
sudo useradd nagios;
sudo usermod -a -G nagios www-data;
sudo make install;
sudo make install-init;
sudo update-rc.d nagios defaults;
sudo make install-commandmode;
sudo make install-config;
sudo make install-webconf;
sudo a2enmod rewrite;
sudo a2enmod cgi;
sudo ufw allow Apache;
sudo ufw reload;
sudo htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin;
sudo systemctl restart apache2.service;
sudo systemctl start nagios.service;
sudo apt-get install -y autoconf gcc libc6 libmcrypt-dev make libssl-dev wget bc gawk dc build-essential snmp libnet-snmp-perl gettext;
cd /tmp;
wget --no-check-certificate -O nagios-plugins-2.2.1.tar.gz https://nagios-plugins.org/download/nagios-plugins-2.2.1.tar.gz;
tar zxf nagios-plugins-2.2.1.tar.gz;
cd /tmp/nagios-plugins-2.2.1;
sudo ./configure;
sudo make;
sudo make install;


sudo systemctl stop nagios.service;    
sudo systemctl start nagios.service;   
sudo systemctl restart nagios.service; 
sudo systemctl status nagios.service;

sed -i "s|#cfg_file=/usr/local/nagios/etc/objects/windows.cfg|cfg_file=/usr/local/nagios/etc/objects/windows.cfg|" /etc/nagios/nagios.cfg
sed -i "
/alias grep/ {
n
a\alias prefly='sudo /usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg'
a\alias fly='sudo /usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg; sudo service nagios restart'
a\alias mknag='cd /usr/local/nagios/etc/objects'
a\alias cls='clear'
a\alias nano='sudo nano'
a\alias reboot='sudo reboot'
a\alias snr='sudo service nagios restart'
:a;n;ba}" ~/.bashrc;
. ~/.bashrc



