# MagentoTutorial

Magento 2.1 install on Windows

Structure Appache +Mysql+Magento

https://www.simicart.com/blog/how-to-install-magento-2-localhost/

The download version of xampp is win32-7.0.32-0

The download version of Magento2 is Magento 2.1.15


Magento 2.2  install on Ubuntu 16.04
Structure Appache +Mysql+Magento2

1.1Operating systems (Linux x86-64)
A Linux distribution such as RedHat Enterprise Linux (RHEL), CentOS, Ubuntu, Debian, and so on.
Here is Ubuntu 16.04 LTS and the below is the installing steps
https://tutorials.ubuntu.com/tutorial/tutorial-install-ubuntu-desktop-1604#0

1.2 Install Apache and Allow in Firewall
sudo apt-get update
sudo apt-get install apache2

sudo vim /etc/hosts
Add 
127.0.0.1 www.magento2.com 
127.0.0.1 magento2.com 
to hosts file


sudo vim /etc/apache2/apache2.conf
Add ServerName www.magento2.com to conf file

sudo systemctl restart apache2


Adjust the Firewall to Allow Web Traffic

sudo ufw app list

sudo ufw app info "Apache Full"

sudo ufw allow in "Apache Full"

1.3 MySQL

sudo apt-get install mysql-server

mysql_secure_installation

1.4 PHP
sudo apt-get install php libapache2-mod-php php-mcrypt php-mysql

sudo vim /etc/apache2/mods-enabled/dir.conf


It will look like this:

/etc/apache2/mods-enabled/dir.conf
<IfModule mod_dir.c>
    DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
</IfModule>
We want to move the PHP index file highlighted above to the first position after the DirectoryIndex specification, like this:

/etc/apache2/mods-enabled/dir.conf
<IfModule mod_dir.c>
    DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>


sudo systemctl restart apache2

sudo systemctl status apache2


apt-cache search php- | less
Use the arrow keys to scroll up and down, and q to quit.

The results are all optional components that you can install. It will give you a short description for each:

libnet-libidn-perl - Perl bindings for GNU Libidn
php-all-dev - package depending on all supported PHP development packages
php-cgi - server-side, HTML-embedded scripting language (CGI binary) (default)
php-cli - command-line interpreter for the PHP scripting language (default)
php-common - Common files for PHP packages
php-curl - CURL module for PHP [default]
php-dev - Files for PHP module development (default)
php-gd - GD module for PHP [default]
php-gmp - GMP module for PHP [default]
…
:
To get more information about what each module does, you can either search the internet, or you can look at the long description of the package by typing:

apt-cache show package_name
There will be a lot of output, with one field called Description-en which will have a longer explanation of the functionality that the module provides.

For example, to find out what the php-cli module does, we could type this:

apt-cache show php-cli
Along with a large amount of other information, you'll find something that looks like this:

Output
…
Description-en: command-line interpreter for the PHP scripting language (default)
 This package provides the /usr/bin/php command interpreter, useful for
 testing PHP scripts from a shell or performing general shell scripting tasks.
 .
 PHP (recursive acronym for PHP: Hypertext Preprocessor) is a widely-used
 open source general-purpose scripting language that is especially suited
 for web development and can be embedded into HTML.
 .
 This package is a dependency package, which depends on Debian's default
 PHP version (currently 7.0).
…
If, after researching, you decide you would like to install a package, you can do so by using the apt-get install command like we have been doing for our other software.

If we decided that php-cli is something that we need, we could type:

sudo apt-get install php-cli
If you want to install more than one module, you can do that by listing each one, separated by a space, following the apt-get install command, like this:

sudo apt-get install package1 package2 ...


sudo vim /var/www/html/info.php

This will open a blank file. We want to put the following text, which is valid PHP code, inside the file:

info.php
<?php
phpinfo();
?>

1.5 phpMyAdmin

sudo apt-get update
sudo apt-get install phpmyadmin php-mbstring php-gettext

Warning: When the first prompt appears, apache2 is highlighted, but not selected. If you do not hit Space to select Apache, the installer will not move the necessary files during installation. Hit Space, Tab, and then Enter to select Apache.

