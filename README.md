if any doubt arises please check the video given below :
https://github.com/Subhabrata2468/project1/issues/2#issue-1837289925


THIS IS THE FIRST PROJECT BASED ON DEVOPS PROJECT (BASED ON FREESTYLE PROJECT) WHERE I USE
-> AWS EC2 INSTANCE AS THE CLOUD PROVIDER
-> A WEBPAGE CREATE BY FRIEND (BASED ON "An esports event page where people can see upcoming events and chief guests and can even register for upcoming events")
-> FILES AND FOLDER THAT ARE PRESENT IN GITHUB 
-> THREE EC2 INSTANCES
      -> JENKINS SERVER - HELPS TO AUTOMATE ANSIBLE AND DOCKER SERVER
      -> ANSIBLE SERVER - TO GIVE COMMANDS TO DOCKER PRESENT IN DOCKER SERVER, HOW TO MAINTAIN THE DOCKER CONTAINER
      -> DOCKER SERVER  - FOR CONTAINER MANAGEMENT
      -> 

-> REQUIRMENTS :
 ----------------------------------------------------------------------------------------------------------------------------------------
 | JENKINS SERVER                              |  ANSIBLE SERVER                             |   DOCKER SERVER                          |
 |--------------------------------------------------------------------------------------------------------------------------------------|
 | 1.SET NAME                                  | 1.SETNAME                                   | 1.SETNAME                                |
 |--------------------------------------------------------------------------------------------------------------------------------------|
 | 1.INSTALL JAVA 11 (ONLY)                    | 2.INSTALL DOCKER                            | 2.INSTALL DOCKER                         |
 |--------------------------------------------------------------------------------------------------------------------------------------|
 | 2.INSTALL GIT                               | 3.DOCKER LOGIN                              |  3.DOCKER LOGIN                          |
 |--------------------------------------------------------------------------------------------------------------------------------------|
 | 3.INSTALL JENKINS                           | 4.INSTALL ANSIBLE                           |                                          |
 |--------------------------------------------------------------------------------------------------------------------------------------|
 | 4 ssh-keygen(connection between             | 5. ssh-keygen(connextion between            |                                          |
 |           jenkins to ansible server)        |         ansible to docker server)           |                                          |
 |--------------------------------------------------------------------------------------------------------------------------------------|
 ----------------------------------------------------------------------------------------------------------------------------------------

-> SETTING UP THE SERVER TO HOST THE PAGE PROPERLY :
      Jenkins (amazon linux 2 )

1.	[ec2-user@ip-172-31-39-46 ~]$ sudo hostnamectl set-hostname Jenkins
2.	[ec2-user@ip-172-31-39-46 ~]$ exit
3.	[ec2-user@jenkins ~]$ sudo yum update -y
4.	[ec2-user@jenkins ~]$ sudo yum install git -y
5.	[ec2-user@jenkins ~]$ sudo yum install -y java-11 -y
6.	[ec2-user@jenkins ~]$ sudo java -version
      openjdk version "11.0.20" 2023-07-18 LTS
      OpenJDK Runtime Environment Corretto-11.0.20.8.1 (build 11.0.20+8-LTS)
      OpenJDK 64-Bit Server VM Corretto-11.0.20.8.1 (build 11.0.20+8-LTS, mixed mode)
7.	[ec2-user@jenkins ~]$ sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo  
8.	[ec2-user@jenkins ~]$ sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
9.	[ec2-user@jenkins ~]$ sudo yum install jenkins -y
10.	[ec2-user@jenkins ~]$ sudo systemctl start Jenkins
11.	[ec2-user@jenkins ~]$ sudo systemctl enable Jenkins
12.	[ec2-user@jenkins ~]$ sudo systemctl status Jenkins
      AFTER THAT GO TO ANY BROWSER COPY THE PUBLIC IP ADDRESS OF THE EC2 JENKINS INSTANCE  “<PUBLIC IP >:8080”
13.	[ec2-user@jenkins ~]$ sudo cat /var/lib/jenkins/secrets/initialAdminPassword
14.	[ec2-user@jenkins ~]$ sudo su
15.	[root@jenkins ec2-user]# passwd root
      Changing password for user root.
      New password:
      BAD PASSWORD: The password is shorter than 8 characters
      Retype new password:
      passwd: all authentication tokens updated successfully.
      (JUMP 1) AfTER THAT GO TO ANSIBLE SERVER DO THE STTING . FIRST GO TO ANSIBLE SERVER TO DO “PERMIT ROOT LOGIN” AND “PASSWORD AUTHENTICATION “
      [go to ansible server from step 1 to 14 ]
16.	[root@ jenkins ec2-user]# vim /etc/ssh/sshd_config
      PermitRootLogin yes
      PasswordAuthentication yes
17.	[root@ jenkins ec2-user]# service sshd restart
      Redirecting to /bin/systemctl restart sshd.service
