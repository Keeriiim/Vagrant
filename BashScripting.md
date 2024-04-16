# Table of Contents

- [Bash](#bash)  
- [Script](#script)  
- [Variables](#variables)  
- [Commandline arguments](#commandline-arguments)  
- [System Variables](#system-variables)
- [User Input](#user-input)


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

# Variables 
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

# CommandLine arguments
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

# System variables
- Random gives value 0 – 32767
```bash
$0               # Name of bash script
$1-9             # cmd arguments
$#               # How many arguments we passed to the script
$@               # All args supplied to the bash script
$?               # Exit satus code of most recent process/command             
$$               # Process ID of the current script
$USER            # Who is running script 
$HOSTNAME        # Name of machine running the script
$SECONDS         # Number of seconds passed from beginning of script
$LINENO          # Current line number in the script                
```

# Quotes
```bash
#! /bin/bash
SKILL= "DevOps # Same as 'DevOps' BUT " " is prefered when the value is not predefined
UP = 'uptime'  # uptime is predefined so we need ' ' to print the real value

echo "i have got $SKILL skill" # Prints i have got DevOps skill
echo 'i have got $SKILL skill' # Prints i have got $SKILL skill

echo "i got \$9 dollars' # \ is a must to print the  $ symbol
```

Advanced
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/82b46dc8-2364-4d5d-9621-73d7bcefa978)  

In this case we have already used " " and ' ' so we use ` ` for storing the entire string
```bash
#! /bin/bash
MEM=`free -m | grep Mem | awk '{print $4}'`

FREE_RAM=$(free -m | grep Mem | awk '{print $4}')
echo $FREE_RAM
```

- ( set -o posix ; set ) | less  # Finds all variables
- unset FREE_RAM # Deletes the variable

# Exporting Variables
## .bashrc or .profile - Individual for each vagrant user
- Every user has .bashrc file that is sourced (loaded) when loged in.
- Test="Hello" will be stored temporarely , if you exit and log in again it will be gone
- If you add export Test="Hello" and exit/login it will be stored permanently.


## /etc/profile - Global ..
- vim /etc/profile
  ```bash
  export Test="Global"
  ```  

![image](https://github.com/Keeriiim/Vagrant/assets/117115289/3761b67b-c107-4a0b-936c-b946eee7dff6) 
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/99017751-5ead-49e0-9981-a90564dc0864)  

Adding export to .bashrc will make it permanent for this user  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/55a75f11-5367-455a-936f-c5d945b437f0)  

Adding export to /etc/profile will make it permanent and global for ALL users  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/64b1c140-93d1-47d4-8f8d-b146f1284748)  


# User Input
This is not recommended in DevOps bcz user input is always error prone
```bash
#!/bin/bash

echo "Enter your skills:"
read SKILL

echo "Your $SKILL skills are in high demand"

read -p 'Username: ' USR   # p - prompt, waiting for input
read -sp 'Password: ' pass # sp - supress input, i.e dont show it

echo

echo "Login Successfull: Welcome USER $USR"

```

# Logical operations
## Conditional (If / else)

```bash
#!/bin/bash

read -p "Enter your number:" NBR   # 

echo "Your number is $NBR "
if [ $NBR -gt 100]; then            # Needs to be spaces around [ x y ]
#then   # optional to remove ; and add then to next row  
  echo "We have entered the if block"
  echo "Your number is greater than 100"
  echo
  date
else
  echo "Your number was not greater than 100"
fi

echo "Execution ended successfully"
echo "Process ID: $$"
echo "Number of arguments: $#"
echo "All arguments: $@"
echo "Statuscode: $?"

```




  
  
