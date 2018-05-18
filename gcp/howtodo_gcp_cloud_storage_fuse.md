Howtodo - GCP - Cloud Storage FUSE for CentOS
=============================================


#### Create Google Cloud Storage

    * Select project.
    * Storage > Browser > Create Bucket
        Name : project-storage
        Default storage class : Coldline
        Location : asia-southeast1 (Nearer to GCE instance zone)
    * Create



#### Add GCS FUSE Repository
----

Create the file /etc/yum.repos.d/gcsfuse.repo

    $ sudo su
    # vi /etc/yum.repos.d/gcsfuse.repo
	
        [gcsfuse]
        name=gcsfuse (packages.cloud.google.com)
        baseurl=https://packages.cloud.google.com/yum/repos/gcsfuse-el7-x86_64
        enabled=1
        gpgcheck=1
        repo_gpgcheck=1
        gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg
            https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg

    
#### Install GCS FUSE
----

    # yum update

        gcsfuse/signature                                        |  454 B     00:00     
        Retrieving key from https://packages.cloud.google.com/yum/doc/yum-key.gpg
        Importing GPG key 0xA7317B0F:
        Userid     : "Google Cloud Packages Automatic Signing Key <gc-team@google.com>"
        Fingerprint: d0bc 747f d8ca f711 7500 d6fa 3746 c208 a731 7b0f
        From       : https://packages.cloud.google.com/yum/doc/yum-key.gpg
        Is this ok [y/N]: y


    # yum install gcsfuse

        Loaded plugins: fastestmirror
        Loading mirror speeds from cached hostfile
        * base: ftp.jaist.ac.jp
        * epel: mirrors.cat.pdx.edu
        * extras: ftp.jaist.ac.jp
        * updates: ftp.jaist.ac.jp
        Resolving Dependencies
        --> Running transaction check
        ---> Package gcsfuse.x86_64 0:0.23.0-1 will be installed
        --> Processing Dependency: fuse for package: gcsfuse-0.23.0-1.x86_64
        --> Running transaction check
        ---> Package fuse.x86_64 0:2.9.2-10.el7 will be installed
        --> Finished Dependency Resolution

        Dependencies Resolved

        ================================================================================
        Package          Arch            Version                Repository        Size
        ================================================================================
        Installing:
        gcsfuse          x86_64          0.23.0-1               gcsfuse          4.0 M
        Installing for dependencies:
        fuse             x86_64          2.9.2-10.el7           base              86 k

        Transaction Summary
        ================================================================================
        Install  1 Package (+1 Dependent package)

        Total download size: 4.1 M
        Installed size: 12 M
        Is this ok [y/d/N]: y
        Downloading packages:
        (1/2): fuse-2.9.2-10.el7.x86_64.rpm                        |  86 kB   00:01     
        (2/2): 3d443dea01de786bd6da54e11f1a7d76632d401ce75fde47100 | 4.0 MB   00:02     
        --------------------------------------------------------------------------------
        Total                                              1.7 MB/s | 4.1 MB  00:02     
        Running transaction check
        Running transaction test
        Transaction test succeeded
        Running transaction
        Installing : fuse-2.9.2-10.el7.x86_64                                     1/2 
        Installing : gcsfuse-0.23.0-1.x86_64                                      2/2 
        Verifying  : fuse-2.9.2-10.el7.x86_64                                     1/2 
        Verifying  : gcsfuse-0.23.0-1.x86_64                                      2/2 

        Installed:
        gcsfuse.x86_64 0:0.23.0-1                                                     

        Dependency Installed:
        fuse.x86_64 0:2.9.2-10.el7                                                    

        Complete!


#### Credentials Options
----

    Option 1 : Set Cloud API access scopes 

        * Stop the GCE instance.
        * Edit the GCE instance.
            - Access scopes : Set access for each API
            - Storage : Full
        * Start the GCE instance.


    Option 2 : Use Spplication Default Credentials

        * SSH into GCE instance
        * Run the command

            $ gloud auth application-default login

            You are running on a Google Compute Engine virtual machine.
            The service credentials associated with this virtual machine
            will automatically be used by Application Default
            Credentials, so it is not necessary to use this command.

            If you decide to proceed anyway, your user credentials may be visible
            to others with access to this virtual machine. Are you sure you want
            to authenticate with your personal account?

            Do you want to continue (Y/n)?  Y

            Go to the following link in your browser:

                https://accounts.google.com/o/oauth2/auth?redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob&prompt=select_account&response_type=code&client_id=764086051850-6qr4p6gpi6hn506pt8ejuq83di341hur.apps.googleusercontent.com&scope=https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fuserinfo.email+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fcloud-platform&access_type=offline


            Enter verification code: 4/AAA3zZGL1bX-M7rccNa7nfjJNxW670LtgieVo_QoqXFBlWpdBEp1_Io

            Credentials saved to file: [/home/user/.config/gcloud/application_default_credentials.json]

            These credentials will be used by any library that requests
            Application Default Credentials.

            To generate an access token for other uses, run:
            gcloud auth application-default print-access-token


#### Mount GCS in GCE instance

	$ sudo su
    # mkdir -p /mnt/gcs
    # gcsfuse project-storage /mnt/gcs
    
    [Verify]
    # df -h
        Filesystem                Size  Used Avail Use% Mounted on
        project-storage           1.0P     0  1.0P   0% /mnt/gcs

    [Unmount]
    # fusermount -u /mnt/gcs


#### Auto Mount GCS in GCE instance

    [Auto mount]
    # vi /etc/fstab
        project-storage /mnt/gcs gcsfuse rw,noauto,user

    Note:
        You might want to ensure root user password are set.
        Just incase boot up failed and access by serial.  
    

#### Source
----
[GCS FUSE](https://github.com/GoogleCloudPlatform/gcsfuse/blob/master/docs/mounting.md) | [Cloud Storage FUSE](https://cloud.google.com/storage/docs/gcs-fuse)