18.	[root@jenkins ec2-user]# ssh-keygen
      Generating public/private rsa key pair.
      Enter file in which to save the key (/root/.ssh/id_rsa):
      Enter passphrase (empty for no passphrase):
      Enter same passphrase again:
      Your identification has been saved in /root/.ssh/id_rsa.
      Your public key has been saved in /root/.ssh/id_rsa.pub.
      The key fingerprint is:
      SHA256:VV9kaKWlbScEJsYhKM83EcL0WD2/dxFLcrGB4LT4n5o root@jenkins
      The key's randomart image is:
      +---[RSA 2048]----+
      |     oo.++++=.o*B|
      |    . o=.oB+.=o@o|
      |     +. .o.= .O.*|
      |      o o.. .  =.|
      |       .S. . .  .|
      |            o o .|
      |             + . |
      |            o    |
      |           E     |
      +----[SHA256]-----+
19.	[root@jenkins ec2-user]# ssh-copy-id -i root@<private ip of ansible server>
      /bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/root/.ssh/id_rsa.pub"
      The authenticity of host '172.31.33.252 (172.31.33.252)' can't be established.
      ECDSA key fingerprint is SHA256:pnVuWaIK8ig6c+iVIpuMKuxI66FlZ704MebwOVqonVY.
      ECDSA key fingerprint is MD5:21:2c:4c:fc:08:b8:31:fb:84:09:72:42:5e:45:8b:d2.
      Are you sure you want to continue connecting (yes/no)? yes
      /bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
      /bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
      <private ip of ansible server>s password:

      Number of key(s) added: 1

      Now try logging into the machine, with:   "ssh 'root<private ip of ansible server>'"
      and check to make sure that only the key(s) you wanted were added.
20.	[root@jenkins ec2-user]# ping <private ip of ansible server>
      PING <private ip of ansible server> (<private ip of ansible server>) 56(84) bytes of data.
      64 bytes from <private ip of ansible server>: icmp_seq=1 ttl=255 time=0.998 ms
      64 bytes from <private ip of ansible server>: icmp_seq=2 ttl=255 time=0.509 ms
      64 bytes from <private ip of ansible server>: icmp_seq=3 ttl=255 time=0.558 ms
      ^Z
      [1]+  Stopped                 ping <private ip of ansible server>
      (JUMP 2) ALL THE WORK OF JENKINS SERVER IS DONE , NOW GO TO DOCKER SERVER
      [go to docker server start from step 1 to 21]
21.	End





Ansible (amazon Linux 2 )


1.	[ec2-user@ip-172-31-33-252 ~]$ sudo hostnamectl set-hostname ansible
2.	[ec2-user@ip-172-31-33-252 ~]$ exit
3.	[ec2-user@ansible ~]$ sudo yum update -y
4.	[ec2-user@ansible ~]$ sudo yum install docker -y
5.	[ec2-user@ansible ~]$ sudo systemctl start docker
6.	[ec2-user@ansible ~]$ sudo systemctl status docker
7.	[ec2-user@ansible ~]$ sudo docker login
      Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
      Username: subhabrata3002
      Password:
      WARNING! Your password will be stored unencrypted in /root/.docker/config.json.
      Configure a credential helper to remove this warning. See
      https://docs.docker.com/engine/reference/commandline/login/#credentials-store

      Login Succeeded
