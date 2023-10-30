# Linux Training

1. Go to your folder where you have the vagrantfile
2. **vagrant up** Start the VM  
3. **vagrant ssh** Log into the VM  
4. **sudo yum install vim -y** Download Vim    

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
**rm -rf dir** Deletes a dir with all it's content  
**cp a b/** Copies file into directory/map b  
**cp -r dev ops/** Copies dev directory into ops  
**mv a b/** Moves file/directory  a into directory/map b  
**mv a.txt b.txt** Moves/replaces the name a to b  
**mv "*"** Moves everything in the dir  
**mv "*".txt** Moves all .txt files  
**History** See all prompted commands  
**cat /etc/os-release** Shows the OS    
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/174d8d21-3ca3-472e-883e-55f0b3c13b04)

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

# Linux continues
## Command List
- **ls -Option** Displays the Options below
<img width="491" alt="image" src="https://github.com/Keeriiim/Vagrant/assets/117115289/95c85cd6-06df-45d5-8ab1-2de7729e1cd5">

## Filetypes
- Type ls -l to see filetype in current directory
Xrwxr-xr-x. The first letter 'X' represents the filetype
<img width="647" alt="image" src="https://github.com/Keeriiim/Vagrant/assets/117115289/dd55fed5-2ef2-4c62-8e86-cdae0c44180a">

## Links
- Type ln -s + full path + shortcut name
<img width="622" alt="image" src="https://github.com/Keeriiim/Vagrant/assets/117115289/f0d9d778-0aac-4211-b595-f26065fda6fb">  

- If the file is missing
<img width="634" alt="image" src="https://github.com/Keeriiim/Vagrant/assets/117115289/38270cae-6379-4cb0-bd8f-309ea5542f44">  

- Remove the link with unlink + linkName
<img width="554" alt="image" src="https://github.com/Keeriiim/Vagrant/assets/117115289/897c0a0d-0c18-4bdd-ba64-00ac22767e0d">

## Filters
If you need to look for a config to change, grep is useful for findning it. Grep is using input redirection.  
- **grep hello file.txt** is the same thing as grep hello < file.txt
- **grep -i** removes upper/lower case
- **grep -R** used to search through directory
- **grep -v** "show everything except" 
- **star** means search all  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/eb931ae2-8714-4ed8-8a05-8224d2c513af)

- **less file** Less is a reader that shows you the content of the file, you can move up/down with the arrows and you can use /word to search for a word in the reader
- **more file** Same as less but move down with enter, use q to quit
- **head -20 file** shows the first 20 lines in a file 
- **tail -20 file** shows the last 20 lines in a file
- **tail -f file** show the last rows with a dynamic update, good for troubleshooting server errors, you can track the log files, use one to track, another window to run commmands, ctrl + c to quit

### Filter training
- **cat /etc/passwd** Shows all users, rows are separated by :
- **cut -d: -f1 /etc/passwd** Shows column one, f3 = userid, f4 = groupid  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/986c13cb-5dde-479f-841c-e81ba53acd2a)


 Cut only works with intelligent filters, else you have to use awk
- **awk -F':' '{print $1}' /etc/passwd  

Bonus
- **sed 's/firstWord/secondWord/g' file.txt** Shows what the replace of the firstWord with the secondWord will look like
- **sed -i 's/firstWord/secondWord/g' file.txt** Replaces the firstWord with the second
Or you can use vim
- **vim txtfile.txt** **%s/firstword/secondword/gg**
- **%s/firstword//g** replaces the words with null


#Redirection ( > and >> )
##Append / Overwrite
- **echo "hello" > file.txt** Overwrites the content of the file with hello
- **echo "hello" >> file.txt** Appends the content of the file with hello  

An easy way of clearing the text on an entire file is to overwrite it with null. There is a null we can use at /dev/null
- **cat /dev/null > /tmp/file.txt**

## Outputs
- **free -m 1>> /tmp/error.log** 1 is the default output, if the code succeeds it will redirect it to the file  
- **free -m 2>> /tmp/error.log** 2 is for logging errors.
- **free -m &>> /tmp/error.log** & is used for all  

## Inputs  
- **wc -l /etc/passwd** This will count the number of lines in the path  
- **wc -l < /etc/passwd** This will works also  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/285228ea-2f71-4b9a-9fd6-9fe0a2143f27)

## Piping
Piping means that the output of something will go as an input for something  
- **ls | wc -l** Counts all maps in the folder 
- **ls | grep host** Prints all files named with host
- **find / -name host'star'** Goes through all directories and looks for the name host

# Users and Groups
Every file in the system is owned by an user with an unique ID, and associated with a group  
Every process has an owner and group affiliation, and can only access the resources its owner or group can access 
User name & password is stored in /etc/passwd  
Users have an assigned homedirectory and a program that run when they login, usually a shell  
Users cannot read, write or execute each others files without permission  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/a0f5c935-6344-4ce8-8734-10979e0e0cc4)  

![image](https://github.com/Keeriiim/Vagrant/assets/117115289/1148daa2-f8ef-4e47-8eaf-2c176b356acc)  
- **root** Username
- **x** The link to shadowfile, which hold the password encrypted
- **0:0** UserID, GroupID
- **root** Comment
- **/root** Homedirectory
- **/bin/bash** Login Shell

 ## Groups
 - **cat /etc/group** Shows all created groups






