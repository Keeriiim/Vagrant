# Table of Contents

- [Bash](#bash)  
- [Script](#script)  
- [Home network](#home-network)  
- [TCP / UDP](#tcp--udp)  
- [Port Communication](#port-communication)


# Bash
Bash: Stands for "Bourne Again SHell." It's a command language interpreter that is widely used in Unix-like operating systems for executing commands from a script.

- " #! " (Shebang): tells the system which interpreter should be used to execute the script. 
- " #!/bin/bash " at the top of a script tells the system to use the Bash interpreter to run the script.

## Relative and Absolute Paths:
- Relative Paths: Paths that are specified relative to the current working directory. For example, if you are in /home/user/, a relative path might be documents/file.txt, which refers to the file.txt in the documents directory within the current directory.
- Absolute Paths: Paths that specify the full directory structure from the root directory. For example, /home/user/documents/file.txt is an absolute path that specifies the location of file.txt starting from the root directory (/).

## Different shells
- Python
  ```bash
  #!/usr/bin/env python3
  import os
  print("Hello, this is a Python script!")
  print("The current directory is:", os.getcwd())
  ```
  
  
- Ruby :
  ```bash
  #!/usr/bin/env ruby
  puts "Hello, this is a Ruby script!"
  puts "The current directory is: #{Dir.pwd}"
  ```
- Vagrantfile :
  The Ruby code in your Vagrantfile is using the Vagrant DSL (Domain-Specific Language). 
  This is a specific set of Ruby methods and syntax provided by Vagrant to define and configure virtual machines (VMs) and their environments.
  In the Vagrantfile, you use this DSL to describe the virtual machines, their settings, network configurations, provisioners, and more.


# Script
- vim test.sh : to create a script
- chmod +x test.sh to make it executable
- ./test.sh to run it
-  > /dev/null : redirects successfull output but shows errors on screen!
    
```bash
#!/bin/bash

# Installing Dependencies
echo "########################################"
echo "Installing packages."
echo "########################################"
sudo yum install wget unzip httpd -y > /dev/null
echo

# Start & Enable Service
echo "########################################"
echo "Start & Enable HTTPD Service"
echo "########################################"
sudo systemctl start httpd
sudo systemctl enable httpd
echo

# Creating Temp Directory
echo "########################################"
echo "Starting Artifact Deployment"
echo "########################################"
mkdir -p /tmp/webfiles
cd /tmp/webfiles
echo

wget https://www.tooplate.com/zip-templates/2098_health.zip > /dev/null
unzip 2098_health.zip > /dev/null
sudo cp -r 2098_health/* /var/www/html/
echo

# Bounce Service
echo "########################################"
echo "Restarting HTTPD service"
echo "########################################"
systemctl restart httpd
echo

# Clean Up
echo "########################################"
echo "Removing Temporary Files"
echo "########################################"
rm -rf /tmp/webfiles
echo

sudo systemctl status httpd
ls /var/www/html/

```

## Variables 
- Temporary storage in RAM
- Editing previous script with the use of variables

```bash
#!/bin/bash

# Variables
PACKAGE = "wget unzip httpd"
SVC="httpd"
URL="https://www.tooplate.com/zip-templates/2098_health.zip"
ARTIFACT_NAME="2098_health"
TEMPDIR="/temp/webfiles"


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
mkdir -p /tmp/webfiles
cd $TEMPDIR
echo

wget $URL > /dev/null
unzip $ARTIFACT_NAME.zip > /dev/null
sudo cp -r $ARTIFACT_NAME/* /var/www/html/
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
```

## CommandLine arguments
- Bash can take up to 9 cmd arguments $1 - $9
```bash
#! /bin/bash

echo "Value of 0 is "
echo $0

echo "Value of 1 is "
echo $1

echo "Value of 2 is "
echo $2

echo "Value of 3 is "
echo $3
```
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/16b793ce-487f-42d7-9bd0-29c670cedfcd)



  
  
