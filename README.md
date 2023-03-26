# test10-Ansible && DockerSwarm
## image
![project-10](https://user-images.githubusercontent.com/111736742/221109082-4f92eeb8-1831-4095-a2bc-1861ddeefbd6.jpg)
## Ansible-Installation
```bash
wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
yum install epel-release-latest-7.noarch.rpm
yum update -y
yum install git python python-devel python-pip openssl ansible -y
ansible --version
```
# SonarQube Download & Installation
```bash
cd /opt
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-8.9.10.61524.zip
unzip sonarqube-8.9.10.61524.zip
mv sonarqube-8.9.10.61524 sonarqube
useradd chaitu
passwd chaitu
chown -R chaitu:chaitu sonarqube
cd /opt/sonarqube/bin/linux-x86-64
vi sonar.sh 
--------------
edit this
#RUN_AS_USER=
RUN_AS_USER=chaitu
su - chaitu
[And start SonarQube]
cd /opt/sonarqube/bin/linux-x86-64
sh sonar.sh start
sh sonar.sh status
ip:9000
```
# Nexus Download & Installation
```bash
yum install java-1.8* -y
cd /opt
wget https://download.sonatype.com/nexus/3/nexus-3.47.1-01-unix.tar.gz
tar -xvzf  nexus-3.47.1-01-unix.tar.gz
mv nexus-3.47.1-01 nexus
useradd chaitu
passwd chaitu
chown -R chaitu:chaitu nexus
chown -R chaitu:chaitu sonatype-work
cd /opt/nexus/bin
vi nexus.rc
--------edit---------
#run_as_user="chaitu"
----------edit--------
sh nexus start
sh nexus status
ip:8081
```
# Ansible-Node Configuration
```bash
cd /etc/ansible
sudo vi hosts
--------------------
#And Place This content
[TomcatServers]
#node-1
172.31.42.33
#node-2
172.31.34.221
----------------------
```
![last2ansible](https://user-images.githubusercontent.com/111736742/221109841-65ed4857-dda3-48eb-b046-760b152d1d90.png)
## To check connectvity between ansible-master & nodes.
![lastping](https://user-images.githubusercontent.com/111736742/221109907-25db0f15-3edf-45dd-ad48-4a4ce369eb94.png)
## copy this [1.context.xml 2.tomcat-users.xml 3.tomcatdeploy.yaml] content into ansible-master home directory.
![lastcopy](https://user-images.githubusercontent.com/111736742/221110044-71a13ad0-a240-4bf8-9d97-cc01c4fccec2.png)
## Docker-swarm configuration
![last1swarm](https://user-images.githubusercontent.com/111736742/221110130-c6408ae3-1ac7-438e-94d1-2ce747b4eb8a.png)
# Jenkins integration with ansible-master Server.
#Goto Manage Jenkins---->Configure System---->SSH Servers
![lastansbileconfiguration](https://user-images.githubusercontent.com/111736742/221119983-bd1fa56e-4a79-4e8e-bdc7-54b3cd3a0043.png)
## Jenkins-Dashboard Before changes
![lastjenkinsdashboard](https://user-images.githubusercontent.com/111736742/221120332-caea9273-f028-423c-9058-2ddcddb31612.png)
#SonarQube
![last sonar-qube](https://user-images.githubusercontent.com/111736742/221120416-f81ef0c3-defc-40ea-8246-bc7270835e50.png)
#Nexus- to storage artifacts
![last-nexus](https://user-images.githubusercontent.com/111736742/221120626-3ef55ee1-2aaf-4b47-bfd8-1e7b1f0790e7.png)
#Docker-Hub Image
![lastdockerhubimage](https://user-images.githubusercontent.com/111736742/221121441-86681632-0712-4578-bb96-da3971906074.png)
#war file copied to anisble master
![lastwarfile](https://user-images.githubusercontent.com/111736742/221121603-fc159d4b-6588-466d-ad95-bde38be0e47a.png)
#Tomcat Output
![lasttomcat](https://user-images.githubusercontent.com/111736742/221121776-c445136b-3576-4846-868d-92b0ca6e5b91.png)
#Docker-swarm-output
![lastdockeroutput](https://user-images.githubusercontent.com/111736742/221121918-392b42c0-5fac-4f1e-b6cc-0ca76b967710.png)
## ----------------------------------------------------
## --------------------------------------------------
## After Changes
#Tomcat Output
![lasteaftertomactchanges](https://user-images.githubusercontent.com/111736742/221122221-0e54c181-f2e3-4b68-9d83-1e2bbfeed118.png)
#Docker-Swarm
![lasterafterchangestomcat](https://user-images.githubusercontent.com/111736742/221122324-24daf277-17cd-4b2d-b6a8-bcda0e223146.png)




