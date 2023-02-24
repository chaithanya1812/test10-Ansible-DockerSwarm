# test10-Ansible-DockerSwarm
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
