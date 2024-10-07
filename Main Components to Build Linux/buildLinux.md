# Main Components to Build Linux

Toolchain , Bootloader , Kernel , Rootfs



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
