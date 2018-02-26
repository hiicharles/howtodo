Howtodo - CentOS7 - Install Virtualbox Guest Additions
======================================================

#### Update kernel
----

    # sudo yum update kernel*
    # sudo reboot 



#### Install Extra Packages for Enterprise Linux (EPEL).
----

    # sudo yum install epel-release
    # sudo yum -y update
    # sudo reboot 



#### Install required packages
----

    # sudo yum install gcc kernel-devel kernel-headers dkms make bzip2 perl
    # sudo reboot


### Install Virtual Box GuestAdditions
----

    # Download latest Guest Additions ISO from website.
    # Use the autorun.  
   
Alternatively, Open Terminal and type the following commands

    # cd /run/media/user/VBox_GAs_5.2.7
    # ./VBoxLinuxAdditions.run
    # sudo reboot



#### Source
----
[Source](https://www.if-not-true-then-false.com/2010/install-virtualbox-guest-additions-on-fedora-centos-red-hat-rhel/)


