Howtodo - Ubuntu 16.04 - Installing Google Cloud SDK for Linux
===============================================================

#### Add Repository and Public Key

    echo "deb http://packages.cloud.google.com/apt cloud-sdk-xenial main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list

    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add 


#### Install

	$ sudo apt-get update
    $ sudo apt-get install google-cloud-sdk

        Reading state information... Done
        Suggested packages:
        google-cloud-sdk-app-engine-java google-cloud-sdk-app-engine-python
        google-cloud-sdk-pubsub-emulator google-cloud-sdk-bigtable-emulator
        google-cloud-sdk-datastore-emulator kubectl
        Recommended packages:
        python-crcmod
        The following NEW packages will be installed:
        google-cloud-sdk
        0 upgraded, 1 newly installed, 0 to remove and 0 not upgraded.
        Need to get 15.2 MB of archives.
        After this operation, 116 MB of additional disk space will be used.
        Get:1 http://packages.cloud.google.com/apt cloud-sdk-xenial/main amd64 google-cloud-sdk all 199.0.0-0 [15.2 MB]
        Fetched 15.2 MB in 3s (4,273 kB/s)           
        Selecting previously unselected package google-cloud-sdk.
        (Reading database ... 214046 files and directories currently installed.)
        Preparing to unpack .../google-cloud-sdk_199.0.0-0_all.deb ...
        Unpacking google-cloud-sdk (199.0.0-0) ...
        Processing triggers for man-db (2.7.5-1) ...
        Setting up google-cloud-sdk (199.0.0-0) ...
    


