Howtodo - Ubuntu1804 - Setup PostgreSQL 11
==========================================


### Installation
---

        # Repository signing key
        $ wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -


        # Add repository
        $ echo "deb http://apt.postgresql.org/pub/repos/apt/ bionic-pgdg main" | sudo tee /etc/apt/sources.list.d/pgdg.list

        # Install postgresql server and client
        $ sudo apt-get update
        $ sudo apt-get install postgresql-11 postgresql-client-11 postgresql-doc-11

                Reading package lists... Done
                Building dependency tree       
                Reading state information... Done
                The following additional packages will be installed:
                libllvm6.0 libpq5 pgdg-keyring postgresql-client-common postgresql-common
                Recommended packages:
                sysstat
                The following NEW packages will be installed:
                libllvm6.0 pgdg-keyring postgresql-11 postgresql-client-11 postgresql-client-common postgresql-common postgresql-doc-11
                The following packages will be upgraded:
                libpq5
                1 upgraded, 7 newly installed, 0 to remove and 17 not upgraded.
                Need to get 32.3 MB of archives.
                After this operation, 128 MB of additional disk space will be used.
                Do you want to continue? [Y/n] Y        


### Configuration

1. Edit /etc/postgresql/11/main/pg_hba.conf

        $ sudo nano /etc/postgresql/11/main/pg_hba.conf
        
        # IPv4 local connections:
        host    all             all             127.0.0.1/32            trust
        host    all             all             0.0.0.0/0               md5


2. Edit /etc/postgresql/11/main/postgresql.conf

        $ sudo nano /etc/postgresql/11/main/postgresql.conf
        
        listen_addresses = '*'          # what IP address(es) to listen on;


3. Restart to take effect.

        $ sudo systemctl restart postgresql


4. Change password for postgresql.

        $ psql -h 127.0.0.1 -p 5432 -U postgres -w postgres

                psql (11.5 (Ubuntu 11.5-3.pgdg18.04+1))
                SSL connection (protocol: TLSv1.3, cipher: TLS_AES_256_GCM_SHA384, bits: 256, compression: off)
                Type "help" for help.

                postgres=# \password postgres
                Enter new password: ********
                Enter it again: ********
                postgres=# \q

Note:

You can install pgadmin4 to connect to the server.  Default database `postgres` and default user `postgres` using the password your set in step 4.



### Important Path
---

Configuration

        /etc/postgresql/11/main/

Binary folder

        /usr/lib/postgresql/11/bin


Data folder

        /var/lib/postgresql/11/main/

Log folder

        /var/log/postgresql/





