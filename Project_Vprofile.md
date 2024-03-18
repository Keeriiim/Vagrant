# VProfile setup [Local]  

- [Project info](#project)
- [VM Setup](#vm-setup)
- [Credits](#credits)
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

## MySQL / MariaDB
**yum update -y**  
**yum install epel-release -y** - The epel-release package provides Extra Packages for Enterprise Linux (EPEL) repository configuration. /etc/yum.repos.d/  
**yum install mariadb-server -y** - installs the server  
**systemctl start mariadb**- starts the service  
**systemctl enable mariadb**- enables it to always be on when ssh  
**mysql_secure_installation** - a script available in MySQL that helps you secure your MySQL installation by performing various security-related operations. These include setting the root password, removing anonymous users, disabling remote root login, and removing test databases.  

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
```sql
// Connect to DB
mysql -u root -proot  
create database accounts;
show databases
```
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/b6c05d5f-efac-47fa-8a3f-f3c529c85e1a)  

```sql
GRANT ALL PRIVILEGES ON accounts.* TO 'admin'@'%' IDENTIFIED BY 'root';
``` - Grants user 'admin' all priveliges for accounts and a password 'admin'  
**FLUSH PRIVILEGES;** - reloads the grant tables in MySQL so that the changes take effect immediately  








