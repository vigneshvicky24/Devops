# SYSTEM ADMINISTRATOR

## sudo – Super User Do
- The special key is `sudo`, which temporarily grants you permission to perform an action that requires elevated privileges.

### Feature Comparison Table

    | Feature            | root       | sudo                       |
    |-------------------|------------|----------------------------|
    | Is it a user?      | Yes        | No (it's a command)        |
    | Unlimited power?   | Yes        | Yes, but temporarily       |
    | Security           | Risky      | Safer                      |
    | Logging of actions | No         | Yes                        |
    | Can be restricted? | No         | Yes (sudoers file)         |
    | Typical use        | System admin | Regular users doing admin tasks |

## SSH Key-Based Authentication

SSH (Secure Shell) is a secure way to connect to another computer over a network.

### How SSH Works (Simple Explanation)

SSH uses two keys:

- 🔐 **Private Key** – stays on your computer  
- 🔓 **Public Key** – you upload it to server / cloud / GitHub / Azure DevOps

When you connect:

1. Server checks your public key.
2. Server sends a challenge that only your private key can answer.
3. If the answer matches → **You are authenticated (logged in).**
4. **Password is NOT required.**

> **Private key must never be shared.**  
> **Public key can be shared with anyone.**

1.To create the SSH key;

	  ssh-keygen -t rsa -b 4096 -C "name@gmail.com

    ssh-keygen -t rsa -b 4096 -C "name@gmail.com
    |           |  |      |        └── comment (email/identifier)   
    |           |  |      |
    |           |  |      └── bit size (key strength)
    |           |  |       
    |           |  |
    |           |  |
    |           |  └── algorithm type
    |           └── type of key to create 
    |
    └── type of key to create

2. It asks a file location  
3. It asks for a passphrase (optional)

File Paths:
  /.ssh/id_rsa.pub # public key
  /.ssh/id_rsa # private key


## How to Add SSH Key to Azure DevOps

1. Go to **Azure DevOps → Top right User Settings**
2. Click **SSH Public Keys**
3. Click **Add Key**
4. Paste the content of the **public key** there → **Save**

NOTE:with this ssh authentication ,no password is needed

###FLOW OF SSH AUTHENTICATES:

    Client (your laptop)        Server (Azure/Git/VM)
    --------------------------------------------------------
    1.Sends request          --->    Checks if your PUBLIC key exists
    2.Server sends challenge <--- Needs private key to decode
    3.Client uses PRIVATE key to reply
    4.Server confirms match  --->  Access granted (login success)

# USER AND GROUP MANAGEMENT

User and group management refers to creating, modifying, and controlling:

### Users  
People or system accounts that can log in.

### Groups  
Collections of users who share permissions.

### Permissions  
What a user/group can read (r-4), write (w-3), or execute (x-1).

---

## USERS

![Image](image/image1.png)


###To create the user 

	useradd <username>

###To set the password to the user

	passwd <username>

###To list of user account 

	getent passwd	(or)	cat /etc/passwd

![Image] (images/image2.png)

###To see the created user “ID”

	id <username>

###To delete user account	

	userdel <filename>
---
## GROUP

###To create the group:

    groupadd <group name>

###To add a user to a group:

    usermod -aG <username> <groupname>


![Image](images/image3.png)

###To remove the user from the group:

    gpasswd -d <username> <group name>
###Example:

    gpasswd -d demo1 demogroup1


###To create the user with an associated group:
    
    useradd -u 1550 -g <group-name> -G <secondary names,names> <new user_name>

    # 1550 – it is the user ID
###To delete group
    	
        groupdel <groupname>

###Difference Between primary group & Secondary group

| Feature                  | Primary Group                                                          | Secondary Group                                                     |
|-------------------------|------------------------------------------------------------------------|---------------------------------------------------------------------|
| Number of Groups        | Each user has one primary group                                        | Each user can belong to multiple secondary groups                   |
| Default Group for Files | Files created by the user are assigned to their primary group          | Files created by the user are assigned to their primary group (unless specified otherwise) |
| Group Creation          | Automatically created with the user account (same name as user)        | Can be created independently of users (for access control)          |
| Main Purpose            | Identifies user’s default group; used when user creates files          | Grants access to shared resources (directories, files, etc.)        |
| Modification            | Can be changed using `usermod -g`                                      | Can be changed using `usermod -aG` (to add a user to a group)       |

###Differences between type of Users

| Feature        | Root User                                                     | Regular Users                                                  | Service Users                                                             |
|----------------|--------------------------------------------------------------|----------------------------------------------------------------|---------------------------------------------------------------------------|
| Username       | root                                                         | Custom usernames (e.g., devops, alice)                         | Service-specific usernames (e.g., www-data, postgres)                      |
| UID            | 0                                                            | 1000+                                                          | 1-999 or system-defined low range                                         |
| Purpose        | Full system control, system administration                    | Day-to-day user tasks, access to specific resources            | Running specific services (e.g., web servers, databases)                  |
| Permissions    | Full: Unlimited system control                                | Limited: Access to specific resources and files                | Minimal: Access only to specific directories and files                    |
| Login Access   | Yes, but best avoided in practice                             | Yes (with specific shell)                                      | No login shell (cannot log in)                                            |
| Example Tasks  | System administration (installing software, managing users)   | Running applications, accessing files, working on code         | Running services (e.g., web server, database, cron jobs)                  |
| Usage in DevOps| Rarely used directly (via sudo)                               | Common for CI/CD, deployments, troubleshooting                 | Configuring, managing, and securing application services                  |

###To get into created user 

    	Su - <username>
        
![Image] (/images/image4.png)

---

##PASSWORD MANAGEMENT 

###To set password to user 

    	Passwd <username>

###To change  password forcelly to user 
	
    Passwd -e <username>
###To set password expiry data 
    
    chage -M <days> <username> 	#MAX DAYS
Example: 
    
    chage -M 60 demo1
    chage -m 3 demo1	#minimum days
    chage -W 14 demo1	

###To view password status
	
    chage -I demo1
![Image] (images/image6.png)

---
##FILE PERMISSION AND OWNERSHIP

![Image] (images/image8.png)

###Change the file permission 
Example :

    Chmod 400 <filename.txt>

###To change the directory permission
Example:
    
    Change [permissions] <directory name>
    
![Image] (images/image9.png)

##chown – It is a Linux command used to change the ownership of files and directories.
 
 Syntax: 
    
    chown [options] owner:group file_name
Owner means user who will own the file
Group means group ownership

![Image] (images/image10.png)
---
#PROCESS MANAGEMENT
![Image] (images/image5.png)

What is Process?

Process is the running instance of the program
Example : when work on anything in the computer behind see process is running 
COMMANDS:
1.ps -process status
	
    Ps aux
# a: all users
# u: user-oriented format
# x: include processes without controlling terminal

![Image] (images/image11.png)

Explaination of Output
| Column   | Meaning                                                           |
|----------|-------------------------------------------------------------------|
| USER     | The user who owns the process (root here)                         |
| PID      | Process ID (unique number assigned to process)                    |
| %CPU     | CPU usage percentage                                              |
| %MEM     | Memory usage percentage                                           |
| VSZ      | Virtual memory size in KB used by process                         |
| RSS      | Resident memory (actual RAM) in KB used                           |
| TTY      | Terminal linked to the process (pts/0 means terminal session)     |
| STAT     | Current status of process                                         |
| START    | Time when the process started                                     |
| TIME     | Total CPU time consumed                                           |
| COMMAND  | The command that started the process                              |

To specific process
	
    ps -p <pID>

    ps -ef

![Image] (images/image12.png)

top- To see process,memory used in real time
![Image] (images/image13.png)

1.top - 17:41:12 up 1:55, 0 user, load average: 0.77, 0.43, 0.27
Explaination

    | Part                        | Meaning                                                |
    |-----------------------------|--------------------------------------------------------|
    | 17:41:12                    | Current system time                                    |
    | up 1:55                     | System uptime (1 hour 55 minutes)                      |
    | 0 user                      | Number of logged-in users                              |
    | load average: 0.77, 0.43, 0.27 | System load last 1, 5, 15 mins. (CPU demand)        |

2. Tasks: 4 total, 1 running, 3 sleeping, 0 stopped, 0 zombie
    
        | Item       | Meaning                    |
        |------------|----------------------------|
        | 4 total    | Total processes            |
        | 1 running  | Currently executing on CPU |
        | 3 sleeping | Idle but waiting           |
        
3. %Cpu(s): 0.0 us,  0.0 sy,  0.0 ni, 100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st

        | Field | Meaning                          |
        |-------|----------------------------------|
        | us    | User processes CPU time          |
        | sy    | System/kernel processes time     |
        | ni    | Nice value processes CPU         |
        | id    | Idle time (CPU free)             |
        | wa    | Waiting for I/O                  |
        | hi    | Hardware interrupts              |
        | si    | Software interrupts              |
        | st    | CPU stolen by hypervisor (VM)    |

5. MiB Mem : 7836.2 total, 7136.4 free, 591.6 used, 330.3 buff/cache
     MiB Swap: 1024.0 total, 1024.0 free, 0.0 used. 7244.6 avail Mem

        | Field       | Meaning                          |
        |-------------|----------------------------------|
        | total       | Total RAM installed              |
        | free        | Not used at all                  |
        | used        | Used by programs                 |
        | buff/cache  | Disk buffers + cached files      |
        | avail Mem   | Available without swapping       |
        | swap        | Hard-disk backup memory          |

---
##PROCESS CONTROL

kill – used to stop or terminate processes by sending signals to them.

    kill <pid>	#default  kill signal process
    kill  -9 <pid>	 # forcefully kill the process
    kill -1 <pid>	# Restart /reload configuration 
    kill -STOP <pid> #pause /suspend process
    kill -CONT <pid>  #Resume stopped process
    kill -15 <pid> # gracefully kill process
    killall <process_name> 	#kill all like nginx processes
    pkill  -u <user>	#kill user’s process
    Pkill -f  “python script.sh”	#kill by pattern

jobs - list background and suspended processes in current terminal.It does not change the state
& - run a command in the background
fg – foreground jobs
bg – It is used to resume a stopped job in the background. It changes job state from stopped → running(background).

bg – It is used to resume a stopped job in the background. It changes job state from stopped → running(background)

![Image] (images/image15.png)
 
lsof – List Open Files
It is a command used to view all open files and the processes using them in linux.
To show which files are currently opened by processes in the system.

	
Example:
	![Image] (images/image15.png)

Explaination 

    | Column   | Meaning                                         |
    |----------|-------------------------------------------------|
    | COMMAND  | Name of the process using the file (bash)       |
    | PID      | Process ID (1 in this case)                     |
    | USER     | Owner of the process (root)                     |
    | FD       | File Descriptor (stdin, stdout, memory, etc.)   |
    | TYPE     | File type (DIR, REG, CHR, etc.)                 |
    | DEVICE   | Device number where the file resides            |
    | SIZE/OFF | Size or file offset                             |
    | NODE     | Inode number of the file                        |
    | NAME     | Path of the file opened                         |

lsof -I :80 	#check with process is using port 80
lsof -u username	#files opened by a specificed user
---
##SYSTEMCTL COMMANDS

systemctl start <service_name>	#start service
systemctl status <service_name> 	#check service is running 
systemctl reload <service_name> 	#reload service
systemctl stop <service_name>	#stop service
systemctl enable <service_name> 		#enable at boot
systemctl enable  -–now  <service_name>	#Enable and start immediately
systemctl disable --now <service_name>	#Disable and stop immediately
systemctl mask nginx  	# mask = fully disable the service
systemctl unmask ngnix	#unmask = allow service to start again
#Listing
systemctl list-unit-files 	#to list all installed unit files
systemctl all units
systemctl list-dependencies <service_name>	#show service dependencies

---

##NETWORKING
Computer connect through together exchange the data is network
Internet is a collection of the computer networks.
![Image] (images/image17.png)
---
##CORE NETWORKING 
Ip Address:
	IP address is phone book of internet. we basically remember the domain name and it will point to the computer or server of that IP address .Ip address is for understand for the Ip address.
	It is unique address of the devices on a network
    
![Image] (images/image.png)

Port Number:
Ports tells which applications we are working with. 
A port number is like a specific door on a computer or device that lets data in or out for certain services or applications .It helps organize the flow of information.
Router:
Role of router is direct and manage the traffic between different devices and network.
And also It is the one assign the Ip address to the devices.
It protect the device from network by filtering the bad data.

Packets:
Packets are small chucks of data that through the network to reach their destination.
With help of packets to send the data faster in the network and again combining the packet  to data with help of sequence number to correct order.

How Networking works in Linux?
Simple analogy:
•  Linux connects to network using Wi-Fi or cable (wlan0, eth0).
•  It gets an IP address (like your house address).
•  When you open a website, Linux asks DNS to find its IP.
•  Data is broken into small packets.
•  Packets go to router, then to the internet.
•  Website server sends packets back.
•  Linux collects them and shows the page on your screen.

##Flowchart

    When we type google.com
            ↓
    Linux looks DNS for Google IP
            ↓
    Linux makes packets
            ↓
    Packets go to Router
            ↓
    Router sends to Internet
            ↓
    Google sends packets back
            ↓
    Linux receives & reassembles packets
            ↓
    Website appears on browser
    
To check Ip addr
	
    ip addr
EXPLAINATION 
1: lo: <LOOPBACK,UP,LOWER_UP> 
    inet 127.0.0.1/8
    inet6 ::1/128
2: wlan0: <BROADCAST,MULTICAST,UP,LOWER_UP>
    inet 192.168.1.10/24
    inet6 fe80::abcd:1234:5678/64

3: eth0: <NO-CARRIER,BROADCAST,MULTICAST,UP>
    inet 10.0.0.5/24
    inet6 fe80::9876:abcd:1234/64
    
#loopback mean is a special IP address that allows a computer to send data to itself, effectively creating a virtual network interface.
Explaination of ip addr
    
    | Line/Section              | Meaning (Simple)                                   |
    |---------------------------|----------------------------------------------------|
    | 1: lo                     | Loopback interface (system talks to itself)        |
    | inet 127.0.0.1/8          | IPv4 loopback address (localhost)                  |
    | inet6 ::1/128             | IPv6 loopback address                              |
    | 2: wlan0                  | Wi-Fi network interface                            |
    | <UP,BROADCAST,MULTICAST>  | Interface active and ready to send/receive data    |
    | inet 192.168.1.10/24      | IPv4 address of Wi-Fi on local network             |
    | inet6 fe80::abcd:.../64   | IPv6 address of Wi-Fi                              |
    | 3: eth0                   | Ethernet (wired) interface                         |
    | <NO-CARRIER>              | Cable not connected / no link                      |
    | inet 10.0.0.5/24          | IPv4 address for Ethernet (if connected)           |
    | inet6 fe80::9876:.../64   | IPv6 for Ethernet                                  |

To view interface
It displays network interfaces and their status (without IP addresses).
	
    ip link show
Example:

    #ip addr – phone number on phone
    #ip link show – The phone device details itself 

Output

    1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default 
        link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP mode DEFAULT group default
        link/ether a4:b1:c1:22:33:44 brd ff:ff:ff:ff:ff:ff
    3: wlan0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN mode DEFAULT group default 
        link/ether ab:cd:ef:12:34:56 brd ff:ff:ff:ff:ff:ff
---
##DNS (Domain Name Space):
DNS configuration:

    Cat /etc/resolv.conf

Test DNS:
	#nslookup google.com	#single DNS queries
	#ding google.com	#Detailed DNS query tool

ip route
    It is used to view the routing table in linux.
Example:
    
    ip route
Output:

    default via 192.168.1.1 dev wlan0 proto dhcp metric 600
    192.168.1.0/24 dev wlan0 proto kernel scope link src 192.168.1.10 metric 600

    | Line                                             | Meaning (Simple)                                                                 |
    |--------------------------------------------------|----------------------------------------------------------------------------------|
    | default via 192.168.1.1 dev wlan0                | All internet traffic goes through gateway 192.168.1.1 (router) using Wi-Fi (wlan0) to the internet. |
    | 192.168.1.0/24 dev wlan0 src 192.168.1.10        | Inside Local network 192.168.1.x uses wlan0 and the device’s IP is 192.168.1.10. |


##Ping
    It checks if another computer or website is reachable over a network
Example:
    
    ping www.google.com
output

	64 bytes from 142.250.xxx.xxx: time=22 ms

•  Received reply
•  Connection working
•  Reply came in 22 milliseconds

##Traceroute:
    traceroute is a network tool that shows the path your data takes from your computer to another host (like google.com).
Example

    traceroute google.com
Output:
    
    traceroute google.com
    traceroute to google.com (142.250.183.46), 30 hops max, 60 byte packets
     1  172.17.0.1 (172.17.0.1)  0.039 ms  0.026 ms  0.051 ms
     2  * * *
     3  * * *
     4  * * *
     5  * * *
Explaination
Hop 1 → 100.0.0.1
•	This is your gateway/router
•	Response time is very fast (0.03 ms)
•	Means your local network is reachable
•  Hop 2 → * * *
•	The next router did not reply
•	Could be because of:
o	Firewall blocking ICMP
o	Router not configured to respond
o	Timeout/delay

simple analogy:
Post Office → City Center → Other City → Friend’s Home
---
##LINUX FIREWALL:
The Linux firewall is a set of tools that control the flow of network traffic to and from your system. It filters packets based on predefined rules to secure the system from unwanted access or attacks.
iptables -L lists all the rules in the firewall for controlling network traffic (incoming, outgoing, and forwarded).
	    
        iptables -L
#wget = download files,
#curl = fetch data or interact with servers/APIs.

CURL
    Curl is like a browser without a screen — it fetches data from the internet directly in the terminal.
    
    | Task                  | Example                                      |
    |----------------------|-----------------------------------------------|
    | Download a file      | `curl -O https://example.com/file.zip`        |
    | Save output to file  | `curl https://example.com > file.txt`         |
    | Check website response | `curl -I https://google.com`                |
    | Test API             | `curl https://api.example.com/data`           |


Wget 
Wget is a command-line tool used to download files from the internet.

    | Task                          | Example                                                |
    |------------------------------|---------------------------------------------------------|
    | Download a single file       | `wget https://example.com/file.txt`                     |
    | Download and rename          | `wget -O newname.txt https://example.com/file.txt`      |
    | Download an entire website   | `wget --mirror https://example.com`                     |
    | Resume an interrupted download | `wget -c https://example.com/largefile.iso`           |


SCP
    SCP (Secure Copy) is a Linux command used to copy files or folders between two systems over a network securely using SSH encryption.
Example:
To copy file from local->remote server

    scp file.txt user@remote_ip:/path/to/destination/
Copy file from remote → local
	
    scp user@remote_ip:/path/file.txt /local/path/
Copy a folder (use -r for recursive)
	
    scp -r myfolder/ user@remote_ip:/path/destination/

rsync:
The main use of rsync is to copy and synchronize files/folders efficiently between locations — locally or between two machines.
Used for backup, mirroring, syncing files locally or remotely.

##Difference between cp and rsync

    | Feature                  | cp (copy)                     | rsync                                |
    |--------------------------|------------------------------|---------------------------------------|
    | Copies all files every time | Yes                         | Only copies changed files             |
    | Good for backups         | Not efficient                | Best for backups                      |
    | Transfer over network    | Limited                      | Works over SSH easily                 |
    | Resume interrupted copy  | No                           | Supported                             |
    | Speed                    | Slower for repeated tasks    | Faster (transfer only changes)        |


Example:
Imagine you have a project folder with 10,000 files
You want to backup it daily to another drive or server.
•	If you use cp, it will copy everything again → takes long time
•	If you use rsync, it copies only new or modified files → very fast

Syntax:    
    
    rsync [options] source/ destination/
Example:
1.To local copy (same machine)
    
    rsync -av /home/user/docs/ /home/user/backup/
2.Copy to remote server:
	
    rsync [options] source/ user@remote_host:/path/
Example: rsync -av project/ user@192.168.1.10:/var/www/project/
3.Copy from remote server to local machine
	
    rsync [options] user@remote_host:/path/ destination/
Example:
	
    rsync -av user@192.168.1.10:/var/logs/ /home/user/logs/

        
    | Option   | Meaning                                                     |
    |----------|-------------------------------------------------------------|
    | -a       | Archive mode (preserves permissions, time, etc.)            |
    | -v       | Verbose – shows details while syncing                       |
    | -r       | Recursive – include subfolders (included in -a)             |
    | -P       | Show progress + allow resume                                |
    | -z       | Compress data while transfer over network                   |
    | --delete | Delete files in destination that don't exist in source      |

    
    | Command                     | Description                                         |
    |----------------------------|------------------------------------------------------|
    | sudo apt update            | Refreshes package list from repositories             |
    | sudo apt upgrade           | Upgrades installed packages to newest version        |
    | sudo apt full-upgrade      | Upgrades packages and handles dependencies/removals  |
    | sudo apt install pkg       | Installs a package                                   |
    | sudo apt install pkg1 pkg2 | Installs multiple packages at once                   |
    | sudo apt install pkg=version | Installs a specific package version                |
    | sudo apt remove pkg        | Removes package only (keeps config files)            |
    | sudo apt purge pkg         | Removes package + config files                       |
    | sudo apt autoremove        | Removes unused/leftover dependencies                 |
    | apt search pkg             | Searches for package in repo                         |
    | apt-cache search keyword   | Searches packages using keyword                      |
    | apt show pkg               | Displays package details/info                        |
    | apt-cache show pkg         | Shows package information + metadata                 |
    | apt list --installed       | Lists all installed packages                         |
    | apt list --upgradable      | Shows packages with available updates                |
    | apt download pkg           | Downloads package without installing                 |
    | sudo apt clean             | Removes all cached packages                          |
    | sudo apt autoclean         | Removes outdated cache files                         |
    
    
dpkg - Low-level Package Tool
dpkg (Debian Package) is a low-level package management tool used in Debian-based systems like Ubuntu for installing, removing, and managing .deb packages` manually.

    | Command                      | Short Description                                  | Small Example                        |
    |-----------------------------|---------------------------------------------------|--------------------------------------|
    | sudo dpkg -i package.deb    | Installs a .deb package manually                   | sudo dpkg -i google-chrome.deb       |
    | sudo dpkg -r package-name   | Removes installed package (keeps config)           | sudo dpkg -r nginx                   |
    | dpkg -l                     | Lists all installed packages                       | dpkg -l                              |
    | dpkg -L package             | Shows files installed by the package               | dpkg -L nginx                        |
    | dpkg -S /path/file          | Finds which package owns a specific file           | dpkg -S /usr/sbin/nginx              |
    | sudo apt --fix-broken install | Fixes broken dependencies after dpkg installation | sudo apt --fix-broken install        |
    
YUM/DNF Package Manager

    | Command                                      | Description                                 | Small Example            |
    |----------------------------------------------|--------------------------------------------------|--------------------------|
    | sudo yum update / sudo dnf update            | Updates package lists and upgrades packages      | sudo dnf update          |
    | sudo yum install pkg / sudo dnf install pkg  | Installs a package                               | sudo dnf install nginx   |
    | sudo yum remove pkg / sudo dnf remove pkg    | Removes a package from system                    | sudo yum remove nginx    |
    | yum search pkg / dnf search pkg              | Searches for a package in repo                   | dnf search nginx         |
    | yum info pkg / dnf info pkg                  | Shows package details and version info           | yum info nginx           |
    | yum list installed / dnf list installed      | Lists all installed packages                     | dnf list installed       |
    | sudo yum clean all / sudo dnf clean all      | Cleans package cache                             | sudo dnf clean all       |

---

##SYSTEM MONITORING

1.free – show the memory usage and available memory
![Image] (images/image19.png)

•	Total: Total physical RAM
•	Used: Used RAM
•	Free: Completely unused RAM
•	Shared: Shared memory (tmpfs) or  Memory shared between processes, often used for shared memory segments like /dev/shm.
•	Buff/cache: Disk cache (reclaimable) or RAM used for buffering/caching files to speed up system performance. It can be freed when needed
•	Available: Memory available for applications or Shows how much memory is actually available to new programs, considering cache can be reused.
---
df -disk space
Show disk usage (human-readable)
    
    df -h
Show inodes
    
    df -i
Show specific filesystem type

    df -t ext4
Show specific mount point
    
    df -h /var
Exclude filesystem type

    df -x tmpfs
![Image] (images/image.png)
# overlay is the main filesystem in container environment

# uptime – System Update
Example:
	Uptime		#show uptime and load average

# vmstat – Virtual Memory Statistics
It is a command used in Linux/Unix to monitor the overall system performance such as 
    CPU Usage
    Memory (RAM) usage
    Swap usage
    Disk IO, Processes
    System interrupts & context switches
# Example	
    vmstat
# Update every 2 seconds
	vmstat 2
# 10 samples, 2 seconds apart
	vmstat 2 10
![Image] (images/image21.png)
# Disk statistics
	vmstat -d
# Active/inactive memory
	vmstat -a
![Image] (images/image22.png)

du -Directory Usage
# To size of directory
    du -sh /var/log
# To show all files and directories
	du -ah /var/log
# Sort by size
	du -ah /var/log | sort -rh | head -10
# Show only directories
	du -h -d 1 /var | sort -rh

# I/O Statistics
It is performance monitoring tool in linux used to analyze 
    CPU usage
    Disk I/O (read/write activity)
    Device performance
    Storage bottlenecks.
# Example
	iostat
# Update every 2 second
	iostat -x 2
# Specific device
	iostat -x /dev/sda

# LOGGING Log are stored in the path called “/var/log”

# To view entire log
	Cat /var/log/syslog
# View last 50 lines
	tail -n 50 /var/log/syslog
# Follow multiple logs
	Tail -f /var/log/syslog /var/log/auth.log
# View first 20 lines
	Head -n 20 /var/log/syslog

# Journalclt
It is used to view and analyze system logs collected by systemd-journald in Linux.
It helps you check system events, boot logs, service errors, failures, crashes, warnings, and application logs.
It is used to read system and service logs for debugging, monitoring, and troubleshooting issues in Linux.
# Example:
	Journalctl

Cron – Task Scheduling
![Image] (images/image23.png)

# To edit crontab
	crontab -e
# List crontab
	Crontab -l
# Remove crontab
	Cron -r
# Edit for specific user
	Crontab -u <username> -e
Example:
# Every Wednesday at 10AM
    0 10 * * * /path/to/script.sh
# Multiple times
     0 8,13,19 * * * /path/to/script.sh