8.	[ec2-user@ansible ~]$ sudo yum install epel-release -y
9.	[ec2-user@ansible ~]$ sudo yum install ansible -y
10.	[ec2-user@ansible ~]$ sudo ansible –version
      ansible 2.9.27
        config file = /etc/ansible/ansible.cfg
        configured module search path = [u'/root/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
        ansible python module location = /usr/lib/python2.7/site-packages/ansible
        executable location = /bin/ansible
        python version = 2.7.18 (default, Feb 28 2023, 02:51:06) [GCC 7.3.1 20180712 (Red Hat 7.3.1-15)]
11.	[ec2-user@ansible ~]$ sudo su
12.	[root@ansible ec2-user]# passwd root
      Changing password for user root.
      New password:
      BAD PASSWORD: The password is shorter than 8 characters
      Retype new password:
      passwd: all authentication tokens updated successfully.
13.	[root@ansible ec2-user]# vim /etc/ssh/sshd_config
      PermitRootLogin yes
      PasswordAuthentication yes
14.	[root@ansible ec2-user]# service sshd restart
      Redirecting to /bin/systemctl restart sshd.service
      (JUMP3) NOW AGAIN GO TO JENKINS SERVER TO DO SSH CONNECTION FROM JENKINS TO ANSIBLE SERVER
      [go to jenkins server start from step 15 to 20]
15.	[ec2-user@ansible ~]$ sudo ssh-keygen
      Generating public/private rsa key pair.
      Enter file in which to save the key (/root/.ssh/id_rsa):
      Enter passphrase (empty for no passphrase):
      Enter same passphrase again:
      Your identification has been saved in /root/.ssh/id_rsa.
      Your public key has been saved in /root/.ssh/id_rsa.pub.
      The key fingerprint is:
      SHA256:lPLyt5b+W9eJ3gA9Xigren+kiLUz5pYSg5eNX35BiZs root@ansible
      The key's randomart image is:
      +---[RSA 2048]----+
      |                 |
      |         .       |
      |      . o   . .  |
      |       +   ..o.  |
      |      o S  o++ . |
      |     . O o E=o+ o|
      |      . B.Boo+o.o|
      |       o.%++.+o. |
      |       .*+*o=o . |
      +----[SHA256]-----+
16.	[ec2-user@ansible ~]$ sudo ssh-copy-id -i root@<private ip of docker server>
      /bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/root/.ssh/id_rsa.pub"
      The authenticity of host '<private ip of docker server> (<private ip of docker server>)' can't be established.
      ECDSA key fingerprint is SHA256:rKhO0RKTd/g3t+YA3MSwUAPS2tNuI98Lqn9VJzhn31s.
      ECDSA key fingerprint is MD5:4b:4f:53:e4:7f:a2:f0:27:89:09:cd:0e:7b:61:53:b3.
      Are you sure you want to continue connecting (yes/no)? yes
      /bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
      /bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
      root@<private ip of docker server>'s password:

      Number of key(s) added: 1

      Now try logging into the machine, with:   "ssh 'root@<private ip of docker server>'"
      and check to make sure that only the key(s) you wanted were added.

17.	[ec2-user@ansible ~]$ ping <private ip of docker server>
      PING <private ip of docker server> (<private ip of docker server>) 56(84) bytes of data.
      64 bytes from <private ip of docker server>: icmp_seq=1 ttl=64 time=0.449 ms
      64 bytes from <private ip of docker server>: icmp_seq=2 ttl=64 time=0.607 ms
      64 bytes from <private ip of docker server>: icmp_seq=3 ttl=64 time=0.562 ms
      64 bytes from <private ip of docker server>: icmp_seq=5 ttl=64 time=0.527 ms
      ^Z
      [1]+  Stopped                 ping <private ip of docker server>
18.	[ec2-user@ansible ~]$ sudo vim /etc/ansible/hosts
      [slave]
      <private ip of docker server>
19.	[ec2-user@ansible ~]$ sudo vim /etc/ansible/ansible.cfg
      inventory      = /etc/ansible/hosts
      sudo_user      = root
20.	[ec2-user@ansible ~]$ mkdir ansible
21.	[ec2-user@ansible ~]$ mkdir docker
      ALL THE WORK IS DONE ON ANSIBLE SERVER
22.	end



Docker (amazon red hat )

1.	[ec2-user@ip-172-31-37-224 ~]$ sudo hostnamectl set-hostname docker
2.	[ec2-user@ip-172-31-37-224 ~]$ exit
3.	[ec2-user@docker ~]$ sudo yum update -y
4.	[ec2-user@docker ~]$ sudo yum remove docker docker-client docker-client-latest docker-common docker-latest docker-latest-logrotate docker-logrotate             docker-engine
5.	[ec2-user@docker ~]$ sudo yum install epel-release
6.	[ec2-user@docker ~]$ sudo yum install -y yum-utils device-mapper-persistent-data lvm2
7.	[ec2-user@docker ~]$ sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
8.	[ec2-user@docker ~]$ sudo yum install docker-ce -y
9.	[ec2-user@docker ~]$ sudo systemctl start docker
10.	[ec2-user@docker ~]$ sudo systemctl enable docker
      Created symlink /etc/systemd/system/multi-user.target.wants/docker.service → /usr/lib/systemd/system/docker.service.
11.	[ec2-user@docker ~]$ sudo systemctl status docker
12.	[ec2-user@docker ~]$ docker --version
      Docker version 24.0.5, build ced0996
23.	[ec2-user@docker~]$ sudo docker login
      Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
      Username: subhabrata3002
      Password:
      WARNING! Your password will be stored unencrypted in /root/.docker/config.json.
      Configure a credential helper to remove this warning. See
      https://docs.docker.com/engine/reference/commandline/login/#credentials-store

      Login Succeeded
13.	[ec2-user@docker ~]$ sudo yum install python3
14.	[ec2-user@docker ~]$ sudo pip3 install docker -y
15.	[ec2-user@docker ~]$ python --version
      Python 3.9.16
16.	[ec2-user@docker ~]$ sudo pip3 install docker
17.	[ec2-user@docker ~]$ sudo pip3 install 'urllib3<2.0'
18.	[ec2-user@ docker ~]$ sudo su
19.	[root@ docker ec2-user]# passwd root
      Changing password for user root.
      New password:
      BAD PASSWORD: The password is shorter than 8 characters
      Retype new password:
      passwd: all authentication tokens updated successfully.
20.	[root@ docker ec2-user]# vi /etc/ssh/sshd_config
      PermitRootLogin yes
      PasswordAuthentication yes
21.	[root@ docker ec2-user]# service sshd restart
      Redirecting to /bin/systemctl restart sshd.service
      (JUMP4) NOW GO TO ANSIBLE SERVER AND DO SSH CONNECTION FROM ANSIBLE TO DOCKER SERVER
      [go to ansible server ans=d start from step 15 to 21]
      ALL THE WORK IS DONE IN DOCKER SERVER
22.	END 

