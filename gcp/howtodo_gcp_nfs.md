Howtodo - GCP - Setup EDB Postgresql 9.5 
========================================


#### Pre-requisite files
----

	* postgresql-9.5.12-2-linux-x64.run
	* edb_languagepack_95.bin


#### Upload the files to your Google Cloud Compute Engine
----

	$ sftp user@35.187.X.X
	sftp> put postgresql-9.5.12-2-linux-x64.run
	sftp> put edb_languagepack_95.bin

	

#### Change permission
----

Connect to compute engine.

	$ ssh user@35.187.X.X


Make the files executable.

	$ sudo chmod +x postgresql-9.5.12-2-linux-x64.run
	$ sudo chmod +x edb_languagepack_95.bin


#### Install Postgresql 9.5

	$ sudo ./postgresql-9.5.12-2-linux-x64.run --mode text

		----------------------------------------------------------------------------
		Welcome to the PostgreSQL Setup Wizard.
		
		----------------------------------------------------------------------------
		Please specify the directory where PostgreSQL will be installed.
		
		Installation Directory [/opt/PostgreSQL/9.5]: 
		
		----------------------------------------------------------------------------
		Please select a directory under which to store your data.
		
		Data Directory [/opt/PostgreSQL/9.5/data]: 
		
		----------------------------------------------------------------------------
		Please provide a password for the database superuser (postgres). A locked Unix 
		user account (postgres) will be created if not present.
		
		Password :
		Retype password :
		----------------------------------------------------------------------------
		Please select the port number the server should listen on.
		
		Port [5432]: 
		
		----------------------------------------------------------------------------
		Advanced Options
		
		Select the locale to be used by the new database cluster.
		
		Locale
		
		[1] [Default locale]
		[2] aa_DJ
		.
		.
		[772] zu_ZA.iso88591
		[773] zu_ZA.utf8
		Please choose an option [1] : 
		
		----------------------------------------------------------------------------
		Setup is now ready to begin installing PostgreSQL on your computer.
		
		Do you want to continue? [Y/n]: Y
		
		----------------------------------------------------------------------------
		Please wait while Setup installs PostgreSQL on your computer.
		
		 Installing
		 0% ______________ 50% ______________ 100%
		 #########################################
		
		----------------------------------------------------------------------------
		Setup has finished installing PostgreSQL on your computer.



#### Install EDB Language Pack 9.5

	$ sudo ./edb_languagepack_95.bin --mode text

		Language Selection
		
		Please select the installation language
		[1] English - English
		Please choose an option [1] : 1
		----------------------------------------------------------------------------
		Welcome to the Language Pack Setup Wizard.
		
		----------------------------------------------------------------------------
		Setup is now ready to begin installing on your computer.
		
		/opt/EnterpriseDB/LanguagePack/9.5
		
		Do you want to continue? [Y/n]: Y
		
		----------------------------------------------------------------------------
		Please wait while Setup installs Language Pack on your computer.
		
		 Installing Language Pack
		 0% ______________ 50% ______________ 100%
		 #########################################
		
		----------------------------------------------------------------------------
		EnterpriseDB is the leading provider of value-added products and services for 
		the Postgres community.
		
		Please visit our website at www.enterprisedb.com


#### Important

    Installation path 	: /opt/PostgreSQL/9.5
    Configuration path 	: /opt/PostgreSQL/9.5/data
    Log path 			: /opt/PostgreSQL/9.6/data/pg_log
    Binary path 		: /opt/PostgreSQL/9.6/bin
	EDB Language Pack	: /opt/EnterpriseDB/LanguagePack/9.5
    

#### Edit /opt/PostgreSQL/9.5/data/pg_hba.conf 
----

Add new access.

	$ sudo vi /opt/PostgreSQL/9.5/data/pg_hba.conf

		# IPv4 local connections:
		host    all             all             127.0.0.1/32            md5
		host    all             all             10.148.0.0/24           md 
		host    all             all             211.24.X.X/32       md5

    $ sudo systemctl reload postgresql-9.6
    $ sudo systemctl status postgresql-9.6



#### Verify database is working fine
----

    # cd /opt/PostgreSQL/9.5/bin
    # ./psql -h 127.0.0.1 -p 5432 -U postgres

    To exit psql
    postgres=# \q


