Introduction Of Linux

Linux:

The operating system (OS) is like a manager or middleman between your
computer's hardware (CPU, memory, hard drive) and the software
(applications you run). It makes sure everything works together
smoothly.

Key Responsibilities:

Resource Management: Decides how hardware resources like CPU time,
memory, and disk space are shared.

Process Management: Keeps track of running programs, starting/stopping
them, and allocating resources.

Memory Management: Manages RAM usage so multiple programs can run
without crashing the system.

User/Group Management: Controls access to files and commands, often
using user accounts and permissions.

\| OS \| Focus \| Strengths \| Weaknesses \|

\| \-\-\-\-\-\-\-\-\-\-- \| \-\-\-\-\-\-\-\-\-\-- \|
\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--
\|
\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--
\|

\| Windows \| GUI-focused \| Easy to use, lots of software \| Less
secure, more resource-heavy \|

\| Linux \| CLI-focused \| Secure(least priviledge), lightweight, \| \|

\| \| \| powerful for servers \| Steeper learning curve for beginners \|

\| Mac \| Hybrid \| Good GUI + Unix-like security \| Expensive, less
customizable \|

Simple example :

Think of the OS as a restaurant manager: it organizes chefs (hardware)
and recipes (software), ensures the kitchen runs efficiently, and makes
sure everyone gets what they need without chaos.

Linux Architecture:

Linux has a layered structure that helps separate responsibilities.

Layer of linux architecture:

1.Hardware layer:

The physical components: CPU, memory, disk, network devices.

Linux interacts with these via drivers.

2.Kernel Layer (Core):

The most important part. Think of it as the "brain" of Linux.

Responsibilities:

Process management

Memory management

Device management

System calls (interface between user programs and hardware)

3.System Call Interface (API Layer):

Provides functions for programs to request services from the kernel.

Example: Reading a file, writing data, creating a process.

4.Shell / Command Interpreter:

Acts as a bridge between the user and the kernel.

Examples: Bash, Zsh, Fish.

Users type commands here, and the shell translates them for the kernel.

5.user space / Application layer:

All the programs and apps you use run here: browsers, editors, games.

They use the shell and system calls to interact with hardware.

Boot Process:

1.BIOS:

When turn on the computer, the BIOS (older systems) or UEFI (newer
systems) performs a Power-On Self Test (POST) to check hardware like
CPU, RAM, keyboard, and drives.

2.Bootloader (GRUB2)

What happens: The bootloader (usually GRUB2) loads the Linux kernel into
memory and initializes a temporary RAM filesystem.

3.Kernel Initialization:

What happens: The Linux kernel decompresses itself, sets up memory
management, process scheduling, and mounts the root filesystem (/).

4.Init System (systemd)

What happens: The systemd process starts as PID 1 (the first process)
and becomes responsible for launching all other processes and services.

5.System Services

What happens: systemd launches essential background services (like
networking, logging, database services, GUI if applicable).

6.Login Prompt

What happens: Finally, the system presents a login prompt (text-based or
graphical), allowing the user to log in and start using the system.

Simple Example to understnad the Linux Boot Process -- Restaurant
Analogy

BIOS/UEFI → Checking the Restaurant

The manager inspects the kitchen, tables, and equipment to make sure
everything works.

Bootloader (GRUB2) → Unpacking Ingredients

The chef opens the delivery boxes and decides what to cook first (loads
the kernel).

Kernel Initialization → Setting Up the Kitchen

The chef arranges the tools, stove, and counters so cooking can begin
(memory and process setup).

Init System (systemd) → Assigning Staff Tasks

The manager tells the waiters, cooks, and cleaners what to do and when
(starting system processes).

System Services → Opening the Restaurant

Lights, ovens, and music start; everything is ready for customers
(networking, printing, background services).

Login Prompt → First Customer Arrives

The doors open, and the first customer walks in (user can log in and use
the system).

Linux As File System:

