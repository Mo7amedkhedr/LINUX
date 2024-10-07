# Main Components to Build Linux

Toolchain , Bootloader , Kernel , Rootfs

![image2](https://github.com/user-attachments/assets/5efa63ff-6c22-4c98-be0a-d9428489270a)


## Booting Sequence 
### 1- PC Power on 
### 2- BIOS
```
1- POST
2- initial HW Drivers [screen, keyboard,...]
3- check HW Functionality
4- check portable device
5- check short circuit
6- LOAD (MBR/GPT) 
```
### 3- MBR ( Master boot record ) ---> First stage bootloader
```
Located in the 1st sector of the bootable disk. Responsible for loading and executing the GRUB boot loader. Contains information about GRUB
```

