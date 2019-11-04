Howtodo - Ubuntu1804 - Setup Apache 2, PHP 7.2 and Postgresql
=============================================================


### Installation of PostgreSQL
---

Refer to - [howtodo_ubuntu1804_setup_postgresql11.md](https://github.com/hiicharles/howtodo/blob/master/ubuntu/howtodo_ubuntu1804_setup_postgresql11.md)



### Installation of Apache 2
---

        $ sudo apt-get install apache2
        [sudo] password for user: ********        

                Reading package lists... Done
                Building dependency tree       
                Reading state information... Done
                The following additional packages will be installed:
                apache2-bin apache2-data apache2-utils libapr1 libaprutil1
                libaprutil1-dbd-sqlite3 libaprutil1-ldap
                Suggested packages:
                apache2-doc apache2-suexec-pristine | apache2-suexec-custom
                The following NEW packages will be installed:
                apache2 apache2-bin apache2-data apache2-utils libapr1 libaprutil1
                libaprutil1-dbd-sqlite3 libaprutil1-ldap
                0 upgraded, 8 newly installed, 0 to remove and 31 not upgraded.
                Need to get 1,604 kB of archives.
                After this operation, 6,493 kB of additional disk space will be used.
                Do you want to continue? [Y/n] Y


### Installation of PHP 7.2
---

        $ sudo apt-get install php libapache2-mod-php php-pgsql
        [sudo] password for user: ********        

                Reading package lists... Done
                Building dependency tree       
                Reading state information... Done
                The following additional packages will be installed:
                libapache2-mod-php7.2 php-common php7.2 php7.2-cli php7.2-common php7.2-json php7.2-opcache php7.2-pgsql php7.2-readline
                Suggested packages:
                php-pear
                The following NEW packages will be installed:
                libapache2-mod-php libapache2-mod-php7.2 php php-common php-pgsql php7.2 php7.2-cli php7.2-common php7.2-json php7.2-opcache php7.2-pgsql php7.2-readline
                0 upgraded, 12 newly installed, 0 to remove and 17 not upgraded.
                Need to get 3,928 kB of archives.
                After this operation, 17.4 MB of additional disk space will be used.
                Do you want to continue? [Y/n] Y





### Create Virtual Host - mysite.com
---

1. Create the site root directory in /var/www/.

        $ sudo mkdir -p /var/www/mysite_com
        

2. Copy the index.html to /var/www/mysite_com/

        $ sudo cp -p /var/www/html/index.html /var/www/mysite_com/


3. Create entries in /etc/hosts

        $ sudo nano /etc/hosts
        127.0.0.1 mysite.com
        127.0.0.1 www.mysite.com


4. Create the virtual host configuration.

        $ sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/mysite_com.conf

        $ sudo nano /etc/apache2/sites-available/mysite_com.conf
        <VirtualHost *:80>
                ServerAdmin webmaster@localhost
                ServerName mysite.com
                ServerAlias www.mysite.com
                DocumentRoot /var/www/mysite_com/
                <Directory /var/www/mysite_com>
                        Options Indexes FollowSymLinks MultiViews
                        DirectoryIndex index.php index.html 
                        AllowOverride All
                        Order Allow,Deny
                        Allow from all
                        Require all granted                        
                </Directory>
                ErrorLog ${APACHE_LOG_DIR}/error.log
                CustomLog ${APACHE_LOG_DIR}/access.log combined
        </VirtualHost>

        Note: 
        - Will search for index.php first.  Not found then search for index.html


5. Enable the virtual host.

        $ cd /etc/apache2/sites-available
        $ sudo a2ensite mysite_com.conf
        $ sudo systemctl reload apache2


6. Create a test index.php

        $ sudo nano /var/www/mysite_com/index.php

        <?php
            echo "Hello World!";
        ?>


7. Open web browser
        
        http://mysite.com
        http://www.mysite.com
        http://mysite.com/index.php



### Important Path
---

Apache 2 default document root

        /var/www/html/

Apache 2 Configuration

        /etc/apache2/apache2.conf   - Main apache2 configuration file
        /etc/apache2/ports.conf     - port apache2 listening on
        /etc/apache2/envvars        - apache2 environment variables

Apache 2 Virtual hosts

        /etc/apache2/sites-available/

Apache 2 Mods

        /etc/apache2/mods-available/

Apache 2 Logs

        /var/log/apache2/    

PHP 7.2 Configuration

        /etc/php/7.2/apache2/php.ini



### Source
---

[HTTPD - Apache2 Web Server](https://help.ubuntu.com/lts/serverguide/httpd.html)
[How to install Apache, PhP, Postgresql (LAPP) on Ubuntu 16.04](https://medium.com/@Riverside/how-to-install-apache-php-postgresql-lapp-on-ubuntu-16-04-adb00042c45d)