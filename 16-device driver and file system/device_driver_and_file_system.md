**What is a Device Driver ??**

![image100](https://github.com/user-attachments/assets/1254f440-401a-4244-bc64-4f77e18036a4)

•A device driver is a `kernel module` responsible for handling a hardware device in order to isolate the operating system and the user application from the details of this hardware device

•This way, the Linux Kernel and the user applications running on top of it don’t have to know about the details of the hardware device

•For example, the user application deals with a hard disk (of any kind) and a flash drive the same way, although the internal handling of them is completely different

•This leads to possibility for the introduction of new hardware devices everyday, and the Linux Kernel can support them using the proper device driver without the need to modify the kernel

•This definition represent only some of the device drivers and not all of them

•device drivers are not limited to the support of hardware devices

•Some device drivers perform a complete software function and don’t perform any hardware device interaction

•Examples are the device drivers supporting these devices,

•Random number generator (/dev/random & /dev/urandom)

•Zeros generator (/dev/zero)

•Output Sink (/dev/null)

•We need to understand the more general definition of Devices and Device Driver



**The Extendable Architecture of Linux**

•Linux kernel is under continuous development with thousands of developers with different objectives

•It supports a lot of fancy and advanced features

•Not all of these features are required by all users

•It also has support for tons of hardware devices (printers, scanners, cameras, storage devices, …. )

•To build the kernel with all of its features and hardware device support will result in a very large image (unnecessarily) and some times with conflicting functions

•With such a large image, Linux may not be able to run on a lot of systems including embedded systems, and will need too much resources (again unnecessarily)

•The solution for that problem, is that a lot of the advanced features, and the hardware devices support functionality are considered optional features

•When building the kernel, we go through a configuration phase, to set for each optional feature,

•Enable: to build the code for that feature and include it in the kernel image build in a static way

•Disable: To bypass the build the code for that feature, and hence the kernel would not support it

•Module: The code is built as a separate module, resulting in a separate binary (*.ko), which can be dynamically added/removed to/from the kernel at run time on need basis

•Also, kernel modules can be developed and built independent of the kernel build and then added to the kernel tree for future load/unload

•A lot of the kernel features can be built as a “Kernel Loadable Modules” to keep the kernel image smaller, and to add the flexibility of adding or removing them when needed

**Kernel Loadable Module (KLM)**

•A KLM is a binary file (*.ko) that can be created as an additional step when building the Linux Kernel, or as a completely separate procedure

•KLM’s reside in the Linux tree in,

`/lib/modules/{kernel release}/`

•KLM’s can be loaded or unloaded to/from the Linux Kernel at run time (after the kernel has booted)

•Using KLM enables the following,

•No need to rebuild the kernel every time a new KLM is introduced

•No need to reboot the kernel every time we need to load/unload a KLM

•The KLM runs inside the kernel


**Loading Kernel Modules**

•Kernel Modules can be activated as follows,

•Kernel modules can be loaded in the kernel on demand based on user commands (we will go this later in this lecture)

•The Linux kernel supports automatic discovery of new hardware devices, and this may result in the automatic load of the associated kernel modules (using the udev subsystem in the kernel). An example is when inserting a USB flash drive

•The Linux kernel has a list of kernel modules to load at startup (via some startup scripts)

•Some Kernel Modules are needed in the boot process of the Linux Kernel, and hence they are statically built in the kernel

•Other modules are necessary for system operation, and it is decided to build them statically in the kernel (they can not be unloaded, since they are becoming part of the kernel image)


**Selecting Modules to Start at Boot (/etc/modules)**

•The file `/etc/modules` will contain the list of modules to start at kernel startup


**Inserting a Module (insmod Command)**

`$ insmod <module file>`

`$ insmod <module file> <arguments>`

•This command inserts a module in the kernel

`$ sudo insmod /lib/module/`uname –r`/my-driver.ko`

•Note that the module full path needs to be specified

•You can pass parameters to the module, these parameters are processed by the module code

`$ sudo insmod /lib/module/`uname –r`/my-device.ko debug_enable=1`

•Sometimes, a kernel module would require another module to be loaded first, the user has to take care of this dependency, otherwise, the insmod command may fail

**Removing a Module (rmmod Command)**

`$ rmmod <kernel module>`

•This command removes the kernel module from the kernel

`$ sudo rmmod my-driver`

•Since we are addressing now the kernel module inside the kernel and not its binary file inside the Linux tree, no path is specified. Just the module name

**Displaying Kernel Module info (modinfo Command)**

`$ modinfo <kernel module name>` This command shows information about the module

`$ modinfo my-driver`

•This includes,

•Full path for the .ko file

•Author

•License type

•Description of the module function

•Valid parameters

•Dependencies on other modules

**What are Device Drivers ??**

•A device driver is a kernel module

•It can be either built statically in the kernel image, or loaded dynamically

1- Automatically loaded via `udev`

2- On demand via user commands (modprobe)

3- At boot time via startup scripts

•The device driver registers itself to the system with a number (called the major number)

•The device driver runs in the kernel and performs the required functions (interacts with hardware interrupts, communicate with hardware devices, access Linux Kernel structures, communicate with other device drivers, …etc)

•The device driver supports one or more devices


**Device Classification**

•Two main classes of devices:

•Character devices

    •Serial streams of data
    
    •Read and Write operations are done in a serial manner
    
    •Examples:
    
            •Keyboard
            
            •Mouse
            
            •/dev/ones
            
            •/dev/tty1
            
            •/dev/ttyS1
            
            •Represented by a file with type “c”
            
            •Most common devices
            
•Block devices

    •Read and Write are performed in Blocks
    
    •Blocks are addressable, and hence can read in a non sequential way
    
    •Examples are:
    
           •Storage devices (hard disk, flash)
           
          •/dev/sda1
          
    •Represented by a file with type “b”
    
**Creating a Device file (mknod Command)**

`$ mknod <device file name> <c|b> <Major> <Minor>`

`$ mknod -m <permissions> <device file name> <c|b> <Major> <Minor>`

•This command creates a device file

•The device file name is the file to be created. It should be located in /dev

•The device class is either a “Character” or “Block” device

•The Major Number is the number for the device driver to attach to

•The Minor Number is the number for this device file (it should be unique within all devices attached to that device driver)

•You can deal with the device as a normal file

•It can be read only, write only, or read-write

•You can read from the file using like any file (use cat, or input redirection)

•You can write to a device file like any file (for example use echo or output redirection)

•To create a device node

```
$ mknod /dev/my-new-device c 235 1
$ mknod -m 666 /dev/my-new-device c 235 1
```

**Configuration of Serial Interfaces (setserial Command)**

`$ setserial <options> <serial device file> <parameters to set>`

•This command is used to read/write configuration of serial ports

•This includes,

•Setting the I/O port used by the serial interface

•Setting the IRQ channel used by the serial interface

•Baud rate

•Other info

•Example:

```
$ sudo setserial -a /dev/ttyS1
$ sudo setserial /dev/ttyS1 baud_base 115200
```

**Listing USB Hardware Devices (lsusb Command)**

`$ lsusb`

•This command lists the USB Hardware devices and information about them

```
$ lsusb (List USB Devices)
$ lsusb -a (List USB Devices with all information about them)
$ lsusb -t (List USB Devices in a tree hierarchy structure)
```

**Copy And Convert data (dd Command)**

`$ dd if=<source> of=<destination> <options>`


•This command copies data from one file, perform any needed conversions, and store it an another file

•It is a very useful command specially that it can use device files as either source, destination, or both

•Be cautious when using this command. It can wipe a whole partition or drive on your machine

•Example:

```
$ dd if=/dev/urandom of=~/random-data-file bs=4 count=1000
$ dd if=/dev/sr0 of=/my-file.iso bs=2048 conv=noerror,sync
$ dd if=/dev/sda of=~/disk.img
$ dd if=/dev/sda of=/dev/sdb
```

**Dump of a File (od Command)**

`$ od <Options> <file>`

•This command dumps files in different formats

•Examples:

```
$ od -x file.img (output the file in Hexadecimal format)
$ od -s file.img (output the file in decimal format)
```


## FileSystems in Linux

•In Windows,

•Each partition of each storage device will have its own separate tree.. (C, D, E,…)

•Plugging a flash or a portable hard-disk results in a new tree

•Linux has a unified File Hierarchy

•This means that no matter how many storage devices we have, we will only have one file tree

•The file tree starts with the root (/)

•There is a standard on the high level of the structure of the File Hierarchy, this structure is mostly followed by most Linux Distributions

•This hierarchy may contain sub-trees from multiple storage devices of different natures

•Hard Disk partitions

•Flash Drives

•CD/DVD Driver

•SD Card



**Manage Disk Partitions**

•The Disk can then be segmented into one or more partitions

•Each partition occupies physically a part of the disk storage area

•Partitions are isolated from each other, and each one acts as if it is a separate disk, and will have its own device file

•Why do we need to have multiple partitions ?

•This enables us to have a different filesystem type in each partition which enable the following,

•Some partitions will be read only, others will be writable

•Some partitions will have the data compressed, others will have them without compression

•Some partitions will have their data encrypted, others will have their files in clear text

•Isolation of data on different partitions,

•Corruption of one partition does not affect other partitions

•For example it is advised to have /var directory in a separate partition to make sure that explosion of log file sizes and other spoolers does not affect the system operation



**Partition Categories**

•Partitions can be:

•Primary Partitions:

   •They can be set to be bootable
   
   •You can install a bootable OS on it
   
   •Count is limited
   
•Logical Partitions:

    •Can not be bootable
    
    •No OS can be installed on them
    
    •Only useful to carry data
    
    •Still they provide isolation of data
    
    •They result from the segmentation of a primary partition (named an extended partition) into multiple logical partitions
    
•Swap Partition

**SWAP Partition**

•The SWAP partition is a partition that is only accessible by the system

•The system use one or more swap partitions to extend its physical memory

•In case of high memory utilization, memory pages that is not accessed frequently can be moved from the physical memory into the swap partition

•However, the access time for it is much higher than that of memory

•User can not access this partition or put his own filesystem in it

•It is recommended to have swap space double the amount of physical memory in the system

•An example on a system with 512 MB of RAM:

•1st possibility: one swap partition of 1 GB

•2nd possibility: two swap partitions of 512 MB

•3rd possibility: with two hard disks: 1 partition of 512 MB on each disk. This last option will give the best results when a lot of I/O is to be expected

•In general, using multiple swap partitions will speed up access time (specially if they are located at different physical storage devices)


**Partition Table**

•The Partition table is a table located at a known place in the disk

•It contains description of the partitions on the disk

•Start Location

•Length (or End Location)

•Type (Primary/Logical)

•Other Info

•There are multiple formats for the partition table, most popular are,

•Master Boot Record (MBR)

    •Supports disks up to 2 TB size
    
    •Supports up to 4 Primary partitions (maximum of 4 OS’s in a multi-boot environment)
    
•Most common format

   •GUID Partition Table (GPT)
   
   •Supports disks of much larger size
   
   •Supports more primary partitions (up to 128)


**Partition Table Example (GPT)**  

![image101](https://github.com/user-attachments/assets/20f65bf8-4565-4748-a03b-b63e4a7d845c)

![image102](https://github.com/user-attachments/assets/95714325-8f9c-4efb-8705-66e7b01b6865)


**Manage Disk Partitions (fdisk Command)**

`$ fdisk -l`

`$ fdisk <device Name>`

•This command is responsible for displaying and management of disk partitions

```
$ sudo fdisk -l
$ sudo fdisk -l /dev/sda
$ sudo fdisk /dev/sda
```

•Using this command you can,

  •Display disk partitions
  
  •Create new partitions

  •Delete existing partitions

  •Change the size of existing partitions

•This is achieved by reading/writing in the partition table

•Note that fdisk does not support the GPT partition table format, for that use the parted command


**File-System Types**

•There are different types of file systems

•We select the most suitable type for our needs based on,

•Storage Media type (hard disk, flash memory, network, …)

   •Read only or Read/Write
   
   •Supported File Sizes

   •Optimize for Performance

   •Optimize for file Sizes (performs Compression)

   •Optimize for Security (Performs Encryption)

   •Supports data recovery after failures (Journaling)

   •Other Criteria
   
•There are some filesystems of special nature (such as procfs, sysfs)

•Some of the commonly used filesystem types are (ext2, ext3, ext4, NTFS, FAT, JFSS2, NFS, …)



**Root FileSystem**

•The Root FileSystem is the filesystem that contains all the necessary files that is needed to start the system and make it operational

•It is mounted at startup of the kernel

•The mount point for the root filesystem is “/”

•This filesystem can not be un-mounted during operation

•Other Filesystems can be mounted and un-mounted after the root filesystem is mounted


**Mounting a filesystem**

•When we mount a filesystem, we specify the mount point

•The mount point is the directory where we want to access the filesystem

•Before performing the mount, the directory need to be an empty directory

•Once, we perform the mount, the directory will contain the contents of the filesystem



**View Mounted File-Systems (mount Command)**

```
$ mount
$ mount -l
$ mount -l -t <fs Type>
```

•This command displays the mounted filesystems along with their info including their mount point and associated device

`mount -t <fs Type> <device> <mount point>`

•This command mounts the filesystem (of a certain type) for a certain block device file to a mounting point

•Examples:

```
$ sudo mount -t ext4 /dev/sda1 /home/aelarabawy/project/
$ sudo mount -t iso9660 -o ro /dev/sr0 /mnt
```

**(umount Command)**

`$ umount <device>`
`$ umount <mount point>`

•This command unmounts the filesystem that was previously mounted. The filesystem can be identified by its,

•Associated device (example /dev/sd1)

•Associated mount point (example /mnt/SdCard)


**/etc/fstab File**

•The /etc/fstab file contains a list of filesystems along with their description

•Mount point

•Associated device

•Filesystem type

•This file can be utilized by the mount command,

•To mount a filesystem that is listed in /etc/fstab you don’t have to list all its info, it is enough to specify its device name or its mount point

`$ sudo mount /dev/sd2`
`$ sudo mount /mnt/my-SD-Card`

•The mount command will read the rest of the information from the **/etc/fstab** file

•To mount / unmount all filesystems listed in /etc/fstab

```
$ sudo mount -a
$ sudo umount -a
```


















