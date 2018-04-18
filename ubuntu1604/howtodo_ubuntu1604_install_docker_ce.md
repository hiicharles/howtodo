Howtodo - Ubuntu 16.04 - Install Docker CE
==========================================


#### Install Pre-requisites

	# sudo apt-get update
	# sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
	

#### Add key and repository

	# curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
	# sudo apt-key fingerprint 0EBFCD88
	# sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs)  stable"


#### Install Docker CE
----

	# sudo apt-get update
	# sudo apt-get install docker-ce


#### Verify installation
----

    # docker run hello-world
	
	Unable to find image 'hello-world:latest' locally
	latest: Pulling from library/hello-world
	9bb5a5d4561a: Pull complete 
	Digest: sha256:f5233545e43561214ca4891fd1157e1c3c563316ed8e237750d59bde73361e77
	Status: Downloaded newer image for hello-world:latest
	
	Hello from Docker!
	This message shows that your installation appears to be working correctly.
	
	To generate this message, Docker took the following steps:
	 1. The Docker client contacted the Docker daemon.
	 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
	    (amd64)
	 3. The Docker daemon created a new container from that image which runs the
	    executable that produces the output you are currently reading.
	 4. The Docker daemon streamed that output to the Docker client, which sent it
	    to your terminal.
	
	To try something more ambitious, you can run an Ubuntu container with:
	 $ docker run -it ubuntu bash
	
	Share images, automate workflows, and more with a free Docker ID:
	 https://hub.docker.com/
	
	For more examples and ideas, visit:
	 https://docs.docker.com/engine/userguide/

  


#### Source
----
[Get Docker CE for Ubuntu](https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-docker-ce)