#### Initialize - Set user, project and zone

		$ gcloud init

			Welcome! This command will take you through the configuration of gcloud.
			
			Your current configuration has been set to: [default]
			
			You can skip diagnostics next time by using the following flag:
			  gcloud init --skip-diagnostics
			
			Network diagnostic detects and fixes local network connection issues.
			Checking network connection...done.                                                                                  
			Reachability Check passed.
			Network diagnostic (1/1 checks) passed.
			
			You must log in to continue. Would you like to log in (Y/n)?  Y
			
			Your browser has been opened to visit:
			
			    https://accounts.google.com/o/oauth2/auth?redirect_uri=http%3A%2F%2Flocalhost%3A8085%2F&prompt=select_account&response_type=code&client_id=32555940559.apps.googleusercontent.com&scope=https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fuserinfo.email+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fcloud-platform+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fappengine.admin+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fcompute+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Faccounts.reauth&access_type=offline
			
			
			[3371:3409:0422/224220.765023:ERROR:browser_gpu_channel_host_factory.cc(120)] Failed to launch GPU process.
			Created new window in existing browser session.
			You are logged in as: [user@gmail.com].
			
			Pick cloud project to use: 
			 [1] my-project
			 [2] stalwart-star-198705
			 [3] Create a new project
			Please enter numeric choice or text value (must exactly match list 
			item):  1
			
			Your current project has been set to: [my-project].
			
			Do you want to configure a default Compute Region and Zone? (Y/n)?  Y
			
			Which Google Compute Engine zone would you like to use as project 
			default?
			If you do not specify a zone via a command line flag while working 
			with Compute Engine resources, the default is assumed.
			 [1] us-east1-b
			 [2] us-east1-c
			 [3] us-east1-d
			 [4] us-east4-c
			 [5] us-east4-b
			 [6] us-east4-a
			 [7] us-central1-c
			 [8] us-central1-a
			 [9] us-central1-f
			 [10] us-central1-b
			 [11] us-west1-b
			 [12] us-west1-c
			 [13] us-west1-a
			 [14] europe-west4-a
			 [15] europe-west4-b
			 [16] europe-west4-c
			 [17] europe-west1-b
			 [18] europe-west1-d
			 [19] europe-west1-c
			 [20] europe-west3-b
			 [21] europe-west3-c
			 [22] europe-west3-a
			 [23] europe-west2-c
			 [24] europe-west2-b
			 [25] europe-west2-a
			 [26] asia-east1-b
			 [27] asia-east1-a
			 [28] asia-east1-c
			 [29] asia-southeast1-b
			 [30] asia-southeast1-a
			 [31] asia-northeast1-b
			 [32] asia-northeast1-c
			 [33] asia-northeast1-a
			 [34] asia-south1-c
			 [35] asia-south1-b
			 [36] asia-south1-a
			 [37] australia-southeast1-b
			 [38] australia-southeast1-c
			 [39] australia-southeast1-a
			 [40] southamerica-east1-b
			 [41] southamerica-east1-c
			 [42] southamerica-east1-a
			 [43] northamerica-northeast1-a
			 [44] northamerica-northeast1-b
			 [45] northamerica-northeast1-c
			 [46] Do not set default zone
			Please enter numeric choice or text value (must exactly match list 
			item):  30
			
			Your project default Compute Engine zone has been set to [asia-southeast1-a].
			You can change it by running [gcloud config set compute/zone NAME].
			
			Your project default Compute Engine region has been set to [asia-southeast1].
			You can change it by running [gcloud config set compute/region NAME].
			
			Created a default .boto configuration file at [/home/charles/.boto]. See this file and
			[https://cloud.google.com/storage/docs/gsutil/commands/config] for more
			information about configuring Google Cloud Storage.
			Your Google Cloud SDK is configured and ready to use!
			
			* Commands that require authentication will use user@gmail.com by default
			* Commands will reference project `my-project` by default
			* Compute Engine commands will use region `asia-southeast1` by default
			* Compute Engine commands will use zone `asia-southeast1-a` by default
			
			Run `gcloud help config` to learn how to change individual settings
			
			This gcloud configuration is called [default]. You can create additional configurations if you work with multiple accounts and/or projects.
			Run `gcloud topic configurations` to learn more.
			
			Some things to try next:
			
			* Run `gcloud --help` to see the Cloud Platform services you can interact with. And run `gcloud help COMMAND` to get help on any gcloud command.
			* Run `gcloud topic -h` to learn about advanced features of the SDK like arg files and output formatting


#### Modification

To update the configuration, refer to 

	$ gcloud config --help


#### Verify
----

	$ gcloud auth list

		     Credentialed Accounts
		ACTIVE  ACCOUNT
		*       user@gmail.com
		
		To set the active account, run:
		    $ gcloud config set account `ACCOUNT`


	$ gcloud config list

		[compute]
		region = asia-southeast1
		zone = asia-southeast1-a
		[core]
		account = user@gmail.com
		disable_usage_reporting = False
		project = my-project

	$ gcloud info

		Google Cloud SDK [198.0.0]
		
		Platform: [Linux, x86_64] ('Linux', 'ubuntu', '4.13.0-38-generic', '#43~16.04.1-Ubuntu SMP Wed Mar 14 17:48:43 UTC 2018', 'x86_64', 'x86_64')
		Python Version: [2.7.12 (default, Dec  4 2017, 14:50:18)  [GCC 5.4.0 20160609]]
		Python Location: [/usr/bin/python2]
		Site Packages: [Disabled]
		
		Installation Root: [/home/user/Downloads/google-cloud-sdk]
		Installed Components:
		  core: [2018.04.13]
		  gsutil: [4.30]
		  bq: [2.0.32]
		System PATH: [/home/user/Downloads/google-cloud-sdk/bin:/home/user/bin:/home/user/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/usr/lib/jvm/java-9-oracle/bin:/usr/lib/jvm/java-9-oracle/db/bin]
		Python PATH: [/home/user/Downloads/google-cloud-sdk/lib/third_party:/home/user/Downloads/google-cloud-sdk/lib:/usr/lib/python2.7/:/usr/lib/python2.7/plat-x86_64-linux-gnu:/usr/lib/python2.7/lib-tk:/usr/lib/python2.7/lib-old:/usr/lib/python2.7/lib-dynload]
		Cloud SDK on PATH: [True]
		Kubectl on PATH: [False]
		
		Installation Properties: [/home/user/Downloads/google-cloud-sdk/properties]
		User Config Directory: [/home/user/.config/gcloud]
		Active Configuration Name: [default]
		Active Configuration Path: [/home/user/.config/gcloud/configurations/config_default]
		
		Account: [user@gmail.com]
		Project: [my-project]
		
		Current Properties:
		  [core]
		    project: [my-project]
		    account: [user@gmail.com]
		    disable_usage_reporting: [False]
		  [compute]
		    region: [asia-southeast1]
		    zone: [asia-southeast1-a]
		
		Logs Directory: [/home/user/.config/gcloud/logs]
		Last Log File: [/home/user/.config/gcloud/logs/2018.04.22/22.49.17.976458.log]
		
		git: [git version 2.7.4]
		ssh: [OpenSSH_7.2p2 Ubuntu-4ubuntu2.4, OpenSSL 1.0.2g  1 Mar 2016]


	$ gcloud help

	$ gcloud help compute instances create



#### Source
----
[Quickstart for Debian and Ubuntu](https://cloud.google.com/sdk/docs/quickstart-debian-ubuntu)

