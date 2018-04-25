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
  

#### Source
----
[Connecting to Instances](https://cloud.google.com/compute/docs/instances/connecting-to-instance)
[Creating a new SSH key](https://cloud.google.com/compute/docs/instances/adding-removing-ssh-keys#createsshkeys)

