# MagentoTutorial
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