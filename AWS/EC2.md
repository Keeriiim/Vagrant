- [Ec2](#ec2)
- [Create instance](#create-instance)



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
- Create account -> Ec2 -> Launch instance

## Tags  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/d2845694-72d9-448f-8fec-7d3ab1a8b7c6)

  
## AMI
- Choose AMI based on your needs (Linux, windows, x86 /arm, size/performance)  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/fde223ca-54c9-4439-8e6d-55f8b643dd70)




## Key Pair  
- Key pairs allow you to connect to your instance securely. [Read](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html?icmpid=docs_ec2_console#having-ec2-create-your-key-pair)
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
- 