#### Enabling plpython3u
----

	Check if plpython3.so met required dependencies
    $ ldd /opt/PostgreSQL/9.5/lib/postgresql/plpython3.so

		linux-vdso.so.1 =>  (0x00007ffff9192000)
		libpython3.3m.so.1.0 => not found
		libc.so.6 => /lib64/libc.so.6 (0x00007feec953e000)
		/lib64/ld-linux-x86-64.so.2 (0x000055b86569d000)

    ** not that libpython3.3m.so.1.0 not found ** 


    Add to root environment 
  	# vi ~/.bashrc
    
      PYTHONHOME=/opt/EnterpriseDB/LanguagePack/9.5/Python-3.3
      export LD_LIBRARY_PATH=$PYTHONHOME/lib:$LD_LIBRARY_PATH

    To reload .bashrc 
    # source ~/.bashrc  

    Check if plpython3.so has all the dependencies
    
    Check if plpython3.so met required dependencies
    $ ldd /opt/PostgreSQL/9.5/lib/postgresql/plpython3.so

		linux-vdso.so.1 =>  (0x00007ffc87aae000)
		libpython3.3m.so.1.0 => /opt/EnterpriseDB/LanguagePack/9.5/Python-3.3/lib/libpython3.3m.so.1.0 (0x00007fa2e0975000)
		libc.so.6 => /lib64/libc.so.6 (0x00007fa2e05ac000)
		libpthread.so.0 => /lib64/libpthread.so.0 (0x00007fa2e0390000)
		libdl.so.2 => /lib64/libdl.so.2 (0x00007fa2e018c000)
		libutil.so.1 => /lib64/libutil.so.1 (0x00007fa2dff88000)
		libm.so.6 => /lib64/libm.so.6 (0x00007fa2dfc86000)
		/lib64/ld-linux-x86-64.so.2 (0x00005569c7194000)


    Add to ld.so.conf
    # vi /etc/ld.so.conf
      include ld.so.conf.d/*.conf
      /opt/EnterpriseDB/LanguagePack/9.5/Python-3.3/lib/

      
    Refresh ldconfig.
    # ldconfig

    Restart postgresql-9.5
    # systemctl restart postgresql-9.5


#### Add plplython3u language
----
    
    In PostgreSQL, select the database to have plpython3u language.
    $ cd /opt/PostgreSQL/9.5/bin
    $ ./psql -h 127.0.0.1 -p 5432 -U postgres
    postgres=# CREATE LANGUAGE plpython3u;
	postgres=# \q


#### Add pika (support python 3.3) for RabbitMQ 
----

    Download pika-0.11.2
	# cd /opt/EnterpriseDB/LanguagePack/9.5/ 
    # wget https://pypi.python.org/packages/d9/4d/e29eed9904ce16787a1e869fd93c733f0b053c6b6e7a22741be83f93e69a/pika-0.11.2.tar.gz#md5=2cd012637a43e927f8ae2d86e1e1efd5
    # tar -zxvf pika-0.11.2.tar.gz
    # cd pika-0.11.2

    Build pika
    In the pika-0.11.2, run
    -- For 9.5
    # /opt/EnterpriseDB/LanguagePack/9.5/Python-3.3/bin/python3.3 setup.py install

	Pika installed at  
    /opt/EnterpriseDB/LanguagePack/9.6/Python-3.3/lib/python3.3/site-packages/pika-0.11.2-py3.3.eggpika-0.11.2-py3.3.egg

    Restart postgresql-9.5
    # systemctl restart postgresql-9.5


#### Add firewall rule to Compute Engine

	$ gcloud compute firewall-rules create default-allow-pgsql --allow tcp:5432 --direction INGRESS
	
	Creating firewall.../Created [https://www.googleapis.com/compute/v1/projects/rakutentrade-uat/global/firewalls/default-allow-pgsql].                                                                                                         
	Creating firewall...done.                                                                                                                                                                                                                    
	NAME                 NETWORK  DIRECTION  PRIORITY  ALLOW     DENY
	default-allow-pgsql  default  INGRESS    1000      tcp:5432

	$ gcloud compute firewall-rules list
	NAME                    NETWORK  DIRECTION  PRIORITY  ALLOW                         DENY
	default-allow-icmp      default  INGRESS    65534     icmp
	default-allow-internal  default  INGRESS    65534     tcp:0-65535,udp:0-65535,icmp
	default-allow-pgsql     default  INGRESS    1000      tcp:5432
	default-allow-rdp       default  INGRESS    65534     tcp:3389
	default-allow-ssh       default  INGRESS    65534     tcp:22
	
	To show all fields of the firewall, please show in JSON format: --format=json
	To show all fields in table format, please see the examples in --help.



#### Add firewall rule to CentOS 7

	# firewall-cmd --zone=public --add-port=5432/tcp --permanent 

#### Source
----
[Language Pack Installers](http://get.enterprisedb.com/docs/README-languagepack-950.txt) | 
[Using Firewall Rules](https://cloud.google.com/vpc/docs/using-firewalls)