Linux is often described as a "Linux as a File System" because
everything in Linux is treated as a file---not just documents or images,
but also devices, hardware, and even processes.

1.Everything is a file

Hard drives, USBs, keyboards, network connections → all are represented
as files.

Example: /dev/sda → represents a hard drive

/dev/ttyUSB0 → represents a USB device

2.Unified Directory Tree

Linux has a single hierarchical directory structure (rooted at /).

Devices, system info, and actual data all appear in this same tree.

Example: /etc (configuration), /home (user files), /proc (process info),
/dev (devices)

3.File Permissions Control Everything

Linux uses permissions on files to manage access to users, groups, and
processes.

This makes the OS secure and organized.

4.Interaction via Files

Programs interact with hardware and other resources as if they are
reading/writing files.

Example: Writing to /dev/sda writes data to a hard disk, reading
/proc/cpuinfo gives CPU information.

This is why Linux is often called a file-system-oriented OS---because
files are the core abstraction for everything in the system.

LINUX FILE TYPE:

Regular File - Normal data file (text, code, images, etc.)
/home/user/report.txt Store documents, scripts, or data

Directory d Folder containing files /etc Organize files and subfolders

Symbolic Link l Shortcut/alias to another file /usr/bin/python -\>
Access files from multiple paths without duplication

/usr/bin/python3.11

Character Device c Device that handles data character by character
/dev/ttyS0 (serial port) Read/write one character at a time to devices
like keyboards or mice

Block Device b Device that handles data in blocks /dev/sda1 (hard drive
partition) Read/write large chunks of data efficiently for disks or
storage

Socket s Endpoint for communication between processes
/var/run/docker.sock Allow programs to talk to each other over the
network or locally

