Howtodo - CentOS7 - Install RabbitMQ
====================================

#### Downlaod and Install Erlang
----

    # sudo yum install https://github.com/rabbitmq/erlang-rpm/releases/download/v20.2.3/erlang-20.2.3-1.el7.centos.x86_64.rpm

[Zero-dependency Erlang RPM for RabbitMQ](https://github.com/rabbitmq/erlang-rpm/releases)



#### Download and Install RabbitMQ Server
----

    # sudo yum install https://dl.bintray.com/rabbitmq/all/rabbitmq-server/3.7.3/rabbitmq-server-3.7.3-1.el7.noarch.rpm
    
    Auto start daemon
    # sudo chkconfig rabbitmq-server on

    Check status
    # sudo rabbitmqctl status


#### Open firewall ports 
----

    # sudo firewall-cmd --zone=public --add-port=4369/tcp --permanent
    # sudo firewall-cmd --zone=public --add-port=5671/tcp --permanent
    # sudo firewall-cmd --zone=public --add-port=5672/tcp --permanent
    # sudo firewall-cmd --zone=public --add-port=15672/tcp --permanent
    # sudo firewall-cmd --zone=public --add-port=25672/tcp --permanent
    # sudo systemctl restart firewalld
    # sudo firewall-cmd --list-ports
      4369/tcp 5671/tcp 5672/tcp 15672/tcp 25672/tcp





#### Source
----

[Source](https://www.rabbitmq.com/install-rpm.html)


