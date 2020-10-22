Howtodo - Ubuntu 20.04 - Hostname, Host and Static IP
=====================================================

### Hostname
---
Set hostname

	$ sudo vi /etc/hostname
    kmaster.local

    # sudo reboot now

Retrieve hostname information

    $ hostname -s
    kmaster

    $ hostname -A
    kmaster.local

    $ hostname -f
    kmaster.local

    $ hostname -i
    192.168.1.x


    Note : 
        Always edit /etc/hosts when change the hostname

	

### Hosts
---------

Hosts file will define hostname to specified ip address
Edit /etc/hosts


	$ sudo vi /etc/hosts
    127.0.0.1 localhost kmaster kmaster.local

    Note : 
        When use localhost, kmaster or kmaster.local in the system, it will alwaus resolve to 127.0.0.1 (loopback).


### Static IP
-------------

List network adapter

    $ ip addr
    1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group defaul                                                                                                            t qlen 1000
        link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
        inet 127.0.0.1/8 scope host lo
        valid_lft forever preferred_lft forever
        inet6 ::1/128 scope host
        valid_lft forever preferred_lft forever
    2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group defa                                                                                                            ult qlen 1000
        link/ether dc:a6:32:12:d5:01 brd ff:ff:ff:ff:ff:ff
        inet 192.168.1.102/24 brd 192.168.1.255 scope global dynamic eth0
        valid_lft 2058sec preferred_lft 2058sec
        inet6 fe80::dea6:32ff:fe12:d501/64 scope link
        valid_lft forever preferred_lft forever
    3: wlan0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN group default qle                                                                                                            n 1000
        link/ether dc:a6:32:12:d5:02 brd ff:ff:ff:ff:ff:ff


Change `eth0` to static ip 
    
Before change:

    $ cat /etc/netplan/50-cloud-init.yaml
    # This file is generated from information provided by the datasource.  Changes
    # to it will not persist across an instance reboot.  To disable cloud-init's
    # network configuration capabilities, write a file
    # /etc/cloud/cloud.cfg.d/99-disable-network-config.cfg with the following:
    # network: {config: disabled}
    network:
        ethernets:
            eth0:
                dhcp4: true
                optional: true
        version: 2

After change:

    $ sudo vi /etc/netplan/50-cloud-init.yaml
    # This file is generated from information provided by the datasource.  Changes
    # to it will not persist across an instance reboot.  To disable cloud-init's
    # network configuration capabilities, write a file
    # /etc/cloud/cloud.cfg.d/99-disable-network-config.cfg with the following:
    # network: {config: disabled}
    network:
        version: 2
        ethernets:
            eth0:
                dhcp4: no
                addresses: 
                    - 192.168.1.211/24
                gateway4: 192.168.1.254
                nameservers:
                    addresses: [8.8.8.8, 8.8.4.4]

Apply

    $ sudo netplan apply

References

        https://netplan.io/examples/                    


### nmtui (for earlier ubuntu 20.04)
-------------------------------------

To get `nmtui`

    $ sudo apt-get install network-manager
    Reading package lists... Done
    Building dependency tree
    Reading state information... Done
    The following additional packages will be installed:
    dns-root-data dnsmasq-base libbluetooth3 libidn11 libjansson4 libmbim-glib4
    libmbim-proxy libmm-glib0 libndp0 libnm0 libqmi-glib5 libqmi-proxy
    libteamdctl0 modemmanager network-manager-pptp ppp pptp-linux usb-modeswitch
    usb-modeswitch-data
    Suggested packages:
    avahi-autoipd libteam-utils comgt wvdial
    The following NEW packages will be installed:
    dns-root-data dnsmasq-base libbluetooth3 libidn11 libjansson4 libmbim-glib4
    libmbim-proxy libmm-glib0 libndp0 libnm0 libqmi-glib5 libqmi-proxy
    libteamdctl0 modemmanager network-manager network-manager-pptp ppp
    pptp-linux usb-modeswitch usb-modeswitch-data
    0 upgraded, 20 newly installed, 0 to remove and 0 not upgraded.
    Need to get 4413 kB of archives.
    After this operation, 19.7 MB of additional disk space will be used.
    Do you want to continue? [Y/n] y


Using `nmtui`

    $ sudo nmtui

