Howtodo - CentOS7 - Install MATE Desktop
========================================

#### Install Extra Packages for Enterprise Linux (EPEL).
----

    # sudo yum install epel-release
    # sudo yum -y update
    # sudo reboot 



#### Install MATE Desktop
----

    # yum groupinstall mate-desktop
    # yum groupinstall "X Window System"



#### Enable GUI on system start
----

    # systemctl set-default graphical.target
    # reboot now



#### Source
----
[Source](http://wiki.mate-desktop.org/download)
