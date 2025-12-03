Introduction Of Linux

What is an Operating System?

An Operating System (OS) acts as a manager or intermediary between a computer's hardware (CPU, memory, storage) and the software (applications). It ensures smooth coordination between all components.

Key Responsibilities of an OS

    Resource Management: Allocates CPU time, memory, and disk usage.
    Process Management: Controls running programs, starting/stopping them, and assigning resources.
    Memory Management: Handles RAM usage so multiple applications can run without crashing.
    User/Group Management: Manages user accounts, permissions, and access to files and commands.

OS Comparison
| OS      | Focus       | Strengths                                                | Weaknesses                   |
| ------- | ----------- | -------------------------------------------------------- | ---------------------------- |
| Windows | GUI-focused | Easy to use, widely supported software                   | Less secure, resource-heavy  |
| Linux   | CLI-focused | Secure (least privilege), lightweight, ideal for servers | Steeper learning curve       |
| Mac     | Hybrid      | Good GUI + Unix-like security                            | Expensive, less customizable |


Simple example: Think of the OS as a restaurant manager: it organizes chefs (hardware) and recipes (software), ensures the kitchen runs efficiently, and makes sure everyone gets what they need without chaos.
Linux Architecture

Linux has a layered structure that separates system responsibilities for better performance and control.

Layers of Linux Architecture
1. Hardware Layer
    Contains the physical components of the computer: CPU, Memory, Storage, Network Devices.The Linux system interacts with this layer using device drivers.

2. Kernel Layer (Core)

    The kernel is the heart/brain of Linux.
    Responsibilities:
        Process management
        Memory management
        Device management
    Handling system calls (communication between user programs and hardware)

3. System Call Interface (API Layer)

    Provides APIs/functions that programs use to request kernel services.

    Examples:

        Reading/writing files
        Creating or ending processes

4. Shell / Command Interpreter

    Acts as a communication bridge between users and the kernel.
    You enter commands, and the shell interprets and sends them to the kernel.
    
        Examples of shells:
            Bash
            Zsh
            Fish

5. User Space / Application Layer

    Contains all programs and applications users interact with (browsers, editors, games, etc.).These programs use shell + system calls to access system resources.

Boot Process

1. BIOS/UEFI
    When you turn on the computer, the BIOS (older systems) or UEFI (newer systems) performs a Power-On Self Test (POST) to check hardware like CPU, RAM, keyboard, and drives.
2. Bootloader (GRUB2)
    The bootloader (usually GRUB2) loads the Linux kernel into memory and initializes a temporary RAM filesystem.
3. Kernel Initialization
    The Linux kernel decompresses itself, sets up memory management, process scheduling, and mounts the root filesystem (/).
4. Init System (systemd)
    The systemd process starts as PID 1 (the first process) and becomes responsible for launching all other processes and services.
5. System Services
    systemd launches essential background services (like networking, logging, database services, GUI if applicable).
6. Login Prompt
    Finally, the system presents a login prompt (text-based or graphical), allowing the user to log in and start using the system.

 Simple Example to Understand the Linux Boot Process – Restaurant Analogy
   - BIOS/UEFI → Checking the Restaurant: The manager inspects the kitchen, tables, and equipment to make sure everything works.
   - Bootloader (GRUB2) → Unpacking Ingredients: The chef opens the delivery boxes and decides what to cook first (loads the kernel).
   - Kernel Initialization → Setting Up the Kitchen: The chef arranges the tools, stove, and counters so cooking can begin (memory and process setup).
   - Init System (systemd) → Assigning Staff Tasks: The manager tells the waiters, cooks, and cleaners what to do and when (starting system processes).
   - System Services → Opening the Restaurant: Lights, ovens, and music start; everything is ready for customers (networking, printing, background services).
   - Login Prompt → First Customer Arrives: The doors open, and the first customer walks in (user can log in and use the system).

Linux As File System
    Linux is often described as a "Linux as a File System" because everything in Linux is treated as a file—not just documents or images, but also devices, hardware, and even processes.
1. Everything is a file
    Hard drives, USBs, keyboards, network connections → all are represented as files.
   
            Example: /dev/sda → represents a hard drive
            /dev/ttyUSB0 → represents a USB device
   
