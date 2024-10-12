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























