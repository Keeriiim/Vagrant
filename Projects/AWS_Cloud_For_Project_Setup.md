






# Intro
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/8093eb39-2d31-4da9-9627-13b6920f1336)  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/c39a800b-e59e-4992-afc3-9453b8dc8568)  

# Problems
- Complex Team Management
- Difficulty scaling up/down
- Huge resource cost (UpFront Capex & Regular OpEx)
- Most processes will be manual
- Difficult to automate
- Time consuming

# Solution - Cloud Setup
- We dont pay upfront, rather pay as we go -> IAAS (Infrastructure as Service)
- Flexibilit , easy to scale
- Easier to manage infrastructure
- Automation -> to avoid human errors -> IAAC (Infrastructure as Code)

![image](https://github.com/Keeriiim/Vagrant/assets/117115289/77813ea3-1a6e-4cbd-a180-10aff3f937ba)  

# Architecture
- Ec2 instances
- ELB
- Autoscaling
- EFS/S3 for shared storage
- Amazon certificate manager
- Route 53 service


Users will access our website with an URL
URL will point to ELB enpoint, mentioned in Godaddy DNS
User browser/App will use the endpoint to connect to the loadbalancer by using https
Certificate for https encryption will be mentioned in Amazon Certificate Manager Service

Our loadbalancer will be in a security group & only allow https traffic
Then the lb will route the request to tomcat instances.
Apache tomcat service will run on some set of instances which will be managed by autoscaling. Scaling will be based on the load.
These ec2 instances will be in a separate security group and will only allow traffic on port 8080 only from the loadbalancer.

We know application, our vprofile application sits on Tomcat instance.

We have seen this in our previous project.

And our application needs backend servers, which are MySQL, Memcache and RabbitMQ. Information

of backend services or the backend server IP address will be mentioned in Route 53 private DNA zone.

So Tomcat instances will access back server with a name which will be mentioned in Route 53.

Private dns where the private IP address of our background servers will be mentioned.

These backend ec2 instances, which will be running my sql, RabbitMQ Memcache will be in

a separate security group.

So the AWS. sources, which are in use over here are first Amazon certificate manager for a certificate

application load balancer.

Set of ec2 instances for Tomcat, Memcache Rabbit, MQ and my sql, three separate security groups.

Amazon Route 53 for DNS Private Zones.

And also, there's Amazon S3 bucket to store our software artifacts.

Now, I recommend you pause the video and watch this architectural diagram once again.

Will start the execution now, and this is the flow of execution, first, we will log into our AWS

account.

We're going to key pairs, which will use to login to our ec2 instances.

We create security groups for load balancer, Tomcat and backend services. We will launch instances with

user data, which will be our bash scripts. We will update IP to name mapping in Route 53.

We're going to then build our application from source code, this will do it on our local machine,

on our laptop.

And we upload our artifact to a s3 bucket. From S3 bucket we will download our artifact to ec2

instance, where tomcat service will be running.

Then we'll set up a load balancer with https connection.

Will map our elastic load balancer and point to a website in GoDaddy DNS and will verify. Once we verified

our entire set up, then we'll build an auto scaling group for a Tomcat instances.