2. Unified Directory Tree
    Linux has a single hierarchical directory structure (rooted at /).Devices, system info, and actual data all appear in this same tree.

        Example: /etc (configuration), /home (user files), /proc (process info), /dev (devices)
3. File Permissions Control Everything
    Linux uses permissions on files to manage access to users, groups, and processes.This makes the OS secure and organized.
4. Interaction via Files
    Programs interact with hardware and other resources as if they are reading/writing files.

        Example: Writing to /dev/sda writes data to a hard disk, reading /proc/cpuinfo gives CPU information.
This is why Linux is often called a file-system-oriented OS—because files are the core abstraction for everything in the system.

Linux File Types

    | Type            | Symbol | Description                                  | Example                                     | Purpose                                                         |
|-----------------|--------|----------------------------------------------|---------------------------------------------|-----------------------------------------------------------------|
| Regular File    | -      | Normal data file (text, code, images, etc.)  | /home/user/report.txt                       | Store documents, scripts, or data                               |
| Directory       | d      | Folder containing files                      | /etc                                        | Organize files and subfolders                                   |
| Symbolic Link   | l      | Shortcut/alias to another file               | /usr/bin/python -> /usr/bin/python3.11      | Access files from multiple paths without duplication            |
| Character Device| c      | Device that handles data character by character | /dev/ttyS0 (serial port)                    | Read/write one character at a time to devices like keyboards or mice |
| Block Device    | b      | Device that handles data in blocks           | /dev/sda1 (hard drive partition)            | Efficient storage I/O, reads/writes large chunks of data        |
| Socket          | s      | Endpoint for IPC communication               | /var/run/docker.sock                        | Allow programs to communicate locally or over the network       |
| Pipe            | p      | Channel for communication between processes  | /tmp/mypipe                                 | One process writes data, another reads it                       |


IMPORTANT DIRECTORIES

