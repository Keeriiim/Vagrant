# Linux Training

1. Go to your folder where you have the vagrantfile
2. **Start the VM** vagrant up
3. **Log into the VM** vagrant ssh
4. **Download Vim** sudo yum install vim -y

## Linux Commands
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
**rm -r dir** Deletes a dir
**cp a b/** Copies file into directory/map b  
**cp -r dev ops/** Copies dev directory into ops  
**mv a b/** Moves file/directory  a into directory/map b  
**mv a.txt b.txt** Moves/replaces the name a to b  
**mv "*"** Moves everything in the dir  
**mv "*".txt** Moves all .txt files  
**History** See all prompted commands  
**Os** cat /etc/os-release  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/174d8d21-3ca3-472e-883e-55f0b3c13b04)

## Filetypes
- Type ls -l to see filetypa in current directory
<img width="647" alt="image" src="https://github.com/Keeriiim/Vagrant/assets/117115289/dd55fed5-2ef2-4c62-8e86-cdae0c44180a">

 
# Vim
1. **Open a .txt file you created** vim file1.txt
2. **Add text**


#Vim commands
**Enter insert mode to write** Press i  
**Exit insert mode** Press esc  
**Save the file** Type :w  
**Exit the file** Press esc and type :q  
**Save & Exit** esc, then type :wq  
**Force quit without any change** :q!  
**See number lines** :se nu  
**Shortcut to line 1** gg
**Shortcut to last line** shift+g
**Copy line** yy  
**Paste below current line** p     
**Paste above current line** shift + p  
**Delete/cut line** dd  
**Undo change** u  
**Search for a word and scroll through the list** /word , press  n for search



![image](https://github.com/Keeriiim/Vagrant/assets/117115289/379c939b-66d9-4b9e-914d-701f21f3327a)


- **Portable Environments:** Vagrant enables developers to create a single configuration file (Vagrantfile) describing the project's environment. This configuration can be shared and used across various machines and team members, ensuring consistent development environments.

- **Virtualization Support:** Vagrant supports multiple virtualization providers, such as VirtualBox, VMware, and Hyper-V, offering flexibility for developers to work with their preferred technology.

- **Provisioning:** Developers can automate the setup of software and configurations inside the virtual machine using tools like Puppet, Chef, or shell scripts, ensuring automatic provisioning of the environment.

- **Networking:** Vagrant provides options for configuring network settings, allowing developers to expose specific ports, create private networks, or use public networks to make services inside the virtual machine accessible.


