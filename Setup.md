## Before working with Vagrant it's recommended that you have a package manager installed on your OS. A package manager is a software application that you can use to download packages like mysql, vagrant, git bash e.t.c.
The benefit of having a manager is that you don't have to look for the correct downloads links and updated version on the internet. The manager handles that for you. All you have to do is to communicate through the CLI for what you wnat to do!

## Installation
# Windows: Chocolatey

Search for windows powershell, open it in administrator mode.

# Mac: Homebrew
* Go to [brew](https://docs.brew.sh/Installation) 
 !Check the MacOS requirements!

* Open your cmd and type cd , then xcode-select --install

* Then 
  export HOMEBREW_BREW_GIT_REMOTE=https://github.com/Homebrew/brew.git
  export HOMEBREW_CORE_GIT_REMOTE=https://github.com/Homebrew/homebrew-core.git
  /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"

* Write this to see if its finished to check the current version
  brew --version

* Write this to download Vagrant
  brew install --cask vagrant


[Vagrant](https://www.vagrantup.com/) is an open-source software product designed for building and managing portable virtual software development environments. These environments are utilized for software development, application testing, and software configuration in a reproducible and portable manner. Vagrant simplifies the process of creating, sharing, and replicating development environments through a user-friendly command-line interface.

## Key Features and Concepts

- **Portable Environments:** Vagrant enables developers to create a single configuration file (Vagrantfile) describing the project's environment. This configuration can be shared and used across various machines and team members, ensuring consistent development environments.

- **Virtualization Support:** Vagrant supports multiple virtualization providers, such as VirtualBox, VMware, and Hyper-V, offering flexibility for developers to work with their preferred technology.

- **Provisioning:** Developers can automate the setup of software and configurations inside the virtual machine using tools like Puppet, Chef, or shell scripts, ensuring automatic provisioning of the environment.

- **Networking:** Vagrant provides options for configuring network settings, allowing developers to expose specific ports, create private networks, or use public networks to make services inside the virtual machine accessible.

## Use Cases
