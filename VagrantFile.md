# VagrantFile editing  
VagrantFiles are based on ruby script. Indentation is very important.
1. Go to your folder where you have the vagrantfile.  
**Vagrant.configure("2") do |config|** - config is a variable for configuring all settings.  
**#** - Comments out the sentance  
**end** - Ends the script.

2. Remove comment from provider and change ram to 1600.  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/a5f568d3-b983-4ab6-b33c-7d1baaa3832b)

3. Bridge networking.  
Public network means bridge interface, this is going to fetch IP address from your router. The ip will still be private and not accessable from the internet
Make the network public via bridged adapter(your router)(accessable from the internet)
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/9a917470-1a72-4367-9ca7-1c34d6776de2)

4. Pinging physical host machine from ubuntu vm.
**ipconfig** - Run this on cmd and save the local ipv4 inet. Disable Microsoft Defender Firewall.
Then go to your vagrant machine and write ping 192..........  
You should recieve something like:  **64 bytes from 192.........: icmp_seq=303 ttl=128 time=0.822 ms**  
IF you dont recieve anything, then there is something stopping the connection which requires troubleshooting.




  
