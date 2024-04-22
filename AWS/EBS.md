- [Intro](#intro)
- [EBS](#ebs)
- [Snapshot](#snapshot)


# Intro - A virtual harddisk
Amazon Elastic Block Store (Amazon EBS) is an easy-to-use, scalable, high-performance block-storage service designed for Amazon Elastic Compute Cloud (Amazon EC2)  
Provides 2 things:  
- EBS Volume (virtual harddisk)
- EBS Snapshot (backup of EBS volume)

![image](https://github.com/Keeriiim/Vagrant/assets/117115289/492f04ce-888e-4b68-99b4-2dd3d98a4914)  

# EBS
[Read](#https://aws.amazon.com/ebs/)
[Read](#https://docs.aws.amazon.com/ebs/latest/userguide/what-is-ebs.html)
- Blockbased storage
- When we see the GB on our EC2, its the EBS (root volume)
  Stores the OS data and can be used to store DB data, webbservers, file data
- Placed in a SPECIFIC AZ.
- Automatically replicated within the AZ to protect from failure

## EBS Types
There are different types of harddisks..
1. General purpose (SSD)  
   Use cases:  
     * Most work loads ( example : webbservice )
2. Provisioned IOPS (The I/O (input/output) speed is more than GP SSD)
   Use cases:
     * Large Databases
3. Throughput Optimized HD
   Use cases:
     * Big Data & Data warehouses
4. Cold HDD (Generally lowcost)
   Use cases:
     * File Servers
5. Magnetic (lowest I/O & cost)
   Use cases:
     * Backups & Archives
  


## EBS on AWS
This is the same as Ec2 - > Elastic Block Store -> Volumes 
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/dece0176-ba92-4962-b1aa-26cfc1858a44)  
- Rename the volume to ec2Name-ROOT-Volume (ex webbserver-ROOT-Volume)
- SAME AZ as ec2 instance


- Create Volume & Attach  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/bcfa8439-d13a-4e6f-b9ea-47f9497f714e)


## Linux command for disks
- ***fdisk -l***    # Lists all disks 
- ***df -h***    # Show partitions  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/700962b5-077d-40f2-a23c-f91a96babeb0)  

### New partition
- Go to your disk
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/646ebdc5-f010-433c-82b8-e174f3bd9278)  
- fdisk /dev/DISKNAME , press m from more info
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/bc784bb5-38d8-4cdc-aa7e-65b72eb93902)
- n, p, 1, enter for default, last sector is to specify size +3 is to allocate 3GB.  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/3c31572e-813d-4aee-9ca9-4a5c78ffdd64)
- P to print, w to write  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/4f8810e9-0d61-463f-b0b4-6e82245ddb01)
- Partition created fdisk -l  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/9a40b618-7d54-4b6d-9dde-cf8190994915)

## Formating
- ***find / -name "mkfs.*" -type f -executable***    #shows the different mkfs to use
- mkfs is to create a filesystem
- ***mkfs.ext4 /dev/xvdf1***  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/43117c94-4824-4eae-a6b7-0464acda9a15)  

- Temporary mount that dissapears when relog.  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/545b52d2-bc7b-4d25-b9da-85749b4e039b)  

- ***vi /etc/fstab***  
is a crucial configuration file for managing filesystems and their mount points in Unix-like operating systems. Administrators often edit this file to add, remove, or modify filesystem entries based on changes in hardware configuration or system requirements
Partition part /tab/ mount location /tab/ formatType /tab/ options /tab/ dumpcode space file-system-check
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/f3255ec0-f08c-4380-a172-8ec7c9824037)
- When done write mount -a , if u did something wrong u will get the error there
- df -h to check if all is done, after restart service  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/d4d62195-ab4d-40a8-9f41-76164009ca2b)

- vi /etc/selinux/config -> disable it if you need (not seeing images)
- reboot

















# Snapshot
- Backup of the entire volume


