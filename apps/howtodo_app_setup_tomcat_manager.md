Howtodo - Application - Setup Tomcat Manager
============================================

#### Setup Tomcat
----

    [Change to root]
    $ sudo su

    [Create directory]
    # mkdir -p /opt/servers
    
    [Download]
    # cd /opt/servers
    # wget http://www-eu.apache.org/dist/tomcat/tomcat-9/v9.0.8/bin/apache-tomcat-9.0.8.tar.gz

    [Extract]
    # tar -zxvf apache-tomcat-9.0.8.tar.gz 


#### Add Tomcat Users
----

	[Go to conf]
    # cd /opt/servers/apache-tomcat-9.0.8/conf
    
    [Add users]
    # vi tomcat-users.xml

        <user username="tomcat" password="password" roles="manager-gui,manager-script" />


    In tomcat-9.0.8/webapps/manager/WEB-INF/web.xml, it defined following roles

        manager-gui — Access to the HTML interface.
        manager-status — Access to the "Server Status" page only.
        manager-script — Access to the tools-friendly plain text interface that is described in this document, and to the "Server Status" page.
        manager-jmx — Access to JMX proxy interface and to the "Server Status" page.


#### Allow Any IP to access Tomcat Manager
----

	[Go to conf/Catalina/localhost]
    # cd /opt/servers/apache-tomcat-9.0.8/conf/Catalina/localhost
    
    [IP specific]
    # vi manager.xml

        <Context privileged="true" antiResourceLocking="false" docBase="$ {catalina.home}/webapps/manager">
            <Valve className="org.apache.catalina.valves.RemoteAddrValve" allow="127\.0\.0\.1" />
        </Context>

    [Any IP]

        <Context privileged="true" antiResourceLocking="false" docBase="$ {catalina.home}/webapps/manager">
            <Valve className="org.apache.catalina.valves.RemoteAddrValve" allow="^.*$" />
        </Context>


    [Note]
    You need to start tomcat up once to have the conf/Catalina/localhost folder available.


#### Access to tomcat manager

    [Startup tomcat]
    # cd /opt/servers/apache-tomcat-9.0.8/bin
    # ./startup.sh


#### Source
----
[Introduction](https://tomcat.apache.org/tomcat-9.0-doc/manager-howto.html#Configuring_Manager_Application_Access) | [Configuring Manager Application Acces](https://tomcat.apache.org/tomcat-9.0-doc/manager-howto.html#Configuring_Manager_Application_Access) | 
[Access Tomcat Manager App from different host](https://stackoverflow.com/questions/36703856/access-tomcat-manager-app-from-different-host?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa)
