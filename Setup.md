# Before working with Vagrant it's recommended that you have a package manager installed on your OS. A package manager is a software application that you can use to download tools like mysql, vagrant, git bash e.t.c.
The benefit of having a manager is that you don't have to look for the correct download links and updated version on the internet. The manager handles that for you. All you have to do is to communicate through the CLI for what you want to do!

# Installation
## Windows: Chocolatey
1. Search for windows powershell, right click and open it in administrator mode.
2. Type  
Get-ExecutionPolicy
3. If you get Restricted type  
 Set-ExecutionPolicy Bypass -Scope Process
4. Type  
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
2. Open your terminal and type cd, then run  
xcode-select --install
3. Run     
export HOMEBREW_BREW_GIT_REMOTE=https://github.com/Homebrew/brew.git  
export HOMEBREW_CORE_GIT_REMOTE=https://github.com/Homebrew/homebrew-core.git  
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
4. Search for any software at [brew](https://brew.sh/)

**Brew Commands!**
* **Check current version** brew --version
* **Install a package** brew install packageName
* **Uninstall a package** brew uninstall packageName
* **List all installed packages** brew list
* **List all outdated packages** brew outdated
* **Fetch the lates updates** brew update
* **Update all packages**  brew upgrade
  
