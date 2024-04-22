- [Intro](#intro)
- [Classic LB](#classic-load-balancer)
- [Application LB](#application-load-balancer)
- [Network LB](#intro)
- [Project 3](#project-3)



# Intro
AWS ELB (Elastic Load Balancing) is a service that automatically distributes incoming application traffic across multiple targets, such as Amazon EC2 instances, containers, and IP addresses, in multiple Availability Zones.  
ELB offers three types of load balancers: Classic Load Balancer (CLB), Application Load Balancer (ALB), and Network Load Balancer (NLB).
[READ](#https://docs.aws.amazon.com/elasticloadbalancing/)

## Classic Load Balancer
- Routes incoming traffic to backend servers
- Works at the network layer in OSI model
- Ideal for balancing traffic across multiple Ec2 instances
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/eb5724ec-13aa-4c07-b124-9e8cdb29c91c)

## Application Load Balancer
- Routes webtraffic: websites, apps (only http & https protocol) - basically API routing to different Ec2s: ... /videos ... /registration etc
- Application layer (7) OSI model
- Ideal for balancing traffic across multiple Ec2 instances
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/8293d1f9-f335-4461-9d19-f18c64e5594e)




## Network Load Balancer
- Routes webtraffic: websites, apps (only http & https protocol) - basically API routing to different Ec2s: ... /videos ... /registration etc
- Transport layer (4) OSI model
- Ideal for handling a huge demand on requests, can handle millions of requests per sec
- Classic & network have dynamic ip, with elastic ip you can make it static

## Gateway Load Balancer
-
- Operates at the network layer (layer 3)

# Project 3

## Creating instance
- Create an instance and paste this bash script
```bash
#!/bin/bash

# Variable Declaration
#PACKAGE="httpd wget unzip"
#SVC="httpd"
URL='https://www.tooplate.com/zip-templates/2098_health.zip'
ART_NAME='2098_health'
TEMPDIR="/tmp/webfiles"

yum --help &> /dev/null

if [ $? -eq 0 ]
then
   # Set Variables for CentOS
   PACKAGE="httpd wget unzip"
   SVC="httpd"

   echo "Running Setup on CentOS"
   # Installing Dependencies
   echo "########################################"
   echo "Installing packages."
   echo "########################################"
   sudo yum install $PACKAGE -y > /dev/null
   echo

   # Start & Enable Service
   echo "########################################"
   echo "Start & Enable HTTPD Service"
   echo "########################################"
   sudo systemctl start $SVC
   sudo systemctl enable $SVC
   echo

   # Creating Temp Directory
   echo "########################################"
   echo "Starting Artifact Deployment"
   echo "########################################"
   mkdir -p $TEMPDIR
   cd $TEMPDIR
   echo

   wget $URL > /dev/null
   unzip $ART_NAME.zip > /dev/null
   sudo cp -r $ART_NAME/* /var/www/html/
   echo

   # Bounce Service
   echo "########################################"
   echo "Restarting HTTPD service"
   echo "########################################"
   systemctl restart $SVC
   echo

   # Clean Up
   echo "########################################"
   echo "Removing Temporary Files"
   echo "########################################"
   rm -rf $TEMPDIR
   echo

   sudo systemctl status $SVC
   ls /var/www/html/

else
    # Set Variables for Ubuntu
   PACKAGE="apache2 wget unzip"
   SVC="apache2"

   echo "Running Setup on CentOS"
   # Installing Dependencies
   echo "########################################"
   echo "Installing packages."
   echo "########################################"
   sudo apt update
   sudo apt install $PACKAGE -y > /dev/null
   echo

   # Start & Enable Service
   echo "########################################"
   echo "Start & Enable HTTPD Service"
   echo "########################################"
   sudo systemctl start $SVC
   sudo systemctl enable $SVC
   echo

   # Creating Temp Directory
   echo "########################################"
   echo "Starting Artifact Deployment"
   echo "########################################"
   mkdir -p $TEMPDIR
   cd $TEMPDIR
   echo

   wget $URL > /dev/null
   unzip $ART_NAME.zip > /dev/null
   sudo cp -r $ART_NAME/* /var/www/html/
   echo

   # Bounce Service
   echo "########################################"
   echo "Restarting HTTPD service"
   echo "########################################"
   systemctl restart $SVC
   echo

   # Clean Up
   echo "########################################"
   echo "Removing Temporary Files"
   echo "########################################"
   rm -rf $TEMPDIR
   echo

   sudo systemctl status $SVC
   ls /var/www/html/
fi 

```


## AMI & Template
- AMIs are specific to EC2 instances and provide the configuration for individual instances
- CloudFormation templates define entire infrastructure deployments that can include multiple AWS resources, including EC2 instances

![image](https://github.com/Keeriiim/Vagrant/assets/117115289/9ace0f58-f972-4588-bf01-bedea9e3e0f2)  

AMI 
- Copy image to change to different region
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/cd5f5045-9c7d-4bcb-ac37-7b8adec028a3)  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/d3420a2c-a4cf-48de-82e3-46dbb22a32b5)

Launch Template
- Saving a template to launch an instance
- Always use generic name ex web00 -> change to web03 etc when launching



## loadbalancer between two instances in the same AZ
- Create Target Group: Choose name & port to route through
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/659d7460-a52b-470c-9c93-5d6afabd22f7)

- Create load balancer
- Edit the security group of the load balancer to allow traffic from everywhere (that's it job)
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/208acf59-ff93-4eb6-8167-142ec78dec4d)  
- Add listening (should be health-elb)
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/6d6f1734-8f0c-4b71-934b-79a110588f10)

- Check/attach/detach security groups associated with the load balancer
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/f388d778-9e7b-4b6e-bf46-340a0368c620)

- Last step is to allow traffic FROM load balancer into the application  
  So we have to edit the security group connected to the instances
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/4e8bd1c8-a6c3-4c30-871b-b0a223c7cdea)


- Now we wait for the health check, then we can access the loadbalancer.  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/dae6958d-992e-4ca3-b82c-332d23615762)
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/f523d725-ae98-491a-a548-5d2148834fda)

- Browse DNS name
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/565439e2-e888-4974-84ae-b81d153509be)












