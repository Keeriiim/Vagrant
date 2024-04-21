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

# Snapshot
- Backup of the entire volume


