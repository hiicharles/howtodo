Howtodo - CentOS7 - Install MATE Desktop
========================================

#### Install Extra Packages for Enterprise Linux (EPEL).
----

    # sudo yum install epel-release
    # sudo yum -y update
    # sudo reboot 



#### Install MATE Desktop
----

    # yum groupinstall "X Window System"
    # yum groupinstall "MATE Desktop"
     


#### Enable GUI on system start
----

    # systemctl isolate graphical.target
    # systemctl set-default graphical.target
    # reboot now



#### Source
----
[Source](https://www.45drives.com/wiki/index.php?title=Installing_MATE_on_CentOS_7)
