# Linux overview

# Linux Commands
**Commands Options Arguments** Structure is as follows, ex ls -a /temp  
**Command -help** Shows all Options for the specific command
**Relative path** Default path i.e your home folder, you can directly access folders within it, ex cd /Downloads  
**Absolute path** The full path ex cd /users/JohnDoe/Downloads  
**clear** Clears the terminal  
**pwd** Shows current directory location  
**mkdir a** Creates a directory/map  
**rmdir a** Deletes a directory/map  
**touch file.txt** Creates a file  
**rm file.txt** Deletes a file  
**cp a b/** Copies file into directory/map b  
**cp -r dev ops/** Copies dev directory into ops  
**mv a b/** Moves file/directory  a into directory/map b  
**mv -r dev ops/** Copies dev directory into ops 
 




## Key Features and Concepts

- **Portable Environments:** Vagrant enables developers to create a single configuration file (Vagrantfile) describing the project's environment. This configuration can be shared and used across various machines and team members, ensuring consistent development environments.

- **Virtualization Support:** Vagrant supports multiple virtualization providers, such as VirtualBox, VMware, and Hyper-V, offering flexibility for developers to work with their preferred technology.

- **Provisioning:** Developers can automate the setup of software and configurations inside the virtual machine using tools like Puppet, Chef, or shell scripts, ensuring automatic provisioning of the environment.

- **Networking:** Vagrant provides options for configuring network settings, allowing developers to expose specific ports, create private networks, or use public networks to make services inside the virtual machine accessible.

![image](https://github.com/Keeriiim/Vagrant/assets/117115289/174d8d21-3ca3-472e-883e-55f0b3c13b04)