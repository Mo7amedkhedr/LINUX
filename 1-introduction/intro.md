# Understanding Linux
**With CLI More Control**
* do things you can never reach with GUI 
* Faster, one command can do the effect of several menus, and mouse clicks
* Enable automation and scripting
  
**GUI makes easy tasks easier…. But CLI makes difficult tasks possible**

## Basic Concepts and Commands
* Creating Directories
* Moving and Renaming
* Creating Links and Shortcuts
* Navigation and moving around
* Deleting Files and Directories
* Moving and renaming
* Learinging about the Shell
* Composite Commands
* Basic Text Handling
* Environment Variables
* Searching for Files
* Archiving & File Compression
* Users & Permissions
* Process Management
* Sending Signals
* Package Management
* Regular Expressions
* Networking
* FileSystems

## What is Linux?
* Linux is an open-source operating system linux=kernel.
* Created by Linus Torvalds in 1991 as a hobby project.
* It's the heart of various Linux distributions (distros).

## Features of Linux
* **Open Source**: Source code is freely available and can be modified.
* **Portability**: Runs on various hardware platforms.
* **Multi-User and Multi-Tasking**: Supports multiple users and processes.
* **Networking**: Excellent support for networking protocols.
* **Security**: Strong security features and access controls.

## Why Choose Linux?
* **Cost**: No licensing fees, making it cost-effective.
* **Customization**: Highly customizable and adaptable to different needs.
* **Stability**: Known for stability and reliability.
* **Community**: Large and active community for support and collaboration.
* **Development**: Extensive development tools and libraries available.
* Large device drivers coverage -GPIO OF Raspberry pi
* Hosting huge number of languages & libraries

## What is the Embedded Linux ?
* Embedded Linux is the `customization` of Linux on Embedded target .
* Adapting the Linux kernel and customizing the user-land libraries and utilities to Embedded applications.

![image1](https://github.com/user-attachments/assets/2d6f5a8c-b666-4042-84ec-d018c3184806)



So Due to its ease of customization, Linux has been shipped in many embedded devices (smartphones, network devices, PDAs, IVI, GPS devices).


## Prerequisites for Hardware to Support Embedded Linux

### Processor Architecture
* The hardware target must use a processor architecture supported by the Linux [kernel.
*  Common architectures include ARM, x86, MIPS, PowerPC, etc.

### Memory & Storage
* For minimal, you may need around 64MB to 128MB of RAM.
*  For a basic graphical user interface (GUI) environment, you may need at least 256MB to 512MB of RAM.
* MMU

### Bootloader
* A bootloader like U-Boot is needed to load the Linux kernel into memory.
*  Bootloader configuration must match the hardware specifications.
### Kernel Support
* The Linux kernel must have drivers for the hardware components on the target.
* Without proper drivers, the hardware won't function correctly.
* Device Tree is supported
### Toolchain
* A cross-compilation toolchain is required to build software for the target platform.
* Toolchain includes compilers, libraries, and utilities for the target architecture.
### Power Management:
* Linux systems require power management features for sleep, suspend, and wake-up operations.The MCU should support power management mechanisms to conserve energy. 