| Directory | Description | Purpose | Examples |
|----------|-------------|----------|----------|
| /bin | Essential system binaries | Contains core commands required for basic system operation | ls, cp, cat, /bin/bash |
| /boot | Boot loader and kernel files | Required to boot the operating system | Kernel, initramfs, GRUB config |
| /dev | Device files | Interface to hardware and virtual devices | /dev/sda, /dev/null, /dev/tty |
| /etc | System configuration files | Stores system-wide service and system configs | /etc/nginx/, /etc/ssh/, /etc/systemd/ |
| /home | User home directories | Stores personal data for each user | /home/user1/, /home/user2/ |
| /lib | Shared libraries | Required by binaries and programs for execution | /lib/x86_64-linux-gnu/ |
| /media | Removable media mount | Auto-mounts USB, CD/DVD devices | /media/myusb |
| /mnt | Temporary mount point | Used for manual temporary filesystem mounting | /mnt/data |
| /opt | Optional third-party software | Stores external applications not managed by package manager | /opt/docker/ |
| /proc | Virtual kernel and process info | Provides runtime system details | /proc/cpuinfo, /proc/meminfo, /proc/uptime |
| /var | Variable files | Contains logs, cache, dynamic data | /var/log/, /var/cache/ |
| /usr | User applications & utilities | Non-essential binaries, libraries, docs | /usr/bin/, /usr/lib/ |
| /tmp | Temporary files | Used for temporary runtime storage | /tmp/ |
| /root | Root user's home directory | Home directory for system administrator | /root/ |
| /run | Runtime data | Temporary filesystem cleared on reboot | /run/ |
| /sbin | System binaries for admin | System management commands | ifconfig, reboot, mount, fsck |
| /srv | Service data | Files served by system services | /srv/www/, /srv/ftp/, /srv/mysql/ |
| /sys | Kernel and hardware interface | Real-time kernel information virtual filesystem | /sys/* |

#Example: Think of /sys like a control panel for your computer's hardware.

INODE
# INODE

An inode is a data structure on a Linux filesystem that stores everything about a file except its name.  
Each file has its own unique inode.

## What an inode contains:
- File type
- User (UID)
- Group (GID)
- Permissions (rwx)
- Timestamps (created, modified, accessed)
- File size
- Number of hard links
- Pointers to actual data blocks on disk

## Command to view inode details:

Command to see inode details:

    stat <filename>
Output example:

    stat demo
    File: demo
    Size: 0
    Blocks: 0
    Device: 37h/55d Inode: 7376
    Links: 1
    Access：（0644/-rw-r--r--）
    Access: 2025-12-02 05:19:55.966367276 +0000
    Modify: 2025-12-02 05:19:55.966367276 +0000
    Change: 2025-12-02 05:19:55.966367276 +0000
    Birth: 2025-12-02 05:19:55.966367276 +0000
    
Inode Exhaustion

Inode exhaustion happens when you run out of inodes, even though your disk still has free space. Each file, folder, and symbolic link consumes one inode, and inodes are finite.

How to detect inode exhaustion:
Check overall inode usage:
Find which directory is consuming all the inodes:
To fix the issue:
    Delete old files: Clean up old logs, caches, or temp files
    Set up log rotation using logrotate
    Clean package manager caches (apt clean or yum clean)
    Clean Docker containers: docker system prune -af
    Last resort: Recreate the filesystem with more inodes
    

Hard Link
    - Points directly to the same inode as the original file
    - Both file names share the same data
    - If you delete one, the file still exists
Create hard link:

    ln <original_file> <new_file>

    ln demo.txt backup.txt

Soft Link (Symbolic Link)
    - Points to the path of another file (like a shortcut)
    - If the original file is deleted, the soft link becomes broken
Create soft link:

    ln -s <original_file> <new_file>

# Comparison Table: Hard Link vs Soft Link

| Feature | Hard Link | Soft Link (Symbolic Link) |
|--------|-----------|---------------------------|
| Points to | Inode of original file | Path of original file |
| Inode number | Same as original file | Different |
| Works after original file is deleted? | Yes | No (becomes broken) |
| Can link directories? | No | Yes |
| Works across different filesystems? | No | Yes |
| File content shared? | Yes (same data blocks) | No (only a pointer) |
| File type shown as | Regular file | Link (`ls -l` shows `l`) |
| Size | Same as file | Size = length of path |
| Command to create | `ln file1 file2` | `ln -s file1 file2` |

Linux Commands
Navigation Commands
pwd (Print Working Directory)
Displays the absolute path of the current working directory.
pwd
# Output: /root
cd (Change Directory)
Allows you to change the current working directory.
cd <directory_name>
cd ..       # Go back to previous directory level
cd ~        # Go to home directory
cd -        # Go back to previous directory
cd $HOME    # Go to home directory
ls (List)
Lists files and directories in the current directory.
ls
ls ..           # List parent directory files
ls -a           # List all files (including hidden)
ls -l           # List with detailed information
ls -ltu         # List latest modified files at top
ls -ltc         # List by permission modification time
ls -s           # List sorted alphabetically
ls -al --author # List with author username
tree
Shows tree level view of directories and files.
tree
File Operations
mkdir - Create Directory
mkdir <directory_name>
mkdir -p /path/to/file  # Create parent directories if needed
touch - Create File
touch <filename>
cat - Show File Content
cat <file_name>
cp - Copy Files
cp <source> <destination>
mv - Move/Rename Files
mv <source> <destination>
rm - Remove Files
rm <filename>
rmdir - Remove Empty Directory
rmdir <directory_name>
Search & Filter
grep - Search Text Inside Files
grep "error" /var/log/syslog
grep -i "failed" auth.log       # Search ignoring case
grep -r "nginx" /etc            # Search recursively
find - Find Files
find / -name <filename>
find /var/log -name "*.log"
find /tmp -type f -mtime +7 -delete  # Delete files older than 7 days
sed - Stream Editor
sed 's/old text/new text/' file.txt      # Substitute text
sed 's/banana/BANANA/g' fruits.txt       # Replace all occurrences
sed '2d' file.txt                        # Delete line 2
sed 's/^/Line: /' file.txt              # Add prefix to each line
sed '/^$/d' data.txt                    # Delete empty lines
cut - Extract Columns
cut -d " " -f1 file.txt     # First field with space delimiter
echo "abcdef" | cut -c 1-3  # Extract characters 1-3
cut -b 1-4 filename.txt     # Extract first 4 bytes
sort - Sort Lines
sort -n file.txt  # Sort numerically
sort -r file.txt  # Sort in reverse
sort -u file.txt  # Remove duplicates
uniq - Filter Duplicate Lines
uniq file.txt     # Remove consecutive duplicates
uniq -c file.txt  # Count occurrences
uniq -d file.txt  # Show only duplicated lines
uniq -u file.txt  # Show only unique lines
Permissions
chmod - Change File Permissions
Permissions are defined for three categories:
Owner (user who owns the file)
Group (users in the file's group)
Others (everyone else)
Symbolic Mode:
r → Read (4)
w → Write (2)
x → Execute (1)
+ → Add permission
- → Remove permission
= → Set exact permissions
chmod u+x file.txt      # Give owner execute permission
chmod g-w file.txt      # Remove write permission for group
chmod o+r file.txt      # Give others read permission
chmod a-x file.txt      # Remove execute for everyone
chmod u=rw,g=r,o=r file # Set specific permissions
Numeric Mode:
chmod 755 file.txt  # rwxr-xr-x
chmod 644 file.txt  # rw-r--r--
chown - Change Owner and Group
chown user1 file.txt           # Change owner to user1
chown user1:admin file.txt     # Change owner and group
chown :admin file.txt          # Change group only
chgrp - Change Group
chgrp developers file.txt
chgrp -R developers /path/to/directory  # Recursive
System Information
who - Show Logged Users
who
who | cut -d' ' -f1 | sort | uniq  # Count unique users
df - Disk Free Space
df -h  # Human-readable format
du - Disk Usage
du -sh  # Total for current directory
uname - System Information
uname -a  # All system information
uname -s  # Kernel name
uname -r  # Kernel version
uname -m  # Hardware architecture
Pipe & Redirection
Pipe (|)
Sends output of one command as input to another:
ls -l | grep "txt"
Output Redirection
> - Redirect output to file (overwrite)
>> - Redirect output to file (append)
< - Redirect input from file
echo "Hello" > output.txt      # Overwrite
echo "World" >> output.txt     # Append
wc -l < input.txt              # Count lines from file
Error Redirection
2> - Redirect stderr
&> - Redirect both stdout and stderr
2>&1 - Redirect stderr to stdout
ls non_existent 2> error.log       # Redirect errors
ls file1 file2 &> all_output.txt   # Redirect all output
command 2> /dev/null               # Discard errors
Regular Expressions (Regexp)
Regular expressions are patterns used to match text. Commonly used with grep, sed, awk.
Wildcards
. - Matches any single character
* - Matches zero or more of preceding character
[ ] - Matches any character in brackets
grep 'c.t' animals.txt          # cat, cut, cot, etc.
grep '[aeiou]' file.txt         # Lines with vowels
grep 'd*g' animals.txt          # dg, dog, doog, etc.
Anchors
^ - Beginning of line
$ - End of line
grep '^d' animals.txt   # Lines starting with 'd'
grep 'fish$' file.txt   # Lines ending with 'fish'
Combining Patterns
grep 'cat\|dog' animals.txt     # Match cat OR dog
AWK - Text Processing
awk '/pattern/' file.txt                    # Print matching lines
awk '{print $1}' data.txt                   # Print first field
awk '$2 ~ /apple/ {print}' data.txt        # Match field 2
awk '/^o/' data.txt                        # Lines starting with 'o'
awk '/e$/' data.txt                        # Lines ending with 'e'
awk '/sweet|orange/' data.txt              # Multiple patterns
Zombie Process
A zombie process is a process that has finished running but remains in the process table because its parent process hasn't collected its exit status.
Check for zombies:
ps aux | grep Z

Terminating Zombie Process
Find zombie process:
Find parent PID:
Kill parent process:
This document provides a comprehensive introduction to Linux, covering fundamental concepts, architecture, file system, important directories, and essential commands for system administration and daily use.
kill -9 <parent_pid>
ps -o ppid= -p <zombie_pid>
ps aux | grep defunct

df -i
 
 
 
 
