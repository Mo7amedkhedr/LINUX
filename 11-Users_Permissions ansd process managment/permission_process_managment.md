## Users and Permissions

**Multi-User System**

•Multiple users can access the system

•Simultaneously

•Using multiple physical terminals

•Using multiple virtual terminals

•Via a network connections (multiple users logged on to the same Linux machine)

•A mix of all the above


*At different time using the same interface

•Keep in mind, even if one user is using the Linux system, he may still be using multi-User features since there will be the root user as well


•So what does Linux need to do for multiple users

•Enable each user to have his own work area for his private files

•Enable each user to have his own environment settings

•Environment variables such as search paths, ….

•Aliases and shell functions

•Configuration parameters

* Protect each user files and resources from being manipulated by other users (unless the owner gives permission for that)
  
•Establish a multiple-tiered permission system, so a user maybe able to read a file but not able to modify it

•Enable multiple users to share some resources (such as files) with some level of permissions

•Protect system critical files from normal user access

•Linux provides,

•Each user has his own home directory (for his private files and directories)

`/home/tom/ or ~/`

•Each user has his own environment settings (per user startup scripts),

`~/.bashrc`

•Each user can have his own resources

•Files

•Directories

•Scripts and Binaries

•Sockets

•Devices

•Remember all these resources will be represented in Linux by files

## Users and Groups

•Each user is identified with his user-name and user-id (UID)

•Users can join different user groups

•Groups has group-name and group-id (GID)

•A user can be a member of multiple groups

•He can be added to a group

•He can be removed from the group

•Each user has a primary group

•Initially it is a special group created under his same name when the user is created

•Can be modified later

•Each resource in Linux has knowledge of :

•Which user own it (UID)

•Which group it belongs to (GID)

•Permissions for its owner, group, and the rest of the world

**Permissions**

•Permissions are associated with system resources not with users

•This means that each system resource will have an owner, and a set of permissions for its owner, and for non-owners

•There are 3 types of access rights

```
•Read (r)
•Write (w) (change, move, delete)
•Execute (x)
```

•And three levels of access levels

```
•User (u)
•Group (g)
•World, or others (o)
```

