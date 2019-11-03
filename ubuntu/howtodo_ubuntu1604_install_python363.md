Howtodo - Ubuntu 16.04 - Install Python 3.6.3
=============================================

#### Note

Ubuntu 16.04 came with 

	* Python 2.7.12
	* Python 3.5.2


#### Install Python 3.6.5
----

	# sudo apt-get install software-properties-common python-software-properties
	# sudo add-apt-repository ppa:jonathonf/python-3.6
 	# sudo apt-get update
	# sudo apt-get install python3.6

	Reading package lists... Done
	Building dependency tree       
	Reading state information... Done
	The following additional packages will be installed:
	  libpython3.6-minimal libpython3.6-stdlib python3.6-minimal
	Suggested packages:
	  python3.6-venv python3.6-doc binfmt-support
	The following NEW packages will be installed:
	  libpython3.6-minimal libpython3.6-stdlib python3.6 python3.6-minimal
	0 upgraded, 4 newly installed, 0 to remove and 1 not upgraded.
	Need to get 4,361 kB of archives.
	After this operation, 23.7 MB of additional disk space will be used.
	Do you want to continue? [Y/n] Y


#### Verify installation
----

    # python3.6 -V
    Python 3.6.3
  


#### Source
----
[How to Install Python 3.6 on Ubuntu 16.04](https://www.rosehosting.com/blog/how-to-install-python-3-6-on-ubuntu-16-04/)

