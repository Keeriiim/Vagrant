# Before working with Vagrant, it's recommended to have a package manager installed on your operating system. A package manager is a software application that facilitates the downloading and management of packages, such as MySQL, Vagrant, Git Bash, and more..
The benefit of using a package manager is that you don't have to search for correct download links and updated versions online. The manager handles these tasks for you. Your only task is to communicate your needs through the command-line interface (CLI)!

# Installation
## Windows: Chocolatey
1. Search for windows powershell, right click and open it in administrator mode.
2. Run 
Get-ExecutionPolicy
3. If you get Restricted Run  
 Set-ExecutionPolicy Bypass -Scope Process
4. Run
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
5. If you don't see any errors, all is complete !
6. Search for any software at [Chocolatey](https://community.chocolatey.org/packages)

**Choco commands!**  
* **Check the version** choco
* **Install a package** choco install packageName
* **Uninstall a package** choco uninstall packageName
* **List all installed packages** choco list
* **List all outdated packages** choco outdated
* **Update all packages**  choco upgrade all  


## Mac: Homebrew
1. Go to [brew](https://docs.brew.sh/Installation) 
 !Check the MacOS requirements!
2. Open your terminal and Run cd, then run  
xcode-select --install
3. Run     
export HOMEBREW_BREW_GIT_REMOTE=https://github.com/Homebrew/brew.git  
export HOMEBREW_CORE_GIT_REMOTE=https://github.com/Homebrew/homebrew-core.git  
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
4. Search for any software at [brew](https://brew.sh/)

**Brew Commands!**
* **Check current version** brew --version
* **Install a package** brew install --cask packageName
* **Uninstall a package** brew uninstall packageName
* **List all installed packages** brew list
* **List all outdated packages** brew outdated
* **Fetch the lates updates** brew update
* **Update all packages**  brew upgrade
  

# Installing Tools for Vagrant (Windows)
choco install git  
choco install virtualbox  
choco install vagrant  

1. Go to your BIOS and enable Virtualization (VTx / Secure virtual machine / Virtualization)
2. Search for Windows features -> disable Microsoft Hyperv, Windows Hypervisor platform, Windows Subsystem for linux, Docker Desktop, Virtual Machine Platform
3. Reboot your compter
4. Open git bash, run the following commands  
mkdir /c/vagrant-vms  
cd /c/vagrant-vms  
mkdir centos  
cd centos  

5. Go to [Vagrant](https://app.vagrantup.com/boxes/search) and search for centos 9.
6. Run  
vagrant init generic/centos9s
7. Run cat Vagrantfile to see if it was successfully installed
8. In order for the vagrant commands to work, you always need to be in that folder where the vagrant file was created!

**Vagrant Commands!**
* **Check the vagrantfile** cat Vagrantfile
* **Start the VM** vagrant up
* **Status of VM** vagrant status
* **Shutdown the VM** vagrant halt
* **Log into the VM** vagrant ssh
* **Exit the VM** logout
* **Reboot the VM** vagrant reload