![image91](https://github.com/user-attachments/assets/5a274be7-aba7-4e42-9ede-25a7033362d6)


•To be able to read a file, you need `r` permission

•To be able to write/modify a file, you need `w` permission

•To be able to execute a binary or a script, you will need both `r` and `x`  permission

•If you want to preserve the permission of a file during copying, use,

`$ cp -p`

## Permissions of a Directory

A directory is a special type of file that contain meta information about its contents (subdirectories and files)

![image92](https://github.com/user-attachments/assets/48826a45-6c27-4a8a-827d-5085177e5bd8)

## Changing file Permissions 

**(chmod Command)**

`$ chmod <permission> <file or directory>`

This sets the selected permissions to the chosen file or directory

•Permissions can be set as relative to the current permissions

`+` to add this permission and keep other permissions untouched

`-` to remove this permission and keep other permissions untouched

```
$ chmod +x my-script
$ chmod u+w file1
$ chmod u-w file2
$ chmod go+r file1

```

•Permissions can be set as an absolute value irrespective of the current settings

`=` to set the permissions and overwrite the old permissions

`$ chmod a=x file3 (a for all ‘ugo’)`


## Defining Default Permissions 

**(umask Command)**

`$ umask`

`$ umask <mask value>`

This command sets the default permissions for all newly created files and folders

Examples:

```
$ umask (shows the current used umask)
$ umask 000 (Sets the mask for new file permissions)
```

Note, A mask of `000` means files are defaulted to permissions of `777`, since the mask is one for reset bits


## Special Permissions setuid/setgid Permission “s”

•When a user executes a program/script, it executes it using its own privileges

•For example, if the user does not have the privilege to write into a specific file then the script will fail to do so

•Sometimes, we need to run a script that require to do more than what we are privileged to do, in this case we can assign this script an `s` permission

•The `s` permission can be assigned to either the user or group

```
$ chmod u+s file1
$ chmod g+s file2
```

•This permission causes the script to execute with the privileges of its

•Owner (if ‘s’ is assigned to the user)

•Owning group (if ‘s’ is assigned to the group)

and not with the privileges of the user running it (as normal scripts would do)

•For example, if the script is owned by `root`, and it is assigned

`$ chmod u+s file1` Then this script will run with root privileges no matter which user is running it

**Sticky bit Permission “t”**

•The sticky bit can be very useful in shared directories


•When a directory has its sticky bit set, then only file owner (or root) can rename or delete any of its content (subdirectories/files)

•In case of the sticky bit not set, any user with write access can do this

•This way, in the shared directory, you can give write access of the directory to different users, so they can add files, but limit the deletion/renaming to file owners or root

`$ chmod +t dir1.`

## Changing the owner of a file

**chown Command**

`$ sudo chown <user>:<group> <file>`

This command change the owner of the file to a different user/group

Note that this command will need to have root access

Examples:

```
$ sudo chown tom file-1 (make the file owned by the user tom)
$ sudo chown -R tom dir-1 (recursive)
$ sudo chown tom:project-group file-1
$ sudo chown :project-group file-1
$ sudo chown tom: file-1 (group is the login group of the user)
```


## Changing the Owning Group (chgrp Command)

`$ sudo chgrp <group> <file/dir>`

This command will change the owning group of the file/dir

Examples:

```
$ sudo chgrp my-group file.txt
$ sudo chgrp -R my-group ./my-dir
```

## Adding Users

**useradd Command**

`$ useradd <options> <user-name>` This command adds a user to the Linux System

Examples:

•To Add a user “tom” `$ sudo useradd tom`

•To Add a user “tom” and create the home directory for him  `$ sudo useradd -m tom`

•To list defaults for user additions,

`$ sudo useradd -D` 

•To change defaults for user additions, `$ sudo useradd –D <options>`


## Setting User Password

**passwd Command**

`$ passwd`
`$ sudo passwd <username>`

This command is used to set the password of the current user, or of a different user

Examples:

After adding the user “tom”, you will need to setup his password,

`$ sudo passwd tom`

Then you will need to enter the password for “tom” twice

If you need to change your own password

`$ passwd`

**Identifying Users**

`$ id` •Display uid, gid, for current user

`$ who` Lists users logged in the system

`$ whoami` •Displays current user name

`$ finger`

`$ finger` (info about all users currently logged in)

`$ finger` username (info about username)

**To delete a user**

`$ sudo userdel username`

## groupadd & groupdel Commands

•To add a group `$ sudo groupadd groupname`

•To delete a group `$ sudo groupdel groupname`

•To add a user to a group `$ sudo useradd -G <group name> <username>`

•To modify the list of groups for a user `$ sudo usermod -G <list of group names> <username>`

**groups Command**

`$ groups`
`$ groups username` Display the groups for the current user, or for username


•Users are added in `/etc/passwd`

•Groups are added in `/etc/group`

•Passwords of users are encrypted and stored in `/etc/shadow`


`username:password:uid:gid:name:homedir:login-shell`

•If password is null string, no password needed

•If password is `x` or `*` , it is encrypted in `/etc/shadow`

`groupName:password:gid:userlist`

**su Command**

`$ su <Username>` This command allows the user to switch to login as a different user

Examples:

```
$ su <username> (switch to username and keep my environment)
$ su – <username> (switch to username and load his environment)
$ su (switch to the root , this is not acceptable in ubuntu)
```

In all of the above cases, the user will be prompted for a password for the new user, if a password is set for him

•To execute command as root (the only option in ubuntu), we can use the command ‘sudo’

`$ sudo <command>`

•For this to succeed, the username will need to be configured in the configuration file /etc/sudoers

## Process Management

**What is a Process**

•A Process is an instance of a running program

•Linux is a multi-tasking OS, This means it can run multiple tasks simultaneously

•The Linux Kernel distribute the processor time among the running processes

•Even a single application, may have multiple threads (for doing multiple actions in parallel)

•In Linux, a thread is just another process (of special nature) so a multi-threaded application is an application that have multiple processes running in parallel

•We can also have multiple instances of the same application running simultaneously in different processes


**Process Owner**

•Linux is a multi-user System, so multiple users can be using the system

•Each user starting a process becomes its owner

•Note that the process owner does not have to be the same as the owner of the binary file for the process

•Each process have an owner, some processes started by the system can be owned by the root user

•The process owner has privileges on his process. He can kill it, pause it, resume it

•The ‘root’ user have super powers on all system processes

•The process inherits its user privileges when trying to access resources

**Parent & Child Processes**

•Processes are organized in parent-child relationships

•Each process that creates another becomes the parent, and the new process becomes the child process

•First process to run is the `init` process that is started at system boot… this is the grand parent of all processes in the whole system

•If a process dies, then its orphan children are re-parented to `the init process`

**Process IDs**

•Each Process has a unique number to identify it

•It is called Process ID (PID)

•Each process will maintain its PID and the PID of its parent (PPID)

•The PID and PPID enable us to build the process hierarchy tree

•The init process is the parent of all processes, which has

PID = 1

PPID = 0

•To show the Process tree hierarchy

```
$ pstree (Show tree starting at init process)
$ pstree -p (to show PIDs of all processes)
$ pstree 1000 (Show tree starting at process with PID = 1000)
```

**Process Types**

•Interactive Processes

•Automatic Processes (Batch Processes)

•Daemon Processes


**Interactive Process**

•The process is started by a user within a terminal

•It is controlled via that terminal

•It is attached to its terminal, and will be killed if its terminal is closed

•It is called interactive, cause it communicates with the user through the terminal

•Examples:

```
$ ls
$ cat *.log | grep “error” | sort
$ echo “Good Morning” > my-file
```

**The “Job” Concept**

When a command is issued, the execution of this command is called a `Job`

•The Job can be,

**•A single process**

$ gedit

$ cat my-file

**•Multiple connected processes**

$ ls | sort

**•A script that runs multiple processes (within a sub-shell)**

$ ./my-script

•Jobs can be manipulated in the shell via “Job Control”


Jobs can run in the,

**•Foreground**

•All input and Output of the terminal is exclusively for this job

•User can not use the terminal for any other activity or start other jobs

•Only One Job can be a foreground job

•Initially the shell is in the foreground until a job is launched

**•Background**

•Job Input/Output does not utilize the terminal

•However, it is still attached to the terminal

•Possibility of multiple Jobs in the background for the same terminal

•Sometimes it is useful when,

•The process in the job has a Graphical User Interface and does not need the terminal for its Input/Output

•The process takes a long time in processing, and user needs to use the terminal for other purposes

•User needs to launch another job on the same terminal

•Start a job in the foreground

`$ gedit`

•Start a job in the background

`$ gedit &`

•Stop the foreground Job

```
$ gedit
Ctrl-z
```

•Resume the Paused Job in the foreground

```
$ gedit
Ctrl-z
$ fg
```

•Interrupt a foreground Job

```
$ gedit
Ctrl-c
```

•Switch the foreground Job to the background

```
$ gedit
Ctrl-z
$ bg
```

`$ jobs`  This will show which job runs in the FG, and which run in BG

Switch a background job into the foreground

```
$ jobs
$ fg %n (where n is the process number in the list )
```

•Kill a background Job (all processes in this Job)

```
$ jobs
$ kill %n
```

































