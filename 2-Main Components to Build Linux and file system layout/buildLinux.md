# Main Components to Build Linux

Toolchain , Bootloader , Kernel , Rootfs

![image2](https://github.com/user-attachments/assets/5efa63ff-6c22-4c98-be0a-d9428489270a)


## Booting Sequence 
### 1- PC Power on 
### 2- BIOS

**1-POST**

1- initial HW Drivers [screen, keyboard,...]
2- check HW Functionality
3- check portable device
4- check short circuit

**2-LOAD (MBR/GPT)**

### 3- MBR ( Master boot record ) ---> First stage bootloader

**Located in the 1st sector of the bootable disk. Responsible for loading and executing the GRUB boot loader. Contains information about GRUB**


![image3](https://github.com/user-attachments/assets/314f9d0a-d9f5-4692-afda-4f5334d1ebc4)

### 4- GRUB (GNU GRand Unified Bootloader) ---> Second stage bootloader

**The typical boot loader for modern Linux systems. Displays a splash screen with a menu for selecting boot options. Loads and executes the selected kernel image. Uses the grub.conf (or grub.cfg) configuration file**

![image4](https://github.com/user-attachments/assets/7fd8a878-b9b0-4e24-97df-f37db49f3af5)

### 5- Kernal
```
1- Load Device Drivers( Printer , GPIO , Network,etc)
2-memory initializations (RAM)
3-run init process
4-run user process
```

### 6- Init
**Executes runlevels programs based on the chosen run level. Historic systems use /etc/inittab, while modern systems use systemd.**
```
Run level 0 is matched by poweroff.target ( runlevel0.target is a symbolic link to poweroff.target).
Run level 1 is matched by rescue.target ( runlevel1.target is a symbolic link to rescue.target).
Run level 3 is emulated by multi-user.target ( runlevel3.target is a symbolic link to multi-user.target).
Run level 5 is emulated by graphical.target ( runlevel5.target is a symbolic link to graphical.target).
Run level 6 is emulated by reboot.target ( runlevel6.target is a symbolic link to reboot.target).
Emergency is matched by emergency.target.
```
### 7-Runlevel Programs
**Different services start depending on the run level. Located in directories specific to each run level. Programs starting with "S" or "K" for startup and kill, respectively. These are known as runlevel programs, and are executed from different directories depending on your run level. Each of the 6 runlevels described above has its own directory**

```
Run level 0 – /etc/rc0.d/
Run level 1 – /etc/rc1.d/
Run level 2  – /etc/rc2.d/
Run level 3  – /etc/rc3.d/
Run level 4 – /etc/rc4.d/
Run level 5 – /etc/rc5.d/
Run level 6 – /etc/rc6.d/
```
## initramfs (initial ram file system)

* InitRamfs not Mandatory for some devices/ if it is not exit so kernel will mount rootfs directly
* An initramfs is used to prepare Linux systems during boot before the init process starts.
* The initramfs usually takes care of mounting important file systems (by loading the proper kernel modules and drivers) such as /usr or /var, preparing the /dev file structure, etc.


## Init Process (SV , SD)
**_SystemD and SystemV are both init systems used in Linux_, but they differ in the way they manage services and processes. SystemV uses traditional init scripts and
runlevels, while SystemD use unit files and targets services**

## init script process

![image5](https://github.com/user-attachments/assets/488e69e2-1904-46ca-8e01-5ba9fe9fe0bd)

## System call

**A system call is a way for programs to interact with the operating system**

![image6](https://github.com/user-attachments/assets/c95093ff-67b2-4dad-846f-8232c8e29346)






## Linux File System Layout

A major difference Between Windows and Linux in file structure

**In Windows**
* Each partition of drive will have its own separate tree.. (C, D, E,…)
* Plugging a flash or a portable hard-disk results in a new tree
  
**In Linux**
* We have a single tree (unified file-system)
* The head of the tree is called the root ‘/’
* Plugging a device will add a branch (or sub-tree) to the file-system … at the selected mounting point


![image7](https://github.com/user-attachments/assets/2a199ef5-5447-4dc1-ac47-3a2b95ec526b)


![image8](https://github.com/user-attachments/assets/b4600674-a47c-4ffd-9f5f-ac6fbfef9a97)


![image9](https://github.com/user-attachments/assets/fddbdeec-e1ca-4db7-b044-28513ec7ac73)


![image10](https://github.com/user-attachments/assets/f22838ab-8bff-40b9-876e-8fa5168b72ac)



## Linux File-System Hierarchy

**/**      

 ` Root Directory, the head of the tree`

**/home/**  

`Contains the home directories of users /home/khedr (my home directory) Each user can put his files under his home directory`

**/root/**  

`The home directory for the super user (admin)`

**/usr/** 

`Files (programs, libraries, documentation, etc..) used by all users in the system`

**Examples:**

/usr/bin/ binaries used by all users binaries included with the distribution.

/usr/local/ files that don’t come with the distribution and installed by the user.

/usr/sbin/ system files that come with the distribution.

/usr/share/ shared data by programs in /usr/bin/


**/boot/**

`Boot loader, Linux Kernel, Startup files`

**Examples:**

/boot/vmlinuz/ Linux kernel image

/boot/grup/grup.conf Bootloader configuration file

/boot/initrd/ Startup Files used in booting

**/bin/**

`Common programs, shared by the system, the system administrator and the users`

**/sbin/**

`System binaries Programs for use by the system and the system admin`

**/lib/**

Shared libraries

**/opt/**

Optional software; Extra and third party software


**/dev/**

`Device nodes; not a regular file Each device in the system is represented by a file, so to write to the device, we write to this file, to read from a device, we read from this file`

**/etc/**

`System configuration files (similar to those in the Control Panel in Windows)`

**Examples:**

/etc/fstab contains a list of storage devices and their associated mount point

/etc/passwd contains list of user accounts

**/var/**

`Storage for variable files and temporary files created by users, such as log files, the mail queue, the print spooler area, space for temporary storage of files downloaded from the Internet, or to keep an image of a CD before burning it.`

**Examples:**

/var/log  ---> log files

/var/log/messages ---> system log file

**/net/**

`Standard mount point for entire remote file systems`

**/media/**

`contains the mount points of removable media devices such as CD-ROMs and USBs (that are mounted automatically)`

**/mnt/**

`Standard mount point for external file systems, e.g. a CD-ROM or a digital camera.`

**/proc/**

`Does not contain stored files, it is just the front of some devices feedback (reading from it, is like asking a driver to provide information )Used to read information about system resources.`

**/sys/**

`Same as /proc/`

**/tmp/**

`Temporary space for use by the system, cleaned upon reboot, so don't use this for saving any work!`

**/lost+found/**

`For Every disk partition, contains files that were saved during failures are here.`



