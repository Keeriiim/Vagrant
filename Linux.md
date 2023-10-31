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
- **ls -Option** Display any of the options below by replacing option with any value grepbelow
<img width="491" alt="image" src="https://github.com/Keeriiim/Vagrant/assets/117115289/95c85cd6-06df-45d5-8ab1-2de7729e1cd5">

## Filetypes & Permissions  
There are in total 10 characters that can be assigned a value. First is the filetype, the rest are permissions for the specific directory/file/etc.
Links are pointers, meaning the permission is shown for the link and not the actual file it points to.
- Type ls -l to see filetype in current directory  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/f27ea53c-60b2-4d89-bde3-76e4ad309611)
- lrwxrwxrwx, The first letter 'l' represents the filetype  
<img width="647" alt="image" src="https://github.com/Keeriiim/Vagrant/assets/117115289/dd55fed5-2ef2-4c62-8e86-cdae0c44180a">

- The next 3 rwx means the user (root), can read, write and execute commands  
- The next 3 means the user group user (root) can read, write and execute commands  
- The next 3 means other users can read, write and execute commands  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/b77d931f-aa01-4e62-af72-7ea7825f6726)  





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
- **Id username** shows info about the user

 ## Groups
 - **cat /etc/group** Shows all created groups
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/8f571286-a289-42c8-a810-a553b3af89f8)
- **vagrant** Username
- **:x** The link to shadowfile, which hold the password encrypted
- **:1000** GroupID

**Create an User**
You need to be in root to create users and groups.
- **useradd test** Adds an user named test
- **groupadd testgroup** Adds a group named testgroup

## Add an user to a group  
There are two ways:  
1. **vim /etc/group** Find the group you want to add users and add them manually  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/d0765252-94d6-4c7e-984b-73ff5516d2a3)

2. **usermod -aG testgroup test** Adds the user test directly to the testgroup

**Add/change password and login to new user**
- **passwd test** Adds/changes the password for the user test
- **su - test** Logs in as the user test (only root will not need to know any password to log in)
- **exit** Logout from user
- **userdel -r test** Deletes test user and its home directory
- **groupdel -r testgroup** Deletes test group

**Useful commands**
- **last** Shows history of latest logins
- **who** Shows current user
- **lsof -u test** Lists all opened files by the user, the user needs to be logged in (yum install lsof -y)

## Ownership
- **ls -ld /root/devops** Shows the permissions of a directory
- **chown test:testgroup file.txt** Changes the owner of file.txt to test and group to testgroup
- **chmod o-r /opt/devops** Removes the right for others to read to that directory (w for write,  )
- **chmod g+w /opt/devops** Adds the right for others to write in the directoryls  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/4f9059db-5675-4bec-8a3d-ae4f2a121596)  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/923885ee-bcf6-4fd2-9542-bf70edc63fe2)  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/9589857b-6c45-41e8-9b4b-737872f1f603)












