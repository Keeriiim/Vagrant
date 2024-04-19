- [Ec2](#ec2)
- [Create instance](#create-instance)
- [Project 1](#project-1)
- [Delete](#delete)



# EC2

Amazon ECS (Elastic Container Service) is a fully managed container orchestration service provided by Amazon Web Services (AWS). It allows you to run, stop, and manage Docker containers on a cluster of EC2 instances. 

## Pricing
1. On demand (pay per hour)
2. Reserved (Reserve capacity, 1 or 3 yrs with a discount)
3. Spot (bid your price for unused ec2 capacity)
4. Dedicated Hosts (Physical server dedicated for you)

## Components

- AMI (Amazon Machine image)
Provides the info required to launch an instance (virtual server in the cloud)

- Instance type (Size, memory, cpu, ram, network speed, storage) 
When launcing, the type you specify determines the hardware of the host computer used for your instance.

- EBS (Amazons Elastic Block Store)
Provides you with flexible, cost effective & easy to use data storage for your instances.
Its the virtual hard disk on wich you can store your operating system.

![image](https://github.com/Keeriiim/Vagrant/assets/117115289/d2d9d672-1d73-40eb-b4ba-fdb4788221ee)





## Tag
Tags are simple label consisting of a customer defined key and an optional value that can make it easier to manage, search for and filter resources.

## Security Group
Acts as a virtual firewall that controlls the traffic for one or more instances

## Log in 
Amazon EC2 uses public-key crytopgraphy to encripty and decrypt login information
Create - Download

- Linux: Use key for SSH
- Windows: Use key to generate password
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/7d390428-f606-4fa8-8303-b30d58e10cc7)



# Create instance
- Create account -> Ec2 -> Launch instance [Read](https://aws.amazon.com/ec2/instance-types/)

## Tags  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/d2845694-72d9-448f-8fec-7d3ab1a8b7c6)

  
## AMI
- Choose AMI based on your needs (Linux, windows, x86 /arm, size/performance)
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/fde223ca-54c9-4439-8e6d-55f8b643dd70)




## Key Pair  
- Key pairs allow you to connect to your instance securely. [Read](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html?icmpid=docs_ec2_console#having-ec2-create-your-key-pair)
- Good practice is 1 key-pair for stage (dev, QA, prod)
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/4d0ef410-bd69-4f42-a17f-a21e8d0fa219)  

- Rsa / ED25519
```bash
- RSA uses larger key sizes (2048 bits or larger).
- Ed25519 uses fixed-size keys (256 bits), offering simpler and more efficient implementation.

*** Security ***
- Both RSA and Ed25519 are secure with appropriate key sizes.
- Ed25519, based on elliptic curve cryptography (ECC), is believed to offer stronger security for a given key size compared to RSA.

*** Performance ***
- Ed25519 generally offers better performance, especially for key generation, signing, and verification operations.
  Its fixed-size keys and efficient elliptic curve arithmetic make it faster and more resource-efficient than RSA.

*** Signature Size ***
- Ed25519 signatures are fixed-size (64 bytes), while RSA signatures vary in size depending on key size and padding scheme.
  This can impact the size of signed data and the efficiency of signature verification, especially in bandwidth-constrained environments.
```

- Key examples
```bash
RSA:
-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEAnls+8QLvx8coPVCboB3+c1LbG/eY9gRAfxQZr39xaVVprzJC
4UN/rL6ZL8HSFZd3TNe35A9w9yOKNMiP5IwdFaYM1n9fBxcD+IGUvOQS6EcZfthP
TFbS0JnY4mJ4kxNO6jKfY6Qy4M2wPpSTWVmb16Btxv6e3VnjwXI2Z1hvRRVHgcRU
0zvsGAOk50U0Sn+Cp350w/sNJDbnaQ9uvbbM8eXUKw6F/o0eg3FPzYX2o0kvPfdd
qwuql3v10eHAlAOff/8otZ5mPEve2t3lD1QDXIvBDsSzx6wuue4xCJ1+xFv//KJI
sq1QScpZCWRmFt3rSITRRTnIlwNugRWQaPcHeQIDAQABAoIBAHxWZMtUZPVV+NB7
9FX6dwoR6pzBAkdY+1NMcwaLaH8uY3b+XekF2L/IP/txkgUGEtQxJOBbB3XlX+Ul
/WWUZlnTMY1SIUkt1x5OkHzoD7h16xzftxPXsFu+EL9gVhAVPwdAjEnuaUx99H6O
pkunwmfCPa/byN1AcUY46WKn22Y/l+E0tUUjTC5ucHEt0rW5qxsBUhzqChdSPClY
/WQ4ZVECR8iZ0DNy2zGJ9QuGPDMYycIvPkkNPFCTBUa3KX3ZrJvancHumHK1WFn5
Ovm8FkVWJ22ABBc0WXuR3iHEuKDRVryr7/a8WwGBjcpvaC/EbU/tDfrEmJUcPKlb
H4fuC0kCgYEA8Hch66BkDSkvgF19fmR0ImHeZBivF0VTLq223OEBbH/Y8k1pYP8S
mvmaACezi9zO8py+XiYkveVTiR1WXxM0HnRoHVeM3yDPG4apayDLQkZ5L8TCvOFv
T3yPf6XdfEN5GyAWd1kFP20oNFEKYMzKlCN7p62XXf9hLs4xQ8u/ZcMCgYEAqJYt
pZ1sYDuULkBMj8huiEHSgV67VY09Rd9ok08NqgcXYB1+0Exn2D1ZymvyehdqKd6U
Fjab5VV/hsZzuBTywRCl/bQc9VDFF93Ip6WG2pIYbySUPUnfnlZRQxfkmnhR08SB
AlHxm0j29aW6wAhQWPvPysLVeOvsyMzK19ZZ/hMCgYEArCCa50+oTsNsfTZu3kqJ
1xK3Xm9M5ht5r7ApdXKa0k+xu8At7oCnkMeatQG2RCeK+5+3pS0on8XIRh359ZSJ
ekNZQ6en7xBNMCb0nvqahJZtqQPvYcT9KKjBD15rbMffqMsPSd8vInfAj7Jy+1ec
qu27Vgusjlx/9EEkgqMWHoECgYAlQ3y3fMJ1yvWH+6Jwrabw60uyWNQjpuKCTU16
MiEdEhAyqJJdTGYvv+/W9GFWZ1KKCq7E8jEnUeysR7VQXSEDV8C5AVTdTIskKVuu
4sGaEmzgND+oBGovP3ka0W8wTaQYoPi7II28+zXLOmS7CZto79AQS1yQK+XcxJeZ
ecHOjQKBgEjnEOYz5/ZUDDv/4ai1lcFSDI1Px1n0j4DGq+rdv0k189uZQnm2kOco
NkoSe3rL/32R7NtRQo4K8RCP2lumpRfkltQzhv2VfzaKzV/tp5y79hhTddesa9NI
6eYVwMH4hgosEkt/+62xGCA+P0ZBhtEzAUgkbeFx621dz85/016a
-----END RSA PRIVATE KEY-----


ED25519:
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAAAMwAAAAtz
c2gtZWQyNTUxOQAAACD/QHxusWtd47jLGIMQyYFmZLmrcw5zejG8k3RRrwg4QwAA
AIh24I0XduCNFwAAAAtzc2gtZWQyNTUxOQAAACD/QHxusWtd47jLGIMQyYFmZLmr
cw5zejG8k3RRrwg4QwAAAEAwUQIBATAFBgMrZXAEIgQgtH3kTgKa/MB2SnhtjUos
zv9AfG6xa13juMsYgxDJgWZkuatzDnN6MbyTdFGvCDhDAAAAAAECAwQF
-----END OPENSSH PRIVATE KEY-----
```

## Network
- Press Edit to change the name etc
- [Read](https://docs.aws.amazon.com/en_us/AmazonRDS/latest/UserGuide/CHAP_Tutorials.WebServerDB.CreateVPC.html#CHAP_Tutorials.WebServerDB.CreateVPC.SecurityGroupEC2)  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/841bcd31-fe5d-481f-820c-09c21e10990e)  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/a8ec00ee-b92e-446f-8b65-c69295244d08)  

## Storage
- [Read](https://docs.aws.amazon.com/ebs/latest/userguide/what-is-ebs.html?icmpid=docs_ec2_console)  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/c3c0dff8-e463-44f8-8f58-e7b03bf2c52f)

## Advanced details

![image](https://github.com/Keeriiim/Vagrant/assets/117115289/7816d0fa-3612-457a-a9ff-eaa793820253)  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/86c944aa-6fd0-4c17-a241-ae4409ae7474)  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/443a480f-9446-48d1-b8a6-519058ffd273)  


# Connect to instance
- Find ur instance - > Press on Connect -> SSH Client
- Once the SSH is established, the communication is going through port 22 which if allowed, the rest will be allowed.
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/7e8c2fef-bc2f-42b5-bdb0-2fc0e42ecbed)

## From Git Bash
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/fdc2e05d-c803-4c57-900b-7f024130ab3a)  
```bash
Inside the SSH(port 22) you can browse localhost for the httpd
[root@ip-172-31-84-153 ~]# curl http://localhost
<html><body><h1>It works!</h1></body></html>
```

## From windows
```bash
Outside SSH you can not browse because HTTP is using port 80 which currently is not enabled in the AWS firewall

C:\Users\kerim\Downloads>curl http://localhost
curl: (7) Failed to connect to localhost port 80 after 2254 ms: Couldn't connect to server

C:\Users\kerim>curl http://localhost:22
curl: (7) Failed to connect to localhost port 22 after 2247 ms: Couldn't connect to server

C:\Users\kerim>curl http://54.152.95.201:22
curl: (1) Received HTTP/0.9 when not allowed

C:\Users\kerim>curl https://54.152.95.201:22
curl: (35) schannel: next InitializeSecurityContext failed: SEC_E_INVALID_TOKEN (0x80090308) - The token supplied to the function is invalid
```

Lets try to figure out with SSH
```bash
C:\Users\kerim>C:\Users\kerim>ssh http://54.152.95.201:22
'C:\Users\kerim' is not recognized as an internal or external command,
operable program or batch file.

C:\Users\kerim>C:\Users\kerim>ssh 54.152.95.201:22
'C:\Users\kerim' is not recognized as an internal or external command,
operable program or batch file.

C:\Users\kerim>ssh -p C:\Users\kerim>C:\Users\kerim>ssh 54.152.95.201:22
Bad port 'C:\Users\kerim'

STILL WRONG BUT APPROACHING THE CORRECT WAY: 
C:\Users\kerim>ssh -p 22 54.152.95.201
The authenticity of host '54.152.95.201 (54.152.95.201)' can't be established.

GOIN TO THE DIRECTORY I HAVE THE KEY DOWNLOADED:
C:\Users\kerim>cd Downloads

C:\Users\kerim\Downloads>ssh -p 22 54.152.95.201
kerim@54.152.95.201: Permission denied (publickey,gssapi-keyex,gssapi-with-mic).

CORRECT WAY:

C:\Users\kerim\Downloads>ssh -p 22 -i "Linux_SSHkey_ED.pem" ec2-user@54.152.95.201
   ,     #_
   ~\_  ####_        Amazon Linux 2023
  ~~  \_#####\
  ~~     \###|
  ~~       \#/ ___   https://aws.amazon.com/linux/amazon-linux-2023
   ~~       V~' '->
    ~~~         /
      ~~._.   _/
         _/ _/
       _/m/'
Last login: Fri Apr 19 10:12:40 2024 from 78.82.182.26

[ec2-user@ip-172-31-84-153 ~]$ curl http://localhost
<html><body><h1>It works!</h1></body></html>
```

# Project 1
- Installed Httpd
- curl to localhost
- Open port 80:   Ec2 -> instances -> web01 -> Security -> web-sg -> open sg groups  -> Edit inbout groups -> add port 80
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/4df0ffe4-8873-49d1-a0d3-800ccdffb187)  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/5302f95a-e705-4dd3-8f1e-137529479a9a)


```bash
C:\Users\kerim\Downloads>curl http://54.152.95.201
<html><body><h1>It works!</h1></body></html>
```

# Delete
Delete Key Pairs
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/8a532d51-ea94-4f8e-863f-4f979379c046)  

Terminate instances  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/408f5295-ed55-402e-bf2f-6d74b60a587c)    


Delete sg group -> delete web-sg  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/ee35e157-6684-4032-b9f2-31f2d1161b4f)



# Project 2
- Create new instance with new tags
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/ce192bf9-9a7a-496a-97a6-b75af31e9139)
- Ubuntu, free tier type, new SSH keypair, 



Successfully created network interface eni-06e64d9882af0c5e8 var ???