Pipe p Channel for communication between processes /tmp/mypipe One
process writes data, another reads it (e.g., \`ps aux)

IMPORTANT DIRECTORIES:

1\. /bin

It Contains essential system command binaries that are required for
basic system functionality (like ls, cp, cat, etc.).

Why it's important: These binaries are needed for the system to
function, even in single-user mode or if only a minimal environment is
available. This directory is for commands that are critical for system
recovery or repair.

Example: /bin/ls

/bin/bash

2./boot

The /boot directory contains all the files required to boot the system.
This includes the Linux kernel, initial ramdisk (initrd/initramfs),
bootloader configuration files, and related files that are loaded during
the boot process.

Why it's important: Without the files in /boot, the system would not be
able to load the operating system properly. The bootloader (e.g., GRUB)
uses the contents of this directory to start the system. The kernel and
initrd are crucial because they form the foundation for booting the
operating system and mounting the root file system.

3./dev - device files

Contains device files, which are used to interact with hardware (disks,
peripherals, etc.) or software devices (virtual devices).

This directory is essential for interfacing with physical or virtual
hardware on the system. For example, hard drives, terminals, USB
devices, etc., are represented as files in /dev.

Examples:

/dev/sda - First SATA disk drive.

/dev/null - Null device, used to discard data.

/dev/tty - Terminal device.

4./etc - configuration files

Stores system-wide configuration files and settings. It\'s where most
services (like NGINX, SSH, systemd) have their configuration files.

Why it's important: Any system-wide configuration or service setup is
located here. Changing these files can alter system behavior or the
behavior of specific services.

Examples:

/etc/nginx/ - NGINX server configurations.

/etc/ssh/ - SSH configurations.

/etc/systemd/ - Systemd service configurations.

5\. /home -user directories:

Contains personal directories for users on the system. Each user
typically has their own subdirectory within /home.

Why it's important: This is where user-specific data, documents,
configurations, and preferences are stored.

Examples:

/home/user1/ - User-specific files for user1

/home/user2/ - User-specific files for user2.

6\. /lib

/lib is a directory in Linux that stores shared libraries and kernel
modules needed by both system programs and user applications to
function.

Why is it important?

It provides the core libraries required by programs to run, making code
more efficient and reusable. Without /lib, many system functions (like
memory management, I/O operations, and device handling) wouldn\'t work.

Example:

When you run a program like ls, it loads libraries from /lib to handle
basic tasks. Similarly, when you install a new program, it links to
shared libraries in /lib to ensure everything works properly.

7\. /mount

The /media directory is where Linux automatically mounts removable media
devices like USB drives, CDs, and DVDs. It provides a standard location
for accessing external storage.

It allows users to access and manage files from removable devices
easily. The system automatically mounts external storage here, making it
user-friendly for interacting with things like USB drives or external
hard drives.

Example:

/media/myusb

8\. /mnt - mount

The /mnt directory in Linux is traditionally used for temporary mounting
of file systems. While modern Linux systems often handle mounting
automatically (especially for removable media under /media).

It provides a central location for mounting external file systems that
are needed temporarily. It\'s particularly useful for system
administration and maintenance tasks.

Example:

If you need to temporarily mount a new disk for copying files, you would
mount it under /mnt/data. Once the task is complete, you can safely
unmount it.

9\. /opt - Optional third party applications

Contains third-party application software, especially when they are not
part of the operating system's package manager.

Why it's important: This directory is used for installing software
packages that are manually downloaded and installed. Unlike /usr (which
contains essential system software), /opt is used for optional
applications.

Examples:

/opt/docker/

10\. /pro - process and kernel information

Contains a virtual file system that provides runtime system information,
such as process information, memory usage, and hardware stats.

Why it's important: This directory doesn\'t actually contain real files
but virtual files that provide system status information. It\'s a key
source of data for system monitoring and debugging.

Example:

/proc/cpuinfo - Information about the CPU.

/proc/meminfo - Memory usage statistics.

/proc/uptime - System uptime

11\. /var -variable data

Stores variable data files that change frequently, such as logs, cache
files, and mail.

Why it's important: It\'s a place where data is often written to while
the system is running, like log files, databases, or even temporary
files generated by applications.

Examples:

/var/log/ - Log files for system and applications.

/var/cache/ - Cached data that can be recreated.

11\. /usr - user utilities and application

It Contains user-level applications and utilities, libraries, and
documentation.

Why it's important: These are non-essential binaries for users, but they
are typically needed for the day-to-day operation of the system.

Examples:

/usr/bin/ - Non-essential user binaries (e.g., python, vim).

/usr/lib/ - Libraries needed by applications.

12\. /tmp - Temportary files

Stores temporary files that are used during system operations or by
applications.

Why it's important: Files stored here are not guaranteed to be
persistent and may be deleted upon system reboot. Used for files that
are temporarily needed.

Examples:

/tmp/ - Temporary storage for files that can be safely deleted after
use.

13\. /root

The /root directory is the home directory for the root user in Linux.

It holds system-related files, configuration files, and scripts that the
root user uses for system administration.

The root user (the administrator of the system) requires its own home
directory, and that directory is located at /root. The root user has
full administrative control over the entire system and can modify any
file.

Example:

The root user might store administrative scripts in /root/scripts/ and
custom configuration files in /root/.bashrc. These files help the root
user manage the system more effectively.

14./run

/run directory is a temporary filesystem (typically a tmpfs) that is
used to store runtime data.

It is cleared out when the system restarts, and it uses memory (RAM)
instead of disk for faster performance.

15\. /sbin

/sbin stands for \"system binaries.\" It contains important system
executables (programs or commands) that are essential for the system's
operation, especially for system administrators (sysadmins).

These are commands used mainly by root (superuser) or system maintenance
tasks, not regular users.

Inside the sbin directory like ifconfig ,reboot,fsck,mount

16\. /srv

/srv holds data that is served by the system\'s services (like websites,
FTP servers, databases).

It keeps service-specific files organized and separate from other system
files or user data.

Example:

/srv/ftp/ -- Files served by an FTP server.

/srv/www/ -- Files served by a web server (e.g., Apache or Nginx).

/srv/svn/ -- Data for Subversion (SVN) repositories.

/srv/mysql/

17\. /sys

/sys is a virtual filesystem that provides access to kernel and hardware
information in real-time.

Example:

Think of /sys like a control panel for your computer's hardware. It
shows you things like:

How fast your CPU is running.

The status of your battery.

How much space is left on your hard drive.

INODE

An inode is a data structure on a Linux filesystem that stores
everything about a file except its name.

Each file has one inode.

Inode have the metadta of file without the filename and directory path .

Actually innode conatin the information like the

File type

User (UID)

Group (GID)

Permissions (rwx)

Timestamps (created, modified, accessed)

Size of the file

Number of hard links

Pointers to the actual data blocks on disk

When create file ,inode is automatically assign to the file

Command to see inode details

stat \<filename\>

output :

stat demo

File: demo

Size: 0

Blocks: 0

Device: 37h/55d Inode: 7376

Links: 1

Access：（0644/-rw-rir）

Access: 2025-12-02 05:19:55.966367276 +0000

Modify: 2025-12-02 05:19:55.966367276 +0000

Change: 2025-12-02 05:19:55.966367276 +0000

Birth: 2025-12-02 05:19:55.966367276 +0000

INODE EXHAUSTION

Inode exhaustion happens when you run out of inodes, even though your
disk still has free space. Inodes are like the \"metadata\" of files ---
they store information like file permissions, size, timestamps, and the
actual data location on the disk.

Each file, folder, and symbolic link on your system consumes one inode,
and inodes are finite. If you have millions of small files, you can
exhaust all inodes before you run out of actual disk space.

How to detect inode exhaustion:

1.Check overall inode usage:

df -i

2.Find which directory is consuming all the inodes:

du \--inodes -x / \| sort -n \| tail

To fix the issuse:

Delete old files:

Clean up old logs, caches, or temp files using commands like rm -rf.

Set up log rotation using logrotate to automatically handle log file
size.

Clean package manager caches (apt clean or yum clean).

Clean Docker containers: docker system prune -af

Last resort: If the filesystem was created with too few inodes, you may
need to recreate the filesystem with more inodes (mkfs.ext4 -N).

#summary

inode exhaustion is when you run out of inodes (rooms), but your disk
still has free space (beds). It often happens when apps or services
create millions of tiny files. To fix it, clean up old files, rotate
logs, and configure systems to manage temporary files more efficiently.

HARD LINK

Points directly to the same inode as the original file.

Both names share the same data.

If you delete one, the file still exists because the other link still
points to the inode.

-\>Think of it as two names for the same file.

Example:

1.Create the hard link

ln \<already created file \> \<newly create the file\>

ln demo.txt backup.txt

2.check inode

ls -i \<file1_name\> \<file2.txt\>

-\>Both files are have the same inode number ,even if we delete the
original file ,backup file is still accessable

SOFT LINK OR SYMBOLIC LINK:

Point to the path of another file (like a shortcut)

If the original file is deleted,the soft link becomes broken

To create the soft link

ln -s \<original file\> \<new file\>

To see the link is

ln -i \<original file\> \<new file\>

Once it is created the two files different inode number.If original file
is deleted,then soft link is broken ,we cannot access the backup file

#Because soft link points to the path, not the inode.

Original file gone → link broken.

\| Feature \| Hard Link \| Soft Link (Symbolic Link) \|

\|
\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--
\| \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-- \|
\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

\| Points to \| Inode of original file \| Path of original file

\| Inode number \| Same as original file \| Different

\| Works after original file is deleted? \| Yes \| No(broken link)

\| Can link directories? \| ❌No \| ✔️ Yes

\| Can work across different filesystems? \| ❌No \| ✔️ Yes

\| File content shared? \| ✔️ Yes (same data blocks) \| ❌ No (just a
pointer)

\| Shows file type \| Regular file \| Link (\`ls -l\` shows \`l\`)

\| Size \| Same as file \| Size = length of path name

\| Creation command \| \`ln file1 file2\` \| \`ln -s file1 file2\`

LINUX COMMANDS:

1.Navigation Commands:

pwd (Print Working Directory) - Displays the absolute path of the
current working directory.

Example:

pwd

output:

/root

cd (change Directory) - Allows you to change the current working
directory to another directory

Eg:

cd \<directory_name\>

cd .. #Go back the previous directory level of the current directory

cd \~ #goes home directory

cd - #go back previous directory

cd \$HOME \# go to the home directory

ls (list) - Lists files and directories in the current directory.

Eg:

ls

ls .. #list parent directory files

ls -a #List all files and directories (including hidden)

ls -l #List files with detailed information (permissions, ownership,
size)

ls -ltu #list lastes modified or newly created file at top

ls -ltc #list latest modified the permission of file

ls -s #list the files in the sorted alphabetic order

ls -al \--author #list username of the author of the file

tree - It shows the tree level view of the directories and files

FILE OPERATION:

mkdir - create a directory

mkdir \<directory_name\>

mkdir -p /path/to/file

touch - create the file

touch \<filename\>

cat - it show content of the file

cat \<file_name\>

cp - copy file from one loaction to another location

cp \<src directory_location\> \<destination_directory \_lcoation\>

mv - move file from one location to another location

mv \<src directory_location\> \<destination_directory \_lcoation\>

rm - to remove the file

rm \<filename\>

rmdir - to remove the empty directory

rmdir \<filename\>

SEARCH & FILTER:

grep - Search text inside files

Example:

grep \"error\" /var/log/syslog

grep -i \"failed\" auth.log #Search ignore case

grep -r \"nginx\" /etc #Search recursively in folder

find - To find a file in directory structure

Example:

find / -name \<name of the file\>

find /var/log -name \"\*.log\"

find /tmp -type f -mtime +7 -delete #Find and delete files older than 7
days

sed - search & replace text inside files without opening file,it edit
text automatically

Example:

sed \'s/old text/new text/\' \<filename\>.txt #s means substitution

sed\'s/banana/BANANA/g\' fruits.txt #g means all occurrence of the text

sed \'2d\' \<filename.txt\> #to delete the two line

sed \'s/\^/Line: /\' \<filename.txt\> #to add the prefix \"Line: \" to
each line in text.txt.

sed \'s/old/new/\' file.txt \# Replace first occurrence per line

sed \'1,5d\' filename.txt \# Delete lines 1-5

sed -n \'2p\' filename.txt #print line 2

sed \'3i\\New line\' filename.txt \# Insert before line 3

sed \'3a\\New line\' filename.txt \# Append after line 3

sed \'/\^\$/d\' data.txt #to delete the empty line

sed \'s/\\(\[A-Za-z\]\*\\) \\(\[A-Za-z\]\*\\)/\\2 \\1/\' names.txt #to
swap the colunm word

cut - It is used to extract specific columns or fields from a file or
text. cut helps you extract specific columns or characters from text.It
just prints the selected parts

Example:

cut -d \" \" -f1 file.txt #show first row of the column
(d-delimiter(space,colon,comma) ,f-field/column number)

echo \"abcdef\" \| cut -c 1-3 #show ranges of character (c- character
positions)

outpu: abc

cut -b 1-4 filename.txt #extract first 4 byte of each line

sort - Sort lines alphabetically or numerically

Example:

sort -n \<filename.txt\> #sort number correctly

sort -r \<filename.txt\> #sort reverse order

sort -u \<filename.txt\> #remove duplicate lines

uniq - The uniq command in Linux is used to filter out duplicate lines
from a file or input.

Example:

uniq \<filename.txt\> #it removes consecutive duplicates lines from the
input

uniq -c \<filename.txt\> #display the count of each in unique line

uniq -d \<filename.txt\> #it show only lines that are repeated

uniq -u \<filename.txt\> \# it show only the lines that are unique

PERMISSION:

permissions control who can read, write, or execute a file. The three
main commands to modify these permissions are:

chmod: Change file permissions.

chown: Change file ownership (user and group).

chgrp: Change the group of a file.

The chmod command is used to set or modify the permissions of a file or
directory. Permissions are defined in three categories:

Owner (user who owns the file)

Group (users in the file\'s group)

Others (everyone else)

Syntax:

chmod \[permission\] \[file\]

Permissions

Permissions are specified using either symbolic mode (letters) or
numeric mode (numbers).

Symbolic Mode (letters)

r → Read (4)

w → Write (3)

x → Execute (1)

\+ → Add permission

\- → Remove permission

= → Set exact permissions

Example:

Add execute permission for the user:

chmod u+x filename

remove write permission for the group

chmod g-w filename

Set read and write permissions for owner, and read for group and others:

chmod u=rw,g=r,o=r filename

chmod u+x file.txt \# Give the owner execute permission

chmod g-w file.txt \# Remove write permission for the group

chmod o+r file.txt \# Give others read permission

chmod a-x file.txt \# Remove execute permission for everyone

Change File Owner and Group (chown)

The chown command is used to change the owner and/or the group of a file
or directory.

Syntax:

chown \[owner\]\[:group\] \[file\]

chown user1 file.txt \# Change owner to user1

chown user1:admin file.txt \# Change owner to user1 and group to admin

chown :admin file.txt \# Change group to admin (no change to owner)

chgrp - The chgrp command is specifically used to change the group
ownership of a file or directory. It doesn\'t change the user (owner),
only the group.

Example:

chgrp group \<filename\>

chgrp developer \<filename\>

#This changes the group to developers ,leaving the owner unchanged

chgrp developers /path/to/directory

#change the group of the directory and all its files /subdirectories to
developers

chown -change the owner and group ownership

chgrp- change only the group ownership

SYSTEM INFO:

who - The who command in Linux is used to display who is logged into the
system at a given moment.

who \| cut -d\' \' -f1 \| sort \| uniq \# Count unique users logged in

df - Disk Free Space

The df command reports disk space usage for all mounted file systems.

Examples:

df -h

du (disk usage)- The du command provides the disk usage of files and
directories.

Example:

du -sh #Display the total disk usage for the current directory

uname -- System Information

The uname command shows detailed information about the system (like the
kernel name, version, and hardware architecture).

Example:

uname \[options\]

-a → Show all system information

-s → Show kernel name

-r → Show kernel version

-m → Show machine hardware name (architecture)

-v → Show kernel version information

-p → Show processor type

PIPE & DIRECTION:

The pipe symbol (\|) is used to send the output of one command as the
input to another command.

Example:

ls -l \| grep \"txt\"

Redirection allows you to change where output goes or where input comes
from.

\> #redirectly the output to a file ,overwriting the file if it already
exists

\>\> #redirect the output to a file,updating te file if it already
exists

Example:

echo \"Hello, world!\" \> output.txt

\< #redirect input from a file to a command

Example:

wc -l \| \<filename.txt\>

#filename.txt redirect input to the \"wc -l \"command ,then wc -l counts
number of lines of lines

Standard Output (stdout) - normal output of the pogram

Standard Error (stderr) - the default stream used by programs to send
error messages or warnings.

Standard Input (stdin) - the default stream where programs receive input
data from the user or other programs.

2\> Redirect stderr - To redirect the error to a file

Example:

ls demo_non_exist_file 2\> error_log.txt

&\> - Redirect Both stdout and stderr to the Same File

Example:

ls \<command-1\> \<command-2\> &\> err_log.txt

2\>&1 - The expression 2\>&1 is used to redirect the standard error
(stderr) to the same place as the standard output (stdout).

/dev/null - in output we didnot see any output

Example:

ls \> /dev/null

#The normal output (the list of files and directories)is discarded
because it\'s redirected to /dev/null.will not see any output in
terminal

command 2\> /dev/null \# Discard stderr

Example: ls dem 2\> /dev/null

command 2\> /dev/null \# Discard all

Example: ls demo.txt &\> /dev/null

\<\< is a here document (also known as a heredoc) operator. It tells the
shell to accept multiple lines of input until it encounters the
delimiter specified (in this case, EOF).

REGULAR EXPRESSION(Regexps):

Regexps are acronyms for regular expressions. Regular expressions are
special characters or sets of characters that help us to search for data
and match the complex pattern.

A regular expression is a sequence of characters that defines a search
pattern. These patterns can match:

A specific string

A pattern of characters

A range of characters (e.g., digits, letters)

Regexps are most commonly used with the Linux commands :- grep,vi,sed
,tr

Example:

grep \"\<which text want to see\>\" \<filename.txt\>

WILDCARDS:

1\. . It is called wild card,It matches any one character other than new
line

Example:

there is file called animals ,inside thers is animals names are
mentioning ,If I donot any particular animal name ,just type any one
letter after or before or middle type \".\" then it display ouptut which
are related

Example:

grep \'c.t\' animals.txt

2.Matching range of characters \[ \]:

This one match lines that contian any vowel,you can use:

Example:

grep \"\[aeious\]\" \<filename.txt\>

#Here, grep matches any line containing at least one of the characters
within \[aeiou\] (any vowel).

3.Matching Zero or More Characters: \* (Asterisk)

The asterisk \* matches zero or more occurrences of the preceding
character or group.

Example:

To match any line that contains the letter \"d\" followed by zero or
more \"o\" characters and then \"g\" (like
\"dog\",\"doog\".\"doghh\",etc)

grep \"d\*g\" animals.txt

ANCHOR:

1.Match lines starting with \"dog\" (\^)

The caret \^ is used to match the beginning of a line, and the dollar
sign \$ is used to match the end of a line.

Example:

grep \"\^d\" animals.txt

2.Matching lines endiing with \"fish\" (\$)

Example:

grep \"fish\$\" \<filename.txt\>

3\. Combining Patterns:(\\\|)

Let's say we want to match either \'cat\' or \'dog\'. You can use \| to
create an OR condition between patterns.

Example:

grep \"cat\\\|dog\" animals.txt

grep \"dog\\\|cat\\\|phant\" animals.txt

awk - used for text processing

Example:

awk /\<word or letter contain line to print\>/ \<filename.txt\>

awk /a/ { print \$1} data.txt #print the first word (feild ) matching
lines

awk \'\$2 \~ /apple/ { print }\' data.txt #to print the entire line in a
specific field

awk \'/\^o/ data.txt #to print Match Lines That Start with o letter or
word

awk \'/e\$/\' data.txt #to print match lines end with e letter

awk \'/sweet\|orange/\' dataa.txt #to match multiple patterns using OR

ZOMBIE PROCESS:

A zombie process is a process that has finished running, but still
remains in the process table because its parent process hasn't collected
(waited for) its exit status.

Think of it like this:

A child process dies

The parent process should clean it up (using wait())

If the parent does not clean it up → the child becomes a zombie

#fork()-to create new process by duplicatying parent process.

#wait()-system call used by the parent to read th exit status of its
child.

check the zombie process :

ps aux \| grep Z

#defunc means child process is dead but is not remove from process table

#To fix the zombie process ,add wait() in the parent process ,

#the parent will wait for the child, and the zombie will not appear in
the process table because the parent collects the exit status of the
child.

#to check process: ps aux \| grep \'\[Z\]\'

#TO TERMINATE ZOMBIE PROCESS WHEN RUNNING THE ZOM.C CODE

1.Find zombie process

ps aux \| grep defunct

2.Find parent PID with help of child pid which is show previous output

ps -o ppid= -p \<zombie pid\>

3.kill parent process

kill -9 \<parent_pid\>
