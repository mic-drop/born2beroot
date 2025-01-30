# Whar are we doing?
- Setting up a remote server using a virtual machine

What is a virtual machine?
- Is a software digitally emulating a compter hardware

Why?
- So we can emulate two computers comunicating through a network

What is VirtualBox?
- A virtual machine factory with costumable setings

## Rules
### 1- At least 2 Encrypted partions
### 2 - AppArmor must be running at startup
### 3 - Leave only port 4242 open in your virtual machine 
### 4 - Your firewall must be active when you launch your VM
### 5 - hostname musst be loggin ending with 42
### 6 - You will have to modify it during evauation
### 7 - Implement strong password policy rules
### 8 - Implement Sudo with rules
### 9 - In addition too root user, must have a user with your username
### 10 - This user has to belong to user42 and sudo groups
### 11 - During defense, you have to create a new user and assign it to a group

## Password Rules
	#1 Has to expire every 30 days
	#2 Minimum number of days allowed before alter pass is 2 days
	#3 User has to recieve a message 7 days before expiration
	#4.1 - 10 Char Long
	#4.2 - Upper, Lower and Number
	#4.3 - No 3 consecutive chars
	#4.4 - Not include name of the user
	#4.5 - New password must have at least 7 char different from prior pw
	#4.6 - root must follow all rules except 4.5

## Sudo Rules
	#1 sudo auht must be limited to 3 attemps of incorrect pw
	#2 A custom message must occur if wrong pass used as sudo
	#3 sudo i/o must be logged at /var/log/sudo/
	#4 TTY mode has to be enable
		- Enable the requiretty option: In the sudoers file, find the line that contains Defaults and add the following:
	#5 These path must be restricted to sudo
	/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin

## Script Rules
	#1 Must be in bash
	#2 Must be launch at startup
	#3 Broadcast output to every terminal every 10 minutes
	#4 No error must be visible
	#5 Info to be displayed
		- OS architecture & Kernel version
		- number of physical processors
		- number of virtual processors
		- RAM availabitlity and utilization percentage
		- Storage availability & util as percentage
		- Processors util as percentage
		- Date & Time of last reboot
		- Wether LVM is active or not
		- Number of active connections
		- Number of users connected
		- IPv4 & MAC Address
		- number of commands executed with sudo


## Commands to check requirements
	# OS name
	`head -n 2 /etc/os-release`

	# AppArmor loaded
	/usr/sbin/aa-status

	# Check Established Ports
	ss -tunlp

	# Check ufw status
	/usr/sbin/ufw status	

	# Check LVM Partitions
	lsblk

## Glossary

- Virtual Machine
	- Software imitating a physcical machine
 - Partitions
	- Logical division of a physical storage
- Debian vs Rocky
	- Debian and Rocky are Linux distros
- Why Debian?
	- Very Stable & Securre
	- Lightweight : install necessary packages only
	- Extensive repositores

- Operating System
	- A softwar to run other software
- AppArmour
	- Linux Security Model that enforces mandatory access control over computer resources
	- It limits which processes can access which filesr, directories, ports, shared memory and IO devices

- SELinux
	- Linux Security Model more complex to configure than AppArmor

- Apt vs Apitude
	- Both are package managers for Debian
	- Apt is lightweight and faster compared to Aptitude since it doesn’t have a text-based user interface.

- FireWall
	- Hard or software that monitors incoming and outgoing network trafic based on predefined security rules

- UFW
	- A fire wall rules manager. usually included by default in Debian systems

- TTY
	- refers to the terminal, software capable of showing output and collecting input
- Kernel
- Cron
	
- OS Architecture
- Physical Processor
- Virtual Processor
- RAM
- IPv4
- Port
- MAC address

# Questions
	Why 2 partitions?
	- To seperate user data from OS essential files

	Why use LVM?
	- To easely simulate another machine

## Configuration files

### SSH config file
/etc/ssh/sshd_config
/etc/ssh/ssh_config (different files)

### Passowrd Security Libpam
/etc/pam.d/common-password

### Password expirations
/etc/login.defs

### Logs
/var/log/sudo/sudo.log

### Config Suduoers group
/etc/sudoers

### Script
/usr/lcal/bin/

### Cron Configuration
sudo crontab -u root -e
