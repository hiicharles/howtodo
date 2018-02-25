Howtodo - CentOS7 - Install GNOME Desktop
=========================================

#### View available packages.
----
 
    # yum group list
	Loaded plugins: fastestmirror
	Loading mirror speeds from cached hostfile
	 * base: ossm.utm.my
	 * extras: ossm.utm.my
	 * updates: ossm.utm.my
	Available Environment Groups:
	   Minimal Install
	   Compute Node
	   Infrastructure Server
	   File and Print Server
	   Basic Web Server
	   Virtualization Host
	   Server with GUI
	   GNOME Desktop
	   KDE Plasma Workspaces
	   Development and Creative Workstation
	Available Groups:
	   Compatibility Libraries
	   Console Internet Tools
	   Development Tools
	   Graphical Administration Tools
	   Legacy UNIX Compatibility
	   Scientific Support
	   Security Tools
	   Smart Card Support
	   System Administration Tools
	   System Management
	Done



#### Install GNOME Desktop and Graphical Administration Tools
----

    # yum groupinstall "GNOME Desktop" "Graphical Administration Tools"



#### Enable GUI on system start
----

    # ln -sf /lib/systemd/system/runlevel5.target /etc/systemd/system/default.target
    # reboot now



#### Accept agreement
----

    * Click "LICENSE INFORMATION"
    * Click "I accept the license agreement."
    * Click "Done"
    * Click "FINISH CONFIGURATION".



#### Source
----
[Source](https://www.itzgeek.com/how-tos/linux/centos-how-tos/install-gnome-gui-on-centos-7-rhel-7.html)
