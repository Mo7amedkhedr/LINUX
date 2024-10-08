# Task 1
## resolv.conf (/etc/resolv.conf)
**The `resolv.conf` file is a configuration file used by Unix-like operating systems to configure the Domain Name System (DNS) resolver library. The DNS resolver library is responsible for resolving domain names to IP addresses, allowing applications to connect to remote servers using human-readable domain names rather than numerical IP addresses. nameserver: Common entries include the "nameserver" directive followed by the IP addresses of DNS servers**

![image11](https://github.com/user-attachments/assets/f441931f-acc6-4318-bd6c-72d1002e9cd1)

## fstab (/etc/fstab)
**The `/etc/fstab` file, short for File System Table, is a configuration file on Unix-like operating systems that defines how disk drives and partitions should be mounted and integrated into the file system during the system boot process. The information in the fstab file determines where each partition is mounted and with what options.**

![image12](https://github.com/user-attachments/assets/67c592e8-1d95-4add-8492-b68b9cf1f503)

## bashrc, .bash_profile

**bashrc file is a shell script that runs every time a new Bash session is initiated. It is used to configure the Bash environment by defining aliases, functions, environment variables, and executing commands**

 ____Shell Startup (Login Shells)____


When the Login Shell starts up, it goes through these steps to set the proper environment

* System Wide Configurations
*  It reads /etc/profile for global configurations (for all users)
* User Specific Configurations
* Then it reads one of the following for user specific extensions/overrides (if it finds one of the files starting from the first, it will read it and skip the rest) ~/.bash-profile ~/.bash-login ~/.profile

> [!NOTE]
> Note that those files normally call ~/.bashrc internally.


__Shell Startup  (Non-Login Shells)__

* Non-Login Shells build their environment as follows,
* First, they inherit the environment from their parent Login Shells
* On top of that, it reads the following configuration files,
* For Global settings they read the files: /etc/.bashrc /etc/bash.bashrc
* For user specific settings, they read, ~/.bashrc

## passwd, groups

The `passwd` command is used for changing a user's password. It allows users to set or modify their own passwords or, if used by a system administrator, to change the passwords of other users.

The `groups` command displays the groups to which a user belongs. It provides information about the group memberships of a specified user or, if no user is specified, the user who is currently logged in.

## crontab

The `Crontab` Linux Command goes on to check the time on the device and when a particular time arrives, it performs pre-defined tasks automatically . Linux Crontab is a powerful utility that is used for Scheduling and Automating Tasks in Unix-like operating systems. It facilitates the users to run the scripts or Linux Commands at specified times and intervals. It is ideal for repetitive tasks such as system maintenance, backups, and updates.

![image13](https://github.com/user-attachments/assets/c9c4d65f-bf69-44f7-ba67-bfd48f3fae5b)

## uptime

 `uptime` gives a one line display of the following information. 

 
* The current time
* how long the system has been running,
* how many users are currently logged on,
* the system load averages for the past 1, 5,and 15 minutes.

 ![image14](https://github.com/user-attachments/assets/5e40cea5-c8ff-4868-a142-ee69440ebea0)


 ## /proc/cmdline

 This file shows the parameters passed to the kernel at the time it is started. 
 
 `BOOT_IMAGE=/boot/vmlinuz-6.8.0-45-generic`: This part specifies the location of the Linux kernel image that the system is using for booting. In this case, it's located at /boot/vmlinuz-6.8.0-45-generic   

 `root=UUID=6a11842c-94b9-4219-849e-441f3fafb3f1`: This part indicates the root file system's Universal Unique Identifier (UUID). The root= parameter specifies the root file system for the operating system. In this case, it's identified by its UUID, which is a unique identifier assigned to the file system.
 
 `ro`: This option specifies that the root file system should be mounted as read-only. quiet indicates all verbose kernel messages are suppressed at boot time.

 `splash`: This option enables a graphical splash screen during the boot process


![image15](https://github.com/user-attachments/assets/1847f7c3-88ed-42b9-85c7-2b55e2a8c106)


## source.list

In Linux, particularly in Debian-based distributions like Ubuntu, the `sources.list`file is a configuration file that contains a list of repositories from which the package management system (such as APT - Advanced Package Tool) can retrieve and install software packages. This file is located in the `/etc/apt/` directory. Each line in the `sources.list` file represents a repository and typically includes information about the repository's location, distribution codename, and components.

![image16](https://github.com/user-attachments/assets/ae4d276d-6a1b-4d73-8b97-621fe8054bc3)


## XDG_SESSION_TYPE

`XDG_SESSION_TYPE` is an environment variable in Linux that provides information about the type of desktop session being used. It is part of the XDG (X Desktop Group) standard, which aims to standardize the base directory structure and environment variables used by desktop environments.

![image17](https://github.com/user-attachments/assets/32d4747e-a68d-43d6-860f-457158faec48)


## TimeZone

![image18](https://github.com/user-attachments/assets/db941211-2bc1-4f01-bc4c-b70340b95263)





