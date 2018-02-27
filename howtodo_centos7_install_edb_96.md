Howtodo - CentOS7 - Install EnterpriseDB Postgres Developer Standard 9.6 in Text
================================================================================

#### Download installer from EnterpriseDB.
----

    + Go to https://www.enterprisedb.com/software-downloads-postgres
      - Select EDB Postgres Developer - Standard
      - Select PostgreSQL 9.6
      - Select Linux x86-64
      - Click "DOWNLOAD NOW"
    + You are required to LOGIN to download the file.
    + After download, upload the file to the linux server.
    + File : postgresql-9.6.7-1-linux-x64.run


#### Install EnterpriseDB Postgres Developer Standard 9.6 in text mode
----

    # sudo chmod +x postgresql-9.6.7-1-linux-x64.run
    # sudo ./postgresql-9.6.7-1-linux-x64.run
	
    [sudo] password for user: 
	----------------------------------------------------------------------------
	Welcome to the PostgreSQL Setup Wizard.
	
	----------------------------------------------------------------------------
	Please specify the directory where PostgreSQL will be installed.
	
	Installation Directory [/opt/PostgreSQL/9.6]: 
	
	----------------------------------------------------------------------------
	Please select a directory under which to store your data.
	
	Data Directory [/opt/PostgreSQL/9.6/data]: 
	
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
	[3] aa_DJ.iso88591
    .
    .
    .
	[769] zh_TW.euctw
	[770] zh_TW.utf8
	[771] zu_ZA
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
     


#### Notes

    Installation path : /opt/PostgreSQL/9.6
    Configuration path : /opt/PostgreSQL/9.6/data
    Log path : /opt/PostgreSQL/9.6/data/pg_log
    Utility path : /opt/PostgreSQL/9.6/bin
    
    The installation come with pgAdmin4 v2.1 client.

#### Edit /opt/PostgreSQL/9.6/pg_hba.conf 
----

Comment the existing and replace with new configuration to allow access from any IPv4 and IPv6

    # IPv4 local connections: 
    #host    all             all             127.0.0.1/32            md5
    host    all             all             0.0.0.0/0               md5

    # IPv6 local connections:
    #host    all             all             ::1/128                 md5
    host    all             all             ::/0                    md5

    # sudo systemctl status restart
    # sudo systemctl status postgresql-9.6



#### Connect to database using psql
----

    # cd /opt/PostgreSQL/9.6/bin
    # ./psql -h 127.0.0.1 -p 5432 -U postgres

    To exit psql
    postgres=# \q



#### plplython3u
----

	As root user,
    # ldd /opt/PostgreSQL/9.6/lib/postgresql/plpython3.so
	   linux-vdso.so.1 =>  (0x00007ffc431fb000)
	   libpython3.3m.so.1.0 => not found
	   libc.so.6 => /lib64/libc.so.6 (0x00007f2f59687000)
	   /lib64/ld-linux-x86-64.so.2 (0x0000557e39c48000)
    
    ** not that libpython3.3m.so.1.0 not found ** 


    To install python 3.3
      # yum -y install centos-release-scl
      # yum -y update
      # yum -y install python33


    Add to root environment 
  	  # vim ~/.bash_profile
	  export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/rh/python33/root/usr/lib64

    To reload .bash_profile 
      # source ~/.bash_profile  

    Check if plpython3.so has all the dependencies 
	# ldd /opt/PostgreSQL/9.6/lib/postgresql/plpython3.so 
		linux-vdso.so.1 =>  (0x00007ffdacbf0000)
		libpython3.3m.so.1.0 => /opt/rh/python33/root/usr/lib64/libpython3.3m.so.1.0 (0x00007f8ed65d3000)
		libc.so.6 => /lib64/libc.so.6 (0x00007f8ed61fa000)
		libpthread.so.0 => /lib64/libpthread.so.0 (0x00007f8ed5fde000)
		libdl.so.2 => /lib64/libdl.so.2 (0x00007f8ed5dda000)
		libutil.so.1 => /lib64/libutil.so.1 (0x00007f8ed5bd6000)
		libm.so.6 => /lib64/libm.so.6 (0x00007f8ed58d4000)
		/lib64/ld-linux-x86-64.so.2 (0x0000559f98a91000)

    Make sure postgresql can find libpython3.3m.so.1.0
    # vim /etc/ld.so.conf
      include ld.so.conf.d/*.conf
      /opt/rh/python33/root/usr/lib64

    Restart postgresql-9.6
    # systemctl restart postgresql-9.6



#### Add plplython3u
----
    
    In PostgreSQL, select the database to have plpython3u language.  
    
    CREATE LANGUAGE plpython3u;


#### Source
----

[Source 1](https://community.postgresrocks.net/t5/PostgreSQL/CREATE-LANGUAGE-plpython3u-on-PostgreSQL-9-6/td-p/587) | [Source 2](https://www.enterprisedb.com/docs/en/9.6/instguide/EDB_Postgres_Advanced_Server_Installation_Guide.1.50.html)
