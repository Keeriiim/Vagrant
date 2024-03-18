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


# VM Setup

