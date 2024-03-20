# VProfile setup [Local]  

- [Project info](#project)
- [VM Setup](#vm-setup)
- [License](#license)


# Project  
The aim for this project is to create a multi tier web application stack on my local machine (windows 10). A stack is a collection of services working together to create and experience(in this case a WebApp).
This project will make a baseline for more upcoming projects involing deployment to a cloud providers, refactoring, containeraze applications & deploy on clusters etc.
The benefit of this project will also be that it will create a local lab environment for me to practice and make any change i want before pushing it to real servers.
The process will be automated, repeatable (the infrastructure will be codebased)

## User experience
The User will enter the ip adress in a webbrowser to access our app running on tomcat. The the user queries for log in the app will run a SQL query to access the user information stored in the database.
If the login is the first time it will go to the database, if not the request will go to mem chache service.  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/a7164e83-acf0-4b26-ada6-e6040d15668f)  

## Workflow
1. Have all tools installed on local computer.
2. Clone Source Code
3. cd into vagrant dir & start a VM for every service
4. Validate all VMs and the interaction with eachother
5. Setup all services
6. Build and deploy App


## Tools
* **Hypervisor** - Oracle VM Virtual Box
* **Automation** - Vagrant
* **CLI** - Git Bash
* **IDE** - Vs code

## Architecture of automated setup
* Vagrant
* VirtualBox
* Git Bash

## Architecture of project services
* Nginx - Will be used for loadbalancing. All requests will be routed to the tomcat server
* Tomcat - Webservice that will host the application
* RabbitMQ - MessageBroker / Queuing agent to connect two applications together, data can be streamed from this
* MemCached - Caching service that will be connected to MySQL server.
* MySql - Database for storing information

![image](https://github.com/Keeriiim/Vagrant/assets/117115289/9d9f7a08-ed81-4fc5-a71c-c4f6aca4f660)  


## Provisioning  
Setup of the stack should be done in this order to avoid problems, stopping should be done from bottom to top. A stack means combination of multiple services. 
A cluster is group of systems running the same service.  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/e81e0eac-75da-4e21-b997-2b2f060ffea3)  



# VM Setup 
## Prerequisites
1. Oracle VM VirtualBox
2. Git Bash & Vagrant
3. Vagrant plugin hostmanager

## Hostmanager  
Hostmanager is a vagrant plugin that takes the hostname & ip set in the vagrantfile and adds them to /etc/hosts. 
This makes it easy for the user to use the hostname instead of ip when calling a machine.  
**vagrant plugin install vagrant-hostmanager** - Installs the plugin on your local computer  
**vagrant plugin list** - Lists all installed plugins  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/e95e7485-0dca-42ed-b13e-8a41abdc46b2)  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/602065fa-c7ae-4262-ba29-6c0c047fcfe2)  

You can always change the name or ip adress in /etc/hosts file from root.
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/40ed28c0-50c4-48db-a757-58de041479bd)  

## 1. MySQL / MariaDB
* Connect to the first vm -> db01  
  **vagrant ssh db01**  

```bash
yum update -y  
yum install epel-release -y (The epel-release package provides Extra Packages for Enterprise Linux (EPEL) repository configuration. /etc/yum.repos.d/)
yum install mariadb-server -y  (installs the server)  
systemctl start mariadb (starts the service)  
systemctl enable mariadb (enables it to always be on when ssh)  
mysql_secure_installation (a script available in MySQL that helps you secure your MySQL installation by performing various security-related operations. These include setting the root password, removing anonymous users, disabling remote root login, and removing test databases.)
```  

```
For the script:
Y
Y
root
root
Y
Y
Y
Y
```

** Connect to the DB **  
**mysql -u root -proot**  
```sql  
create database accounts;
show databases;
```
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/b6c05d5f-efac-47fa-8a3f-f3c529c85e1a)  

**Create an admin user for other Vms to access the DB.**  
```sql
//Grants user 'admin' all priveliges for accounts and a password 'admin' 
GRANT ALL PRIVILEGES ON accounts.* TO 'admin'@'%' IDENTIFIED BY 'root';

//reloads the grant tables in MySQL so that the changes take effect immediately
FLUSH PRIVILEGES;
exit;
```
**Clone the repo and extract the db to the right table**
```bash
git clone -b main https://github.com/hkhcoder/vprofile-project.git
cd vprofile-project
mysql -u root -proot accounts < src/main/resources/db_backup.sql
```
**Access the table to see the result**
```sql
mysql -u root -proot accounts;
show tables;
exit;
```
<img width="269" alt="image" src="https://github.com/Keeriiim/Vagrant/assets/117115289/9c636354-2508-463d-8bc9-5939eeed908d">  

**systemctl restart mariadb**

