# Table of contents

- [Table of contents](#table-of-contents)
    - [System information](#system-information)
    - [USER INFORMATION AND MANAGEMENT](#user-information-and-management)
    - [FILE AND DIRECTORY COMMANDS](#file-and-directory-commands)
    - [Directory navigation](#directory-navigation)
    - [FILE PERMISSIONS](#file-permissions)
    - [NETWORKING](#networking)
    - [Installing and updating things](#installing-and-updating-things)
    - [SEARCH](#search)

### System information

```shell
uptime # Show how long the system has been running + load
host # Show system host name
hostname -I # Show system host name
date # Show the current date and time
whoami # Who you are logged in as
man # help for commands
su # switch user 
``` 

### USER INFORMATION AND MANAGEMENT

```shell
id # Display the user and group ids of your current user.
groupadd test # Create a group named "test".

useradd -c "John Smith" -m john # Create an account named john, with a comment of "John Smith" and create the user's home directory.
userdel john # Delete the john account.
passwd # password input for user 
```
### FILE AND DIRECTORY COMMANDS

```shell
ls -al # List all files in a long listing (detailed) format
pwd # List all files in a long listing (detailed) format
mkdir directory # Create a directory
rm file # Remove (delete) file
rm -r directory # Remove the directory and its contents recursively
cp file1 file2 # Copy file1 to file2
mv file1 file2 # Rename or move file1 to file2. If file2 is an existing directory, move file1 into directory file2
ln -s /path/to/file linkname # Create symbolic link to linkname
touch file # Create an empty file or update the access and modification times of file.
cat file # View the contents of the file
less file # Browse through a text file
head file # Display the first 10 lines of a file
tail file # Display the last 10 lines of a file
echo "What" > where # typing and moving to file, also rewriting 
echo "What" >> where # typing and moving to file with adding text not rewriting
nano what # terminal text editor
vi what # terminal text eitor 
gedit what # GUI editor
updatedb # updating terminal database
```

### Directory navigation
```shell
cd .. #go to one level up
cd  # Go to the $HOME directory
cd /etc # Change to the /etc directory
```

###  FILE PERMISSIONS

```shell
 U   G   W
rwx rwx rwx     chmod 777 filename
rwx rwx r-x     chmod 775 filename
rwx r-x r-x     chmod 755 filename
rw- rw- r--     chmod 664 filename
rw- r-- r--     chmod 644 filename
```

### NETWORKING

```shell
ifconfig -a # Display all network interfaces and ip address
ping host # Send ICMP echo request to host
whois domain # Display whois information for domain
dig domain # Display DNS information for domain
dig -x IP_ADDRESS # Reverse lookup of IP_ADDRESS
host domain # Display DNS ip address for domain
hostname -i # Display the network address of the host name.
hostname -I # Display all local ip addresses
wget http://domain.com/file # Download http://domain.com/file
netstat -nutlp # Display listening tcp and udp ports and corresponding programs
arp –a # IP addresses and max addresses
netstat –ano # active connections on machine
route # where traffic exits
```

### Installing and updating things

```shell
apt update && apt upgrade  #update whole system
apt install python-pip # installing python
python -m SimpleHTTPServer 8080 # apache start
systemctl enable potgresql  # Keep online 
```

### SEARCH

```shell
grep pattern file # Search for pattern in file
grep -r pattern directory # Search recursively for pattern in directory
locate name # Find files and directories by name
find /home/john -name 'prefix*' # Find files in /home/john that start with "prefix".
find /home -size +100M # Find files larger than 100MB in /home
```


