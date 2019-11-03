Howtodo - Ubuntu1804 - Setup Apache 2
======================================


### Installation
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
                ErrorLog ${APACHE_LOG_DIR}/error.log
                CustomLog ${APACHE_LOG_DIR}/access.log combined
        </VirtualHost>


5. Enable the virtual host.

        $ cd /etc/apache2/sites-available
        $ sudo a2ensite mysite_com.conf
        $ sudo reload apache2


6. Open web browser
        
        http://mysite.com
        http://www.mysite.com



### Important Path
---

        # Default document root
        /var/www/html/

        # Configuration
        /etc/apache2/apache2.conf   - Main apache2 configuration file
        /etc/apache2/ports.conf     - port apache2 listening on
        /etc/apache2/envvars        - apache2 environment variables

        # Virtual hosts
        /etc/apache2/sites-available/

        # Mods
        /etc/apache2/mods-available/

        # Logs
        /var/log/apache2/    


### Source
---
[HTTPD - Apache2 Web Server](https://help.ubuntu.com/lts/serverguide/httpd.html)