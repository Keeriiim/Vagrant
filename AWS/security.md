

# Introduktion
[Read](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-security-groups.html)  
Security-groups are the virtual firewall for the cloud
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/0b9e7409-f805-4fd1-a1b0-10960009f62b)  


## Rules
- Inbound: Any traffic going to the instance
- Outbound: Any traffic going from the instance
- Any port opened for inbout will automatically work for outbound aswell.
- Inbound rules can ONLY focus on PUBLIC HOST ADRESSES!, not private...for private use VPC

# Instances
- Dynamic ip by defualt
- For static choose elastic ip

## Elastic IP
- Allocate elastic ip -> choose correct region -> allocate -> actions -> associate
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/9881bc72-4ebe-45ca-b9af-3a8c0db1a872)
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/6803c7c6-aa3e-40bc-8d45-039812086c43)

After deleting/terminating choose
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/c5e503c3-4444-4e2f-8058-b9b5e172c274)



