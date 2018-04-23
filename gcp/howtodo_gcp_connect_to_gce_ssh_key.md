Howtodo - GCP - Connect to GCE - SSH Keys
=========================================


#### Connect to Compute Engine using built-in SSH
----

	Product & Services > Compute Engine > VM instances
	Click on SSH on the instance to access.
	Built-in terminal will open.
	

#### Connect to Compute Engine using third-party SSH
----

Creating a new SSH key

	$ ssh-keygen -t rsa -f /home/user/.ssh/user -C user

		Generating public/private rsa key pair.
		Enter passphrase (empty for no passphrase): 
		Enter same passphrase again: 
		Your identification has been saved in /home/user/.ssh/user.
		Your public key has been saved in /home/user/.ssh/user.pub.
		The key fingerprint is:
		SHA256:Sj0hgau4SJzypY//sJ2kjXHAlpppZ8+wRlKqVxV9nHE user
		The key's randomart image is:
		+---[RSA 2048]----+
		|     ... ..oE    |
		|    . ... +.     |
		|     .....       |
		|   .o..o .       |
		|...+=.. S        |
		|o++=+o . .       |
		|++=** +          |
		|+.++./ .         |
		| ..+B.B          |
		+----[SHA256]-----+


	
	$ ls -ltr /home/user/.ssh/

		-rw-r--r-- 1 user user  396 Apr 23 04:08 user.pub	# public key
		-rw------- 1 user user 1675 Apr 23 04:08 user		# private key

	$ chmod 400 /home/user/.ssh/user
	$ cat /home/user/.ssh/user.pub

		ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC8pdt163DZVZ+GMp9MTe373DARwTMUHRAMO7+wirFwGtdpyIXwAcpFgPo07KUzZLqHzWLvy3y5j1wMR67f7BRM+Y5C66VvyOsXyq3fDEmXRnB9NoUsfUrLYNkZPNuzbJzErcrvaz4D6k/pwpWrnXoVE8e4FMnEabVuUok2Cro5394AGVfs/I1BS+1uNKwnaflcTLnOpEL2rCaVgoUNK1PgO5lFJYUEoyenXcktYZ9chvIhfGnioFbj8IM2773I6lkbNOY9oQJxWYWGAnSx3E70OGzffnenlv1KJCPiJgyd8ZCU3WLltoeRklDtH1xymSoK0oOkjexBRYeWy6uYQOln user


Import public SSH key to Compute Engine using Metadata
	
	Product & Services > Compute Engine > Metadata > SSH Keys
	Click Edit
	Paste the SSH keys

		ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC8pdt163DZVZ+GMp9MTe373DARwTMUHRAMO7+wirFwGtdpyIXwAcpFgPo07KUzZLqHzWLvy3y5j1wMR67f7BRM+Y5C66VvyOsXyq3fDEmXRnB9NoUsfUrLYNkZPNuzbJzErcrvaz4D6k/pwpWrnXoVE8e4FMnEabVuUok2Cro5394AGVfs/I1BS+1uNKwnaflcTLnOpEL2rCaVgoUNK1PgO5lFJYUEoyenXcktYZ9chvIhfGnioFbj8IM2773I6lkbNOY9oQJxWYWGAnSx3E70OGzffnenlv1KJCPiJgyd8ZCU3WLltoeRklDtH1xymSoK0oOkjexBRYeWy6uYQOln user

	Save

	$ ssh user@35.187.X.X

		The authenticity of host '35.187.244.119 (35.187.X.X)' can't be established.
		ECDSA key fingerprint is SHA256:vaNb71ZbUj8d0tGxKJQcdr80deKBzfPUNAvtFH8de6k.
		Are you sure you want to continue connecting (yes/no)? yes
		Warning: Permanently added '35.187.244.119' (ECDSA) to the list of known hosts.



#### Connect to Compute Engine using Google Cloud SDK (Serial)
----

	- Setup Google Cloud SDK
	$ gcloud compute instances list
	NAME        ZONE               MACHINE_TYPE               PREEMPTIBLE  INTERNAL_IP  EXTERNAL_IP     STATUS
	instance01  asia-southeast1-a  custom (2 vCPU, 8.00 GiB)               10.148.0.2   35.187.x.x  	RUNNING

	$ gcloud compute instances add-metadata instance01 --metadata=serial-port-enable=1
	Updated [https://www.googleapis.com/compute/v1/projects/my-project/zones/asia-southeast1-a/instances/bo-pgedb01].

	$ gcloud compute connect-to-serial-port instance01 --port=2

		WARNING: The public SSH key file for gcloud does not exist.
		WARNING: The private SSH key file for gcloud does not exist.
		WARNING: You do not have an SSH key for gcloud.
		WARNING: SSH keygen will be executed to generate a key.
		This tool needs to create the directory [/home/user/.ssh] before 
		being able to generate SSH keys.
		
		Do you want to continue (Y/n)?  Y
		
		Generating public/private rsa key pair.
		Enter passphrase (empty for no passphrase): 
		Enter same passphrase again: 
		Your identification has been saved in /home/user/.ssh/google_compute_engine.
		Your public key has been saved in /home/user/.ssh/google_compute_engine.pub.
		The key fingerprint is:
		SHA256:mho9f2QZ4XPcMN1SY3uyTMKb78fJ2p4gujZVlAIhOxg user@ubuntu
		The key's randomart image is:
		+---[RSA 2048]----+
		|     E . oo  ..=.|
		|      o o .ooo+ +|
		|     . o . o=+oo.|
		|        . + oB.o.|
		|        S  =+ o  |
		|     . o  +. .   |
		|    . =  o.. .o..|
		|     o o oo ..oo+|
		|    .   o+o  .+= |
		+----[SHA256]-----+
		Updating project ssh metadata.../Updated [https://www.googleapis.com/compute/v1/projects/my-project].                                                                                                                                  
		Updating project ssh metadata...done.                                                                                                                                                                                                        
		serialport: Connected to my-project.asia-southeast1-a.bo-pgedb01 port 2 (session ID: 2d1634b68b656b857f4a24aadf9f8d24370287944a68d88fef9e39aaf18bfe9f, active connections: 1).







#### Connect to Compute Engine using Remote Desktop (for Windows)
----

	$ gcloud compute instances list
	NAME        ZONE               MACHINE_TYPE               PREEMPTIBLE  INTERNAL_IP  EXTERNAL_IP     STATUS
	instance01  asia-southeast1-a  custom (2 vCPU, 8.00 GiB)               10.148.0.2   35.187.x.x  	RUNNING

	Use the EXTERNAL_IP with port 3389
	
	Note:
	Only for Windows instance




#### Verify installation
----

    # python3.6 -V
    Python 3.6.3
  


#### Source
----
[Connecting to Instances](https://cloud.google.com/compute/docs/instances/connecting-to-instance)

Creating a new SSH key
[Creating a new SSH key](https://cloud.google.com/compute/docs/instances/adding-removing-ssh-keys#createsshkeys)