For the server selection, choose apache2.
Select yes when asked whether to use dbconfig-common to set up the database
You will be prompted for your database administrator's password
You will then be asked to choose and confirm a password for the phpMyAdmin application itself

sudo phpenmod mcrypt
sudo phpenmod mbstring

sudo systemctl restart apache2


sudo vim /etc/apache2/conf-enabled/phpmyadmin.conf 

Insert the following codes

#  
#Web application to manage MySQL  
 
#  
 
#<Directory “/usr/share/phpMyAdmin”>  
 
#Order deny,allow  
 
#Deny form all  
 
#Allow from localhost  
 
#</Directory>  
 
Alias /phpmyadmin /usr/share/phpMyAdmin  
 
Alias /phpMyAdmin /usr/share/phpMyAdmin  
 
Alias /mysqladmin /usr/share/phpMyAdmin 

sudo systemctl restart apache2

sudo rm /etc/apache2/conf-available/phpmyadmin.conf
sudo ln -s /etc/phpmyadmin/apache.conf /etc/apache2/conf-available/phpmyadmin.conf

sudo a2enconf phpmyadmin.conf

sudo vim /etc/apache2/apache2.conf
Then add the following line to the end of the file.

Include /etc/phpmyadmin/apache.conf


//sudo ln -s /usr/share/phpmyadmin /var/www/html

sudo cp /usr/share/phpmyadmin /var/www/html

sudo service apache2 reload

sudo systemctl restart apache2

sudo vim /etc/apache2/apache2.conf

http://www.magento2.com/phpmyadmin

https://www.youtube.com/watch?v=6sgRw9XSSX8

//1.6 System update
//sudo apt-get update && sudo apt-get upgrade

1.7 Magento
sudo mkdir /var/www/html/magento2

change hosts

sudo vim /etc/hosts

add 
127.0.0.1 www.magento2.com
127.0.0.1 magento2.com

cd /etc/apache2/sites-available

sudo cp 000-default.conf magento2.com.conf
sudo vim magento2.com.conf

ServerName magento2.com
ServerAlias www.magento2.com

sudo a2ensite magento.com

sudo unzip Mag* -d /var/www/html/magento2

cd /var/www/html/magento2

sudo chown -R www-data .

create database magento2;

sudo a2dismod php5.6

sudo a2enmod php7.0

sudo apt-get install -y php7.0-curl php7.0-intl php7.0-soap php7.0-zip php7.0-bcmath 

/etc/php/7.0/apache2/php.ini  
max_execution_time = 18000
max_input_time = 1800
memory_limit = 1024M


sudo systemctl restart apache2

http://www.magento2.com/magento2

chmod -R 777 pub/ var/

Magento 2.2  Install and config steps


1.System 2.2.x requirements
https://devdocs.magento.com/guides/v2.2/install-gde/system-requirements2.html
https://devdocs.magento.com/guides/v2.2/install-gde/system-requirements-tech.html
1.1Operating systems (Linux x86-64)
A Linux distribution such as RedHat Enterprise Linux (RHEL), CentOS, Ubuntu, Debian, and so on.
Here is Ubuntu 16.04 LTS and the below is the installing steps
https://tutorials.ubuntu.com/tutorial/tutorial-install-ubuntu-desktop-1604#0

1.2 Database
MySQL 5.7 and install steps
https://www.digitalocean.com/community/tutorials/how-to-install-the-latest-mysql-on-ubuntu-16-04

1.3 Composer
PHP version 7.0.32
https://www.digitalocean.com/community/tutorials/how-to-install-and-use-composer-on-ubuntu-16-04

Here is a bug for this document.

This hash value will change based on the sinature file changes

php -r "if (hash_file('SHA384', 'composer-setup.php') === '93b54496392c062774670ac18b134c3b3a95e5a5e5c8f1a9f115f203b75bf9a129d5daa8ba6a13e2cc8a1da0806388a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"

composer 1.7.2

1.4 Nginx
version 1.10.3
https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-16-04


1.5 PHP extension 

https://devdocs.magento.com/guides/v2.2/install-gde/prereq/php-ubuntu.html

https://devdocs.magento.com/guides/v2.2/install-gde/install/web/install-web.html