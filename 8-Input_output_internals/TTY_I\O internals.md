## TTY Device

![image63](https://github.com/user-attachments/assets/62284f92-1708-466f-8a37-7e7da789fa64)


![image64](https://github.com/user-attachments/assets/72bb55d2-384e-4270-9bdc-9d61ad443d2f)

**TTY Devices**

•TTY stands for TeleTYpewriter

•TTY machines were used originally in stock tickers, and Telex Machines

•When Computers were introduced, a computer was a big central unit, TTY machines were used as an I/O terminal, and connect to the computer via UART (Serial Interface)

•In case the terminal is remote, a modem pair were used

•Unix supported all of this via the introduction of TTY subsystem in its kernel

•TTY device is composed of 3 blocks:

     •A driver to the hardware interface(UART driver, USB driver, VGA/KB drivers, ..)
     
     •Line Discipline to handle low level editing commands (backspace, erase word, clear line, …. )
     
     •TTY driver to interface with the user space applications
     
•The User space application communicates with the TTY driver via system calls and signals

•The default I/O Streams of the user application is the assigned TTY device (/dev/tty*)

•This TTY Terminal is also the controlling terminal for its user applications

## VIRTUAL TERMINALS

•When we were connecting terminals via the serial interface, we were able to have multiple terminals to the computer

•However, when we connect the monitor and keyboard directly to the PC, and use the same architecture, we can not have multiple terminals (only one monitor/keyboard pair)

•We need a new architecture that will enable us to run multiple terminals from the same Physical Terminal(Keyboard/Monitor)

•This led to the introduction of the concept of Virtual Terminals in Linux


![image65](https://github.com/user-attachments/assets/c762c1f6-748b-4e13-9667-ac10a2b759b1)


![image66](https://github.com/user-attachments/assets/08ed820c-999f-434b-8534-07da4500636f)


**Virtual Terminals**

•A new architecture is used to be able to have multiple terminals on the same machines (with the same physical terminal)

•The Monitor/Keyboard drivers are no longer part of a TTY device, they are now separate devices

•Linux kernel provides up to 63 virtual terminals (VT) (/dev/tty1 up to /dev/tty63)

•Most distributions initialize only 7 VTs (/dev/tty1 - /dev/tty7)

•On each of these VTs, the user app `getty` is started. This program is responsible for user login

•All VTs are active, but only one have access to the Physical terminal (Monitor/Keyboard)

•To switch between different VTs, use` ALT-Fn` to go to the `VT#n`


**Linux GUI**

•We need to have, Windowing (Multiple windows, maximize, minimize, ...)

•Fonts, colors, icons , Handling of mouse actions and Displaying of Graphics

•For performing all of these tasks, Linux uses `X-Window System` 

•The `X-Window System` (also Called `X system`, or`X11 System`) is a Windowing system for bitmap displays

•It is composed of:

•`Server (X-Server)`:

•A user application that is responsible for handling the Graphical User Interface and connecting to the drivers

•Most Linux distributions use the `Xorg` application for this

•`Client (X-Client)`

•The client part lives in every user application that needs to use the GUI The user app connects to the Xserver using the `X Protocol`


## X-Server and VTs

•As mentioned before, Linux distributions, initialize some VTs to run getty for user login (most Distributions use /dev/tty1 to /dev/tty6 for that)

•The X-Server is started on at least one VT (normally /dev/tty7). This is X-Session # 0

•Some Distributions start the X-server on multiple VTs (so we get multiple X-Sessions)

•A User can add more X-Sessions or stop X-Sessions if needed. Remember, the X-Server, is just a User application that is started on one of the VTs

•Since Alt-Fn has some meaning for the GUI, to move from the GUI to another VT, use Ctrl-Alt-Fn instead

•So assuming we have X-server running on /dev/tty7

     •To move to VT#1 --.> Ctrl-Alt-F1
     
     •To move back to the GUI --> Alt-F7


![image67](https://github.com/user-attachments/assets/9418fabd-9374-4e39-b0b2-9280221214c3)


![image68](https://github.com/user-attachments/assets/5609c1eb-e3d2-407c-9f05-6199159d7417)


![image69](https://github.com/user-attachments/assets/01c149ca-e689-4a32-9a07-003e4369de25)


## Emulated Terminals


•The next step is to use an emulated terminal from the GUI

•This means, to have an X-App that acts as a terminal

•There exists some terminal emulators that run as X-clients such as,

•xterm

•Konsole (in KDE)

•gnome-terminal (in GNOME)

•To support this concept, the Linux Kernel introduces the concept of Pseudo Terminals (PTY)


![image70](https://github.com/user-attachments/assets/ed27eef9-b26c-43ec-b4a4-698157f75184)


![image71](https://github.com/user-attachments/assets/2ab764cc-e6d5-43a7-a3ca-28760f5f046e)


## Running a Shell Command


![image72](https://github.com/user-attachments/assets/f4cab96d-30f5-411f-aba3-69aac5617f81)


**Redirecting stdout to a File**

![image73](https://github.com/user-attachments/assets/4d4ed7c6-2546-45a4-a168-e21f2f37e465)

![image74](https://github.com/user-attachments/assets/ee8f91aa-4b9d-4d05-b866-70ab964738a3)


![image75](https://github.com/user-attachments/assets/0099d629-0c5e-4f9b-a354-55c94480ea5e)

![image76](https://github.com/user-attachments/assets/d41893c6-170a-4f08-9f93-0d11921c5356)

![image77](https://github.com/user-attachments/assets/f9aeef99-36d8-4aaf-93ed-f9f6400a279d)

![image78](https://github.com/user-attachments/assets/d598d004-b549-48dd-bb86-6926e87d9a66)


![image79](https://github.com/user-attachments/assets/5ffdf0b1-88b0-4597-8cea-586d2e592842)


![image80](https://github.com/user-attachments/assets/7e61300a-f994-4082-88ef-befb1f035b61)


![image81](https://github.com/user-attachments/assets/6bc42c14-930d-45a8-b459-4fcdbcc2749c)


![image82](https://github.com/user-attachments/assets/57ec9690-d55e-470c-9c52-987199dcc7fc)


![image83](https://github.com/user-attachments/assets/f78d786d-5731-4b1a-aa3a-ec3a874d6550)


## screen Command

```
$ screen
$ screen -r
```

•The screen Command is an Emulated Terminal Manager

•It enables the user to create multiple emulated terminal sessions (Ctrl-A c to create a new session)

•It then enables the user to move between the different sessions (Ctrl-A n to move to next sesseion)

•The user can detach the screen command from its controlling TTY (Ctrl-A d).

•This is a very useful tool, now the controlling terminal can close without affecting the sessions running under screen

•To regain control of the screen sessions, perform

$ screen -r