## 2. Memcached  
Memcached is an open-source, high-performance, distributed memory caching system. It caches data and objects in RAM to speed up dynamic web applications. Data is stored in key-value pairs and retrieved quickly without the need for repeated database queries. Memcached improves application performance by reducing response times and alleviating the load on backend data sources.  

* Connect to the 2nd vm > mc01
  **vagrant ssh mc01**

Installing packet manager, memcached and changeing the listening port from itself to all ips (0.0.0.0)
```bash
dnf install epel-release -y
dnf install memcached -y
systemctl start memcached
systemctl enable memcached
systemctl status memcached
sed -i 's/127.0.0.0/0.0.0.0/g' /etc/sysconfig/memcached
systemctl status memcached
```
<img width="748" alt="image" src="https://github.com/Keeriiim/Vagrant/assets/117115289/a66b2294-fe6d-4600-9c11-b383015f4257">  

## 3. RabbitMQ  
RabbitMQ is used to facilitate communication between different components of an application or between different applications/systems. It enables asynchronous messaging, meaning that sender and receiver do not have to interact with each other at the same time. Instead, messages can be sent and stored until the recipient is ready to process them. This decoupling of components makes systems more flexible, scalable, and reliable.  *
For security reasons, loopback connection will be dissallowed, meaning you can only connect/use the service from other hosts.

* Connect to the 3rd vm > rmq01
 **vagrant ssh rmq01**

```bash
dnf update -y
dnf install epel-release -y
dnf install centos-release-rabbitmq-38 -y   // repository configuration package that enables the RabbitMQ repository for your system
dnf --enablerepo=centos-rabbitmq-38 -y install rabbitmq-server   // DNF will now look into the centos-rabbitmq-38 repository and install the rabbitmq-server package along with any of its dependencies
systemctl start rabbtimq-server
systemctl enable rabbtimq-server
systemctl status rabbtimq-server
sh -c 'echo "[{rabbit, [{loopback_users, []}]}]." > /etc/rabbitmq/rabbitmq.config'   // Creates a config file to dissallow loopback (127.0.0.1) connection 
rabbitmqctl add_user test test    // Creates a user called test, 
rabbitmqctl set_user_tags test administrator   // Makes the test user an administrator
systemctl status memcached
```

## 3. Tomcat  
Definition: Apache Tomcat is an open-source web server and servlet container developed by the Apache Software Foundation.
Usage: It is primarily used to deploy Java Servlets and JavaServer Pages (JSP), making it a popular choice for hosting Java web applications.

* Connect to the 3rd vm > app01
 **vagrant ssh app01**
  
```bash
dnf update -y
dnf install epel-release -y
dnf install java-11-openjdk java-11-openjdk-devel
dnf install wget git maven -y

cd /temp/
wget https://archive.apache.org/dist/tomcat/tomcat-9/v9.0.75/bin/apache-tomcat-9.0.75.tar.gz // download tomcat
tar xzvf apache-tomcat-9.0.75.tar.gz   // extracts gzip, displays all files in current directory

useradd --home-dir /usr/local/tomcat --shell /sbin/nologin tomcat   //Adds a user 'tomcat' that doesnt require password
cp -r apache-tomcat-9.0.75/* /usr/local/tomcat   // Cp's all files to a new directory
ls -ls /usr/local/tomcat/   // Lists who owns all files
ls -ld /usr/local/tomcat/   // Lists who owns the directory
```  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/e3fdb062-3b06-4bce-9865-af78f21f94cb)  

```bash
chown -R tomcat.tomcat /usr/local/tomcat   // Changes ownershop of all files to user.group, The -R option ensures that the ownership change is applied recursively to all files and subdirectories within /usr/local/tomcat.
ls -ls /usr/local/tomcat/   // Lists who owns all files
```  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/2d1f30ec-48ae-4e4e-a3f5-79b6a3b717d1)  

## Setup systemctl command for tomcat

```bash
vi /etc/systemd/system/tomcat.service -> add the text below

[Unit]
Description=Tomcat
After=network.target
[Service]
User=tomcat
WorkingDirectory=/usr/local/tomcat
Environment=JRE_HOME=/usr/lib/jvm/jre
Environment=JAVA_HOME=/usr/lib/jvm/jre
Environment=CATALINA_HOME=/usr/local/tomcat
Environment=CATALINE_BASE=/usr/local/tomcat
ExecStart=/usr/local/tomcat/bin/catalina.sh run
ExecStop=/usr/local/tomcat/bin/shutdown.sh
SyslogIdentifier=tomcat-%i


systemctl daemon-reload   // Always run this after making a change in /etc/systemd/system
systemctl start tomcat
systemctl enable tomcat
```  

If we didn't run the bash script the configuration would be stored in /etc, and logs in /var/logs. Now we have it like this.
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/bd23e7d1-6938-47a1-b6d6-cb5a629d2c2c)  
















