Howtodo - CentOS7 - Install EnterpriseDB Postgres Developer Standard 9.6 with PlPython and Pika
===============================================================================================

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



#### Verify database is working fine
----

    # cd /opt/PostgreSQL/9.6/bin
    # ./psql -h 127.0.0.1 -p 5432 -U postgres

    To exit psql
    postgres=# \q




#### Install EDB Language Pack
----

    Download edb_languagepack_96.bin from StackBuilder.
    # sudo ./edb_languagepack_96.bin --mode text

    Installation path at /opt/EnterpriseDB/LanguagePack/9.5/

     


#### Setup plplython3u
----

	Check if plpython3.so has required dependencies
    # ldd /opt/PostgreSQL/9.5/lib/postgresql/plpython3.so
        linux-vdso.so.1 =>  (0x00007ffff3bd1000)
        libpython3.3m.so.1.0 => not found
        libc.so.6 => /lib64/libc.so.6 (0x00007fcd47502000)
        /lib64/ld-linux-x86-64.so.2 (0x00007fcd47aea000)

    ** not that libpython3.3m.so.1.0 not found **

    # ldd /opt/PostgreSQL/9.6/lib/postgresql/plpython3.so
	   linux-vdso.so.1 =>  (0x00007ffc431fb000)
	   libpython3.3m.so.1.0 => not found
	   libc.so.6 => /lib64/libc.so.6 (0x00007f2f59687000)
	   /lib64/ld-linux-x86-64.so.2 (0x0000557e39c48000)
    
    ** not that libpython3.3m.so.1.0 not found ** 


    Add to root environment 
  	  # vim ~/.bashrc
      -- For 9.5
      PYTHONHOME=/opt/EnterpriseDB/LanguagePack/9.5/Python-3.3
      export LD_LIBRARY_PATH=$PYTHONHOME/lib:$LD_LIBRARY_PATH

      -- For 9.6
      PYTHONHOME=/opt/edb/languagepack-9.6/Python-3.3
      export LD_LIBRARY_PATH=$PYTHONHOME/lib:$LD_LIBRARY_PATH


    To reload .bashrc 
      # source ~/.bashrc  

    Check if plpython3.so has all the dependencies
    
    -- For 9.5
    ldd /opt/PostgreSQL/9.5/lib/postgresql/plpython3.so
        linux-vdso.so.1 =>  (0x00007ffe483a9000)
        libpython3.3m.so.1.0 => /opt/EnterpriseDB/LanguagePack/9.5/Python-3.3/lib/libpython3.3m.so.1.0 (0x00007f85a53df000)
        libc.so.6 => /lib64/libc.so.6 (0x00007f85a5013000)
        libpthread.so.0 => /lib64/libpthread.so.0 (0x00007f85a4df7000)
        libdl.so.2 => /lib64/libdl.so.2 (0x00007f85a4bf3000)
        libutil.so.1 => /lib64/libutil.so.1 (0x00007f85a49ef000)
        libm.so.6 => /lib64/libm.so.6 (0x00007f85a46ed000)
        /lib64/ld-linux-x86-64.so.2 (0x00007f85a5a7c000)
 
    -- For 9.6
	# ldd /opt/PostgreSQL/9.6/lib/postgresql/plpython3.so 
	  linux-vdso.so.1 =>  (0x00007fff18cb0000)
	  libpython3.3m.so.1.0 => /opt/edb/languagepack-9.6/Python-3.3/lib/libpython3.3m.so.1.0 (0x00007f634ab1a000)
	  libc.so.6 => /lib64/libc.so.6 (0x00007f634a741000)
	  libpthread.so.0 => /lib64/libpthread.so.0 (0x00007f634a525000)
	  libdl.so.2 => /lib64/libdl.so.2 (0x00007f634a321000)
	  libutil.so.1 => /lib64/libutil.so.1 (0x00007f634a11d000)
	  libm.so.6 => /lib64/libm.so.6 (0x00007f6349e1b000)
	  /lib64/ld-linux-x86-64.so.2 (0x000055b89a32f000)


    Make sure postgresql can find libpython3.3m.so.1.0
    # vim /etc/ld.so.conf
      include ld.so.conf.d/*.conf
      -- For 9.5
      /opt/EnterpriseDB/LanguagePack/9.5/Python-3.3/lib/
      
      -- For 9.6
      /opt/edb/languagepack-9.6/Python-3.3/lib/

    Refresh ldconfig.
    # ldconfig

    Restart postgresql-9.6
    # systemctl restart postgresql-9.6



#### Add plplython3u language
----
    
    In PostgreSQL, select the database to have plpython3u language.    
    postgres=# CREATE LANGUAGE plpython3u;

#### Add pika (support python 3.3)
----

    Download pika-0.11.2
    # wget https://pypi.python.org/packages/d9/4d/e29eed9904ce16787a1e869fd93c733f0b053c6b6e7a22741be83f93e69a/pika-0.11.2.tar.gz#md5=2cd012637a43e927f8ae2d86e1e1efd5
    # tar -zxvf pika-0.11.2.tar.gz
    # cd pika-0.11.2

    Build pika
    In the pika extracted folder, run
    -- For 9.5
    # /opt/EnterpriseDB/LanguagePack/9.5/Python-3.3/bin/python3.3 setup.py install  
    /opt/EnterpriseDB/LanguagePack/9.6/Python-3.3/lib/python3.3/site-packages/pika-0.11.2-py3.3.eggpika-0.11.2-py3.3.egg

    -- For 9.6
    # /opt/edb/languagepack-9.6/Python-3.3/bin/python3.3 setup.py install
    /opt/edb/languagepack-9.6/Python-3.3/lib/python3.3/site-packages/pika-0.11.2-py3.3.egg



#### Source
----

[Source 1](http://get.enterprisedb.com/docs/README-languagepack-950.txt) | [Source 2](http://get.enterprisedb.com/docs/README-edb-languagepack-9.6.txt)
