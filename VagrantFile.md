# VagrantFile editing  
VagrantFiles are based on ruby script. Indentation is very important.
1. Go to your folder where you have the vagrantfile.  
**Vagrant.configure("2") do |config|** - config is a variable for configuring all settings.  
**#** - Comments out the sentance  
**end** - Ends the script.

2. Remove comment from provider and change ram to 1600. Add vb.cpus = "2" for clarity.
   If the vm is running -> vagrant reload to apply changes.    
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/6f7f927d-23bd-40bd-a321-bbac8c56c85c)

3. Bridge networking.  
Public network means bridge interface, this is going to fetch IP address from your router. The ip will still be private and not accessable from the internet.
Make the network public via bridged adapter(your router)(accessable from the internet)
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/9a917470-1a72-4367-9ca7-1c34d6776de2)

4. Pinging physical host machine from ubuntu vm.
**ipconfig** - Run this on cmd and save the local ipv4 inet. Disable Microsoft Defender Firewall.
Then go to your vagrant machine and write ping 192..........  
You should recieve something like:  **64 bytes from 192.........: icmp_seq=303 ttl=128 time=0.822 ms**  
IF you dont recieve anything, then there is something stopping the connection which requires troubleshooting.

5. Set a static ip. Change the third octet to 3,4 or 56 because they are common in VMs. The forth octet should start from 2.  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/e9b79609-98af-43d9-9b42-0cd749f7fc14)  
Nat is the host(VM) ip that usually starts on 10. Host only is the static ip. Bridged is the bridged adapter.  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/bf7ade6d-fe92-4b23-8587-87c41e4bb484)  

6. **ip addr** - displays all ip adresses for the vm. Else they may be printed when logging in. 
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/fbeed7a6-2ec6-4b9f-ab40-5acd26e5e052)  

7.To check the ram & cpu see the settings in your VM or type   
  **free -m** - Check the ram  
  **cat /proc/cpuinfo** - check cpu setting   
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/9858510e-5922-44b4-9c61-ee509963f4dc)  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/f81f4acc-28ff-4b00-a4c2-efe01ef5e25e)  


## Sync Directories
1.**cd /vagrant/** - /Vagrant is the default sync D of the VM. Enables you to see, create, delete and update all files in the path on the host machine from the VM.  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/d071f365-9b8e-46e3-ac27-879571f1eee7)  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/a75de4d0-81d9-4b2f-9d3e-901b3368a9cc)  

2. The sync path in the VM can be changed from the Vagrantfile.
   The host machine folders HAS to be created before setting the path, the guest machine(VM) will get created from the config.
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/9c30879b-dbf3-47e6-8219-2dd442d97edc)
Additional sync diretory has been added after reload.  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/b86ad7a2-a282-4475-8861-f6e50b1c5f53)

## Provisioning  
1. The provisioning should not be interactive, it's like a script that should run.
The script can be from docker, puppet, ansible etc. The language should be based on current OS. yum for centos, apt for ubuntu.  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/c57605e4-9772-4e0f-a970-348cdd58b11e)  
**vagrant provision** - If the Vm already is provisioned/bootstrapped, i.e created. Then you need to run.  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/abdcc61c-cf2e-4cb6-85ea-35e64ade39e1)

2. By default ubuntu starts the http service, centos does not. After provisioning search for the ip adress in your webbrowser.  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/e80ab6e3-2478-4451-ad0c-8d366c20f2fa)








 







 









  
