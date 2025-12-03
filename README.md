Introduction Of Linux

What is an Operating System?

The operating system (OS) is like a manager or middleman between your computer’s hardware (CPU, memory, hard drive) and the software (applications you run). It makes sure everything works together smoothly.

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

![Image](images/image1.png)

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

![Image](images/image2.png)

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

![Image](images/image3.png)
    
    # Linux Directory Structure

    | Directory | Description | Purpose | Examples |
    |----------|-------------|----------|----------|
    | /bin     | Essential system binaries            | Core commands required for basic system operation             | ls, cp, cat, /bin/bash |
    | /boot    | Boot loader and kernel files         | Required to boot the operating system                         | Kernel, initramfs, GRUB config |
    | /dev     | Device files                         | Interface to hardware and virtual devices                     | /dev/sda, /dev/null, /dev/tty |
    | /etc     | System configuration files           | System-wide configuration and service configs                 | /etc/nginx/, /etc/ssh/, /etc/systemd/ |
    | /home    | User home directories                | Stores personal data for each user                            | /home/user1/, /home/user2/ |
    | /lib     | Shared libraries                     | Required by binaries/programs for execution                   | /lib/x86_64-linux-gnu/ |
    | /media   | Removable media mount point          | Auto-mounts USB/CD/DVD devices                                | /media/myusb |
    | /mnt     | Temporary mount point                | Manual temporary filesystem mounting                          | /mnt/data |
    | /opt     | Optional third-party software        | External applications not managed by package manager          | /opt/docker/ |
    | /proc    | Virtual kernel/process info          | Runtime system and kernel details                             | /proc/cpuinfo, /proc/meminfo, /proc/uptime |
    | /var     | Variable files                       | Logs, cache, dynamically changing data                        | /var/log/, /var/cache/ |
    | /usr     | User applications & utilities        | Non-essential binaries, libraries, docs                       | /usr/bin/, /usr/lib/ |
    | /tmp     | Temporary files                      | Temporary runtime storage                                     | /tmp/ |
    | /root    | Root admin home directory            | Home directory for system administrator                       | /root/ |
    | /run     | Runtime data                         | Temporary filesystem cleared on reboot                        | /run/ |
    | /sbin    | System binaries for admin            | System management commands                                    | ifconfig, reboot, mount, fsck |
    | /srv     | Service data                         | Files served by system services                               | /srv/www/, /srv/ftp/, /srv/mysql/ |
    | /sys     | Kernel & hardware interface          | Real-time kernel information virtual filesystem               | /sys/* |

#Example: Think of /sys like a control panel for your computer's hardware.

INODE
# INODE
 - An inode is a data structure on a Linux filesystem that stores everything about a file except its name.
 - Each file has one inode.
 - Inode have the metadta of file without the filename and directory path . 
    
## What an inode contains:

- File type
- User (UID)
- Group (GID)
- Permissions (rwx)
- Timestamps (created, modified, accessed)
- File size
- Number of hard links
- Pointers to actual data blocks on disk

 When create file ,inode is automatically assign to the file 

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

 - Inode exhaustion happens when you run out of inodes, even though your disk still has free space. 
 - Inodes are like the "metadata" of files — they store information like file permissions, size, timestamps, and the actual data location on the disk.
 - Each file, folder, and symbolic link on your system consumes one inode, and inodes are finite. 
 - If you have millions of small files, you can exhaust all inodes before you run out of actual disk space.

How to detect inode exhaustion:
  1.Check overall inode usage:

            df -i
2.Find which directory is consuming all the inodes:
            
             du --inodes -x / | sort -n | tail
             
Check overall inode usage:
Find which directory is consuming all the inodes:
To fix the issue:
    -Delete old files: Clean up old logs, caches, or temp files
    -Set up log rotation using logrotate
    -Clean package manager caches (apt clean or yum clean)
    -Clean Docker containers: docker system prune -af
    -Last resort: Recreate the filesystem with more inodes
    

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
To see the link is
        
        ln -i <original file> <new file>
Once it is created the two files different inode number.If original file is deleted,then soft link is broken ,we cannot access the backup file 

#Because soft link points to the path, not the inode.
        Original file gone → link broken.

# Comparison Table: Hard Link vs Soft Link
    
# Hard Link vs Soft Link (Symbolic Link) Comparison

    | Feature                             | Hard Link                     | Soft Link (Symbolic Link)       |
    |-------------------------------------|-------------------------------|----------------------------------|
    | Points to                           | Inode of original file        | Path of original file            |
    | Inode number                        | Same as original file         | Different                        |
    | Works after original file deletion  | Yes                           | No (becomes broken)              |
    | Can link directories                | No                            | Yes                              |
    | Works across different filesystems  | No                            | Yes                              |
    | File content shared                 | Yes (same data blocks)        | No (only a pointer)              |
    | File type shown as                  | Regular file                  | Link (`ls -l` shows `l`)         |
    | Size                                | Same as actual file size      | Size = length of target path     |
    | Command to create                   | `ln file1 file2`               | `ln -s file1 file2`              |

Linux Commands

Navigation Commands
    pwd (Print Working Directory) - Displays the absolute path of the current working directory.
        
        Example:   
            pwd 
            output:
                /root
cd  (change Directory) - Allows you to change the current working directory to another directory
    
    cd (Change Directory)
Allows you to change the current working directory.
    
    cd <directory_name>
    cd ..       # Go back to previous directory level
    cd ~        # Go to home directory
    cd -        # Go back to previous directory
    cd $HOME    # Go to home directory

ls (List) - Lists files and directories in the current directory.
        
        ls
        ls ..           # List parent directory files
        ls -a           # List all files (including hidden)
        ls -l           # List with detailed information
        ls -ltu         # List latest modified files at top
        ls -ltc         # List by permission modification time
        ls -s           # List sorted alphabetically
        ls -al --author # List with author username
        
tree - Shows tree level view of directories and files.
    
    tree
    
File Operations
    
    mkdir - Create Directory
    mkdir <directory_name>
    mkdir -p /path/to/file  # Create parent directories if needed

touch- Create File

    touch <filename>
cat - it show content of the file
        cat <file_name>
    
cp - copy file from one loaction to another location

        cp <src directory_location> <destination_directory _lcoation>

mv - move file from one location to another location

        mv <src directory_location> <destination_directory _lcoation>

rm - to remove the  file 

        rm <filename>
    
rmdir -  to remove the empty directory

        rmdir <filename>
rm - Remove Files

    rm <filename>
    rmdir - Remove Empty Directory
    rmdir <directory_name>

Search & Filter

grep - Search text inside files

    grep - Search Text Inside Files
    grep "error" /var/log/syslog
    grep -i "failed" auth.log       # Search ignoring case
    grep -r "nginx" /etc            # Search recursively

find - Find Files

    find / -name <filename>
    find /var/log -name "*.log"
    find /tmp -type f -mtime +7 -delete  # Delete files older than 7 days
sed - search & replace text inside files without opening file,it edit text automatically

Example:

            sed 's/old text/new text/' <filename>.txt  #s means substitution
            sed's/banana/BANANA/g' fruits.txt   #g means all occurrence of the text
            sed '2d' <filename.txt>     #to delete the two line 
            sed 's/^/Line: /' <filename.txt> #to add the prefix "Line: " to each line in text.txt.
            sed 's/old/new/' file.txt               # Replace first occurrence per line
            sed '1,5d' filename.txt                    # Delete lines 1-5
            sed -n '2p' filename.txt    #print line 2
            sed '3i\New line' filename.txt              # Insert before line 3
            sed '3a\New line' filename.txt              # Append after line 3
            sed '/^$/d' data.txt        #to delete the empty line
            sed 's/\([A-Za-z]*\) \([A-Za-z]*\)/\2 \1/' names.txt    #to swap the colunm word

cut - It is used to extract specific columns or fields from a file or text. cut helps you extract specific columns or characters from text.It just prints the selected parts
    Example:
    
            cut -d " " -f1 file.txt #show first row of the column (d-delimiter(space,colon,comma) ,f-field/column number)
            echo "abcdef" | cut -c 1-3  #show ranges of character   (c- character positions)
                outpu: abc
            cut -b 1-4 filename.txt     #extract first 4 byte of each line

sort - Sort lines alphabetically or numerically

    sort -n file.txt  # Sort numerically
    sort -r file.txt  # Sort in reverse
    sort -u file.txt  # Remove duplicates

uniq - The uniq command in Linux is used to filter out duplicate lines from a file or input.

    uniq file.txt     # Remove consecutive duplicates
    uniq -c file.txt  # Count occurrences
    uniq -d file.txt  # Show only duplicated lines
    uniq -u file.txt  # Show only unique lines

Permissions
 permissions control who can read, write, or execute a file. The three main commands to modify these permissions are:

    chmod: Change file permissions.
    chown: Change file ownership (user and group).
    chgrp: Change the group of a file.
    
    chmod - Change File Permissions

 The chmod command is used to set or modify the permissions of a file or directory. Permissions are defined in three categories:

        Owner (user who owns the file)
        Group (users in the file's group)
        Others (everyone else)

Syntax:
        
        chmod [permission] [file]

Permissions

Permissions are specified using either symbolic mode (letters) or numeric mode (numbers).

        
Symbolic Mode:
    r → Read (4)
    w → Write (2)
    x → Execute (1)
    + → Add permission
    - → Remove permission
    = → Set exact permissions
    
Add execute permission for the user:
        
        chmod u+x filename

remove write permission for the group
        
        chmod g-w filename
    
Set read and write permissions for owner, and read for group and others:
        
        chmod u=rw,g=r,o=r filename
        chmod u+x file.txt   # Give the owner execute permission
        chmod g-w file.txt   # Remove write permission for the group
        chmod o+r file.txt   # Give others read permission
        chmod a-x file.txt   # Remove execute permission for everyone

Numeric Mode:
    
    chmod 755 file.txt  # rwxr-xr-x
    chmod 644 file.txt  # rw-r--r--
    chown - Change Owner and Group
    chown user1 file.txt           # Change owner to user1
    chown user1:admin file.txt     # Change owner and group
    chown :admin file.txt          # Change group only

Change File Owner and Group (chown)
    The chown command is used to change the owner and/or the group of a file or directory.    
    Syntax:

    chown [owner][:group] [file]

    chown user1 file.txt      # Change owner to user1
    chown user1:admin file.txt # Change owner to user1 and group to admin
    chown :admin file.txt      # Change group to admin (no change to owner)


chgrp - The chgrp command is specifically used to change the group ownership of a file or directory. It doesn't change the user (owner), only the group.


Example:

    chgrp group <filename>

    chgrp developer <filename>
    #This changes the group to developers ,leaving the owner unchanged

    chgrp developers /path/to/directory
    #change the group of the directory and all its files /subdirectories to developers


chown -change the owner and group ownership 
chgrp- change only the group ownership


SYSTEM INFO:   

who - The who command in Linux is used to display who is logged into the system at a given moment.
       
        who | cut -d' ' -f1 | sort | uniq   #    Count unique users logged in
    
df - Disk Free Space
    The df command reports disk space usage for all mounted file systems.

    Examples:
        df -h
du (disk usage)- The du command provides the disk usage of files and directories.
Example:
   
    du -sh  #Display the total disk usage for the current directory
The uname command shows detailed information about the system (like the kernel name, version, and hardware architecture).
Example:   

    uname [options]
    -a → Show all system information
    -s → Show kernel name
    -r → Show kernel version
    -m → Show machine hardware name (architecture)
    -v → Show kernel version information
    -p → Show processor type

Pipe & Redirection
Pipe (|) - Sends output of one command as input to another:
    
    ls -l | grep "txt"

 
Redirection allows you to change where output goes or where input comes from.
    >   #redirectly the output to a file ,overwriting the file if it already exists
    >>  #redirect the output to a file,updating te file if it already exists
    
    > - Redirect output to file (overwrite)
    >> - Redirect output to file (append)
    < - Redirect input from file
    echo "Hello" > output.txt      # Overwrite
    echo "World" >> output.txt     # Append
    wc -l < input.txt              # Count lines from file

Error Redirection
    
- Standard Output (stdout) - normal output of the pogram
- Standard Error (stderr) - the default stream used by programs to send error messages or warnings.
- Standard Input (stdin) - the default stream where programs receive input data from the user or other programs.

    
 2> Redirect stderr -  To redirect the error to a file 
    Example:
       
        ls demo_non_exist_file 2> error_log.txt

 &>  - Redirect Both stdout and stderr to the Same File
    Example:
    
        ls <command-1> <command-2> &> err_log.txt
        
2>&1  - The expression 2>&1 is used to redirect the standard error (stderr) to the same place as the standard output (stdout).


/dev/null   -   in output we didnot see any output
    Example:
    
        ls > /dev/null
#The normal output (the list of files and directories)is discarded because it's redirected to /dev/null.will not see any output in terminal

    command 2> /dev/null                 # Discard stderr
    Example: ls dem 2> /dev/null
    command 2> /dev/null                 # Discard all
    Example:    ls demo.txt &> /dev/null
    
<< is a here document (also known as a heredoc) operator. It tells the shell to accept multiple lines of input until it encounters the delimiter specified (in this case, EOF).



Regular Expressions (Regexp)
  - Regexps are acronyms for regular expressions. 
  - Regular expressions are special characters or sets of characters that help us to search for data and match the complex pattern.
  - A regular expression is a sequence of characters that defines a search pattern. These patterns can match:
        A specific string
        A pattern of characters
        A range of characters (e.g., digits, letters)

Regexps are most commonly used with the Linux commands :- grep,vi,sed ,tr
Example:
        
        grep "<which text want to see>" <filename.txt>

Wildcards
    
   1.   .  It is called wild card,It matches any one character other than new line
        Example:
            there is file called animals ,inside thers is animals names are mentioning ,If I donot any particular animal name ,just type any one letter after or before or middle type "." then it display ouptut which are related

        Example:

                grep 'c.t' animals.txt
2.Matching range of characters [ ]:
    This one match lines that contian any vowel,you can use:
        Example:
        
            grep "[aeious]" <filename.txt>
   #Here, grep matches any line containing at least one of the characters within [aeiou] (any vowel).

3.Matching Zero or More Characters: * (Asterisk)

The asterisk * matches zero or more occurrences of the preceding character or group.
    Example:
    To match any line that contains the letter "d" followed by zero or more "o" characters and then "g" (like "dog","doog"."doghh",etc)
    
        grep "d*g" animals.txt
                    
Anchors

1.Match lines starting with "dog" (^)
    
The caret ^ is used to match the beginning of a line, and the dollar sign $ is used to match the end of a line.
    Example:
        
        grep "^d" animals.txt
    
2.Matching lines endiing with "fish" ($)
    Example:
        
        grep "fish$" <filename.txt>

3. Combining Patterns:(\|)
   
   Let’s say we want to match either 'cat' or 'dog'. You can use | to create an OR condition between patterns.
   Example:

        grep "cat\|dog" animals.txt
        grep "dog\|cat\|phant" animals.txt

   awk -  used for text processing
   
        awk /<word or letter contain line to print>/ <filename.txt>
        awk /a/ { print $1} data.txt    #print the first word (feild ) matching lines
        awk '$2 ~ /apple/ { print }' data.txt  #to print the entire line in a specific field
        awk '/^o/ data.txt  #to print Match Lines That Start with o letter or word
        awk '/e$/' data.txt    #to print match lines end with e letter
        awk '/sweet|orange/' dataa.txt  #to match multiple patterns using OR

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

ZOMBIE PROCESS:

  A zombie process is a process that has finished running, but still remains in the process table because its parent process hasn’t collected (waited for) its exit status.

    Think of it like this:
        A child process dies 
        The parent process should clean it up (using wait())
        If the parent does not clean it up → the child becomes a zombie
    
#fork()-to create new process by duplicatying parent process.
#wait()-system call used by the parent to read th exit status of its child.

Check for zombies:
    ps aux | grep Z

#TO TERMINATE ZOMBIE PROCESS WHEN RUNNING ZOMBIE PROCESS CODE
1.Find zombie process

    ps aux | grep defunct
2.Find parent PID with help of child pid which is show previous output
        
    ps -o ppid= -p <zombie pid>
    
3.kill parent process
    
    kill -9 <parent_pid>
    ps aux | grep defunct
