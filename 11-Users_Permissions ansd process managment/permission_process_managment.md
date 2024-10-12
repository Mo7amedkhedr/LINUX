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

**Interactive Process**

•Started by the user inside a terminal

•Attached to the terminal (controlling terminal)

•Can run in the foreground or the background


![image93](https://github.com/user-attachments/assets/36520dec-50b7-4196-b20a-aef0e54dd1ea)


**Automatic Process**

•Also called a batch process

•This is a process that is not started directly by the user, instead, the user schedule it for a later start

•When started, It is not started inside a terminal, and not attached to a terminal (user does not even needs to be logged in when it starts)

•It is queued in a spooler area, to be executed on a FIFO manner

•It is scheduled in one of the following ways,

•Scheduled to run at a certain date and time (using the `at` command)

•Scheduled to run when system load is low (using the `batch` command)

•Scheduled to run periodically with certain periodicity or interval

**Scheduling Automatic Tasks at Command**

`$ at [options] <time> < <script file>`

`$ at -f <script file> <time>`

Schedules jobs described in the file to run at the specified time

•Example:

```
$ at 01:35 < job-to-run
$ at 9am February 2 < job-to-run
$ at tuesday +2 hours < job-to-run
$ at -f job-to-run noon
```

**Run at Low Load times (batch Command)**

`$ batch < <File containing Jobs>`

Run the script whenever the system load allows

•Example:

`$ batch < job-to-run`

**Cron Jobs**

•Cron Jobs are those which are scheduled to run periodically (the word cron comes from Greek word for time)

•Jobs are organized in commands or shell scripts

•They are scheduled by the user to run at,

•Fixed times

•Fixed dates

•Intervals

•Used often to automate repeated tasks (such as maintenance or administration tasks)

•Cron Jobs are organized in a set of configuration files that specify the Job to be run, and the required periodicity

•These are called `crontab files`

•Types of crontab files

•User crontab files (per user file)

•System crontab files (for root user)

•The crontab files have the following format

•It contains a line per scheduled job

•Each line has three sections,

•Time Schedule Section

•This section describes when this Job is to be executed

•User Section

•This section only applicable for some crontab files

•Job Description Section

•Command to execute


![image94](https://github.com/user-attachments/assets/d9aabfe9-af78-41e5-8360-062f3c21a08e)

**crontab Command**

•You should not edit the crontab file manually

•Instead use the `crontab command`, it performs checking for errors on the file before saving it

•Examples:

To edit your user specific crontab file `$ crontab -e`

To display your crontab file `$ crontab -l`

To remove you crontab file `$ crontab -r`

Note, •Applying the same commands with sudo performs the same on the system wide crontab file


`/var/spool/cron/crontabs`

•There are other crontab files setup by the System and packages installed on the distribution,

•The file `/etc/crontab`

•crontab files inside  `/etc/cron.d`

•It is not recommended to edit any of those files


**/etc/crontab**


•This is used by the system

•Not recommended to edit, since system updates will over-write any edits

•It calls scripts inside the directories

```
/etc/cron.monthly
/etc/cron.weekly
/etc/cron.daily
```

•Used mainly for system admin tasks

**/etc/cron.d**

•The `/etc/cron.d`  directory will contain crontab files installed by the different packages in the system

•Each package will have its own crontab file for periodic tasks required for this applications

•Typical periodic tasks,

•Checking the web for updates

•Archiving or Emptying log files

•Delete temp files

•Checking the Inbox for new messages


•Sometimes there are restrictions on which users are allowed to run cron jobs

•The restrictions are defined by the files,

`/etc/cron.allow`

`/etc/cron.deny`

•Those files will have list of users that are allowed/denied to/from use of cron jobs

•If both files don’t exists, then it is up to the distribution to define the behavior,

•Some would open the permission for all users

•Some would limit the permission for the root user

**Daemon Process**

•A Daemon process is a process that runs continuously in the background to perform a task, or waiting for services to be requested from it

•Linux use numerous daemons (normally start them at system startup) to perform things like,

•Accommodate requests for services from other computers on a network

•Respond to other programs

•Respond to hardware activity

•A tradition is to have the daemon name ends with letter ‘d’ such as (syslogd, xinetd, ftpd)

•Daemons keep listening until they are triggered to do some action, some of the triggers would be,

•A specific time or date (such as atd which handles Jobs scheduled by the at command)

•Passage of a specified time interval (such as crond which handles cron Jobs)

•A file landing in a particular directory

•Receipt of an e-mail or a Web request made through a particular communication means

•Connection request from a different computer (such as ftpd which handles FTP requests)

•Since a Daemon process needs to keep running in the background

   •It can not be attached with a terminal (otherwise, it will close with the terminal closure)
   
   •Accordingly, at its start, it disassociate itself from its contorlling terminal
   
•A Daemon process often needs to have its parent as the init process (PPID = 1)

•This is achieved for daemons started at system startup, since they will be launched by init

•Daemons starting afterwards can have their parent set to the init process, by launching the daemon process, then killing its parent. This will cause the kernel to re-parent the process to the init process

**Creation of a Daemon**

•When Daemons are created, the following happens,

•The parent of the Daemon is killed (or dies on its own), to make sure the Daemon is re-parented to the init process

•The Daemon is detached from his controlling terminal to make sure it remains up even when it closes

•The Daemon becomes a session leader (its SID is set to be equal to its PID)

•The Daemon becomes a process group leader (its PGID is set to be equal to its PID)

•Sets its current directory to be the root directory (/) to allow other any file system to unmoun

•Close any relation that it inherited from its parent process

•Sets its stdin, stdout, and stderr to either a logfile, the console, or mute it by using /dev/null



















