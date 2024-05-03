- [Intro](#intro)
- [Stress](#stress)
- [Commands](#commands)
- [Troubleshooting](#troubleshooting)

# Intro
Cloudwatch is a monitoring tool.

#
```bash
apt install stress -y # Install the package to stress the system

vim bash.sh
#!bin/bash
for ((i=1; i<=3; i++)); do
    stress --cpu 1 --io 4 --vm 2 --hdd 2 -t 30s
    echo "Stress run $i completed"
    sleep 30s
done

chmod +x bash.sh


nohup ./bash.sh &     # Run the process in the background to inspect the machine
top                   # prints all processes
```
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/be65649c-d2b4-43d4-8469-bbc1abfc7151)   


## Create alarm in cloudwatch
Cloudwatch - alarm - create alarm - metric - EC" - per instance metrics - cpu utilization
Important ! - Make sure the instance id is correct for the alarm !
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/cde82a74-9565-419c-ba87-1d2cefff3ece)  

![image](https://github.com/Keeriiim/Vagrant/assets/117115289/928c1a4d-a22c-4134-84ea-8d42c5d2ce1c)  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/481c9f5c-96ac-4517-90f8-95b74e062120)  



