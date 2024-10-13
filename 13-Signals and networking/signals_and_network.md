## Using Signals

**What is a Signal ??**

•Linux has two planes:

1- Kernel Plane: Has access to system and hardware resources
2- User Plane: For applications to run on

•User applications don’t have direct access to the kernel

•For a user application to communicate with the kernel, it needs to use a `System Call`

•What about if the kernel needs to send a request/command/notification/… to the user application ??

•The used mechanism is `Signals`

•So, Signals are the mechanism that the kernel uses to communicate with the user applications

•Signals are also used between user applications (when one application needs to send a request/command to the other application)


![image](https://github.com/user-attachments/assets/2a49071e-9152-4f5c-8bbb-6c6f056c47bd)


•Signal is the communication channel used by the Linux Kernel to communicate with a process running in the user plane

•This can be used by the kernel to kill a process, stop it, resume it, notify it of a timer expiry, etc…
•Signals can also be sent by another process running in the user plane. Examples,

•When the user presses `Ctrl-c to` terminate the running application, or `Ctrl-z` to stop it

•When the user uses the command `bg` to resume a stopped application in the background, or fg`` to resume it in the foreground

•When the user uses the `kill` command to terminate a running application

•In all of these cases, a signal is sent to the destination application to achieve the required task

•When sent by another user application, it is first passed to the kernel in a system call, which in turn passes it back to the desired process

•Signals are described in both Unix Systems and POSIX Standard

•There are a table of signals. Each signal has,

•Signal number

•Signal name (starting with ‘SIG’)

•Signals with numbers (1-31) are normal signals

•Signals with numbers > 31 are called “Real Time Signals”

**Passing a Signal to a Process (kill Command)**

```
$ kill <pid>
$ kill -<Signal number> <pid>
$ kill <Signal name> <pid>
```

•The kill command passes a signal to the desired process

•Note that, despite that the command name is `kill`, it is used for all types of signals even those that have different purposes and not just used to kill processes

•If no signal is specified, then the signal `SIGTERM` is assumed by default

•Examples:

```
$ kill -9 1185
$ kill SIGKILL 1185
```

**Selecting Processes by name (killall Command)**

`$ killall <Signal> <command name>`

•The command `killall` sends the desired signal to all processes running the specified command

`$ killall chrome`

•This is useful when you need to pick a process without searching for its pid

•Also useful when you need to send the signal to all instances of the running program

•If no signal is specified, `SIGTERM` is assumed

•Example:

`$ killall -9 gedit (this sends a SIGKILL signal to all “gedit” instances)`

**Selecting Processes by Other Criteria (pkill Command)**

```
$ pkill <signal> -u <username>
$ pkill <siganal> -P <Parent process>
$ pkill <signal> <pattern for command>
$ pkill <signal> -t <Terminal name>
```

•The `pkill` command sends the desired signal to processes that match different criteria

•Examples:

•Send a SIGTERM to all processes owned by user tom `$ pkill -u tom`

•Send a SIGSTOP to all processes running under tty1 terminal `$ pkill SIGSTOP -t tty1`

•Send SIGTERM to all children of process with pid 1107 `$ pkill –P 1107`

**Killing GUI Processes with the Mouse (the xkill Command)**

`$ xkill`


•The xkill command allows the user to select the process to kill with the mouse

•Type the command, then click with the mouse on the UI of the process you want to kill

•If a GUI app is hanging, and you need to kill it but unable due to the hanging screen

•get into a Linux virtual terminal via, `[Ctrl] [Alt] [F1]`

•From the virtual terminal, issue the proper “kill” command `$ killall -9 chrome`

•After you are done, get back to the tty-7 (for the X window) `[Alt] [F7]`


**Keyboard Hot keys**

•Some signals are triggered by the user by typing special hot-keys

•When the kernel detects these hot-keys, it sends the proper signal to the running process (or process group)

•Examples:

```
•Ctrl-c triggers SIGINT
•Ctrl-z triggers SIGTSTP
•Ctrl-\ triggers SIGQUIT
```

**Request from another process**

•A process can trigger the kernel to send a signal to another process by issuing a system call

•Examples for this is when the user issue the commands from the terminal

```
$ kill (triggers sending the desired signal, SIGTERM by default)
$ fg (triggers sending the signal SIGCONT)
$ bg (triggers sending the signal SIGCONT)
```

•A process can also trigger sending a signal to another process programmatically via some special function API


**Death of a Related Process**

•When a process terminates, the kernel sends the following signals,

•A `SIGHUP` is sent to all children processes to inform them about the death of their parent process

•A `SIGCHLD` is sent to the parent of the terminated process to inform it about the death of a child process


**Errors and Exceptions**

•Some exceptions within the process triggers the kernel to send signals to the process,

•Examples:

•If the process tries to execute an illegal instruction, the kernel is triggered to send `SIGILL` signal to it

•If the process suffers from a Floating Point Exception, the kernel sends it a `SIGFPE`

•If the process tries to write to a pipe while the other end is not listening, the kernel sends it a `SIGPIPE`

•If the process accesses a Null Pointer (or other memory exceptions), the kernel sends it `SIGSEGV`

•If a process running in the background tries to read/write to the standard input/output, the kernel will send it a `SIGTTIN/SIGTTOU`

•If the process exits on error using the abort(), the kernel will send it `SIGABRT`

## Process Response to Signals

Default Action
•When a process receives a signal, the normal behavior is to execute the default action

•Each signal has its own default action that is part of its description

•Examples:

•Some signals have the default action of termination (graceful termination). This is applicable for several signals such as SIGTERM, SIGPIPE, SIGUSR1, SIGUSR2, …

•Some signals have the default action of termination with generation of a core dump (stack trace for further debugging). This action is useful for signals that indicate some error in the process operation such as SIGSEGV, SIGILL, SIGABRT, SIGQUIT …

•Some signals have the default action of being ignored by the process such as SIGCHLD

•Some signals does not allow the process to change its default action. This means that the default action is the only allowed action. This includes the SIGSTOP which force the process to stop (suspend) and SIGKILL which force the process to terminate immediately

**Ignoring a Signal**

•A process can set itself to ignore certain incoming signals, accordingly no action is performed when these signals are received

•Some signals can not be ignored such as SIGSTOP, and SIGKILL


**Blocking a Signal**

•A process can set itself to block a certain set of signals

•Blocking a signal means, keeping it in a queue for later handling (when the blocking is taken away)

•This is used when the process is executing some code that should not be interrupted by the incoming signals

•Every process has a mask of which signals to block

•Only one signal of a certain type will be blocked (other instances will be dropped).

•This last rule does not apply to real time signals (signals with numbers > 31)

•Some signals can not be blocked (SIGSTOP and SIGKILL)

**Catching the Signal**

•A process can “catch the signal” before its default handler executes, and pass it to a special handler

•This is specially useful for some of the signals that have their default action of being ignored (such as SIGCHLD)

•Some signals can not be caught (SIGSTOP and SIGKILL)

## Popular Signals

**Hang-Up Signal (1) SIGHUP**

•The hang-up signal is used by the kernel to inform the processes running in a tty session when the session closes. This can be due to,

1- The modem for the session disconnects
2- The network connection used to connect to the machine breaks

•It is commonly used to request daemon processes to re-read their configuration file

•Default action for this signal for the process to terminate


**Interrupt Signal (2) SIGINT**

•Interrupt signal is triggered when the user uses the hot-key `Ctrl-c`

•This causes the kernel to send `SIGINT` to the currently running process group

•The default action for this signal is for the process to terminate


**Quit Signal (3) SIGQUIT**

•The quit signal is triggered by the user when he uses the hot-keys `Ctrl-\`

•This triggers the kernel to send `SIGQUIT` to all processes in the currently running process group

•Default action is for the process to quit and generate a core dump file (to be used for debugging)


**Illegal Command Signal (4) SIGILL**

•The illegal command signal is triggered when the process program tries to execute an invalid instruction

•This may occur in the case of memory corruption of the code area or in stack memory

•Default action is to terminate and generate a core dump file

**Trap Signal (5) SIGTRAP**

•The trap signal is normally used with debuggers and program tracers

**Abort Signal (6) SIGABRT**

•The abort signal is sent by the kernel to the process when it calls the `abort()` function to indicate an erroneous exit of the program

•The default action is to terminate and generate a core dump file


**Bus Error Signal (7) SIGBUS**

•The bus error signal is triggered by an error in the program in which an attempt was made to access memory incorrectly

•This can be caused by alignment errors in memory access

•The default action is to terminate and generate a core dump file

**Floating Point Exception (8) SIGFPE**

•The floating point exception signal is sent by the kernel to the process when it falls into an exception while running a floating point instruction

•The default action is to terminate and generate a core dump file

**Kill Signal (9) SIGKILL**

•The process was explicitly killed by a request from a different process

•The request is to kill the process immediately and forcibly without giving it a chance to clean-up

•A process can not ignore, block, or catch this signal

**Stop Signals (17 &18) SIGSTOP & SIGTSTP**

•SIGTSTP (terminal Stop) is triggered by pressing Ctrl-z

•This signal causes the process (or process group) to suspend operation

•SIGSTOP has the same effect with the only difference that it can not be ignored/blocked/caught by the process while this is possible with SIGTSTP

•Upon stopping due to either SIGSTOP & SIGTSTP, the process awaits SIGCONT to resume operation


**Terminate Signal (15) SIGTERM**

•The terminate signal is the default signal for the kill command when no signal is specified

•The default action for SIGTERM is to gracefully terminate the process (process group) after clean up


## Networking in Linux


**Network Interfaces**

•The computer/board may have one or more network interfaces

•In Hardware, this is represented by,

1- An Ethernet NIC card

2- WiFi port

•In Linux, each interface will have a name,

•Examples (eth0, eth1, …. )


**Showing the Network Interfaces (ifconfig Command)**

`$ ifconfig`

`$ ifconfig <interface name> [up/down]`

•This command is responsible for showing and managing interfaces

•To show the interfaces in the system

`$ ifconfig`

`$ ifconfig -s (shows an abstract description)`

•To show info about a specific interface `$ ifconfig eth1`

•To activate/deactivate

`$ ifconfig eth1 up`

`$ ifconfig eth2 down`

**The MAC Address**

•The MAC address is also called the Hardware Address

•It is a unique address for each NIC card (set by the manufacturer)

•It is a 48 bit number written in hexadecimal format (4 bit digits) as follows, 68:05:CA:03:19:9C

![image923PNG](https://github.com/user-attachments/assets/b47ec65b-9ef0-49ab-ab33-5c0d86c2e122)


**Local Area Network**

•A Local Area Network (LAN) is a set of computers connected together via hub/switch

•The devices (computers) are located in the same area (locally located)

•The computers have the same type of network interface (Ethernet, Wifi, …)

•Data is transferred between the machines based on their MAC addresses


**IP Address**

•Any network interface on a machine in the network is identified by its IP Address

•Sometimes the interface may have multiple IP-Addresses

•The IP address is composed of 4 numbers (0-255) separated by a dot

•Example: 192.168.101.112

•This is assuming, we are using IPv4, another version which is IPv6 has a different format

•Note that the number 0-255 is an 8 bit number

•Port numbers identify different services within the same IP Address

•Each connection will have both source port and destination port numbers

**Subnet**

•Network interfaces within the same subnet share the upper part of the IP address, and differ in the lower part

•The number of bits shared within the subnet control the subnet size

•For example if we have the upper 24 bits (3 bytes) shared within the subnet, then the 
interfaces with the subnet can differ in 8 bits only, which leads to a maximum of 256 addresses

•If the shared part is reduced to 20 bits only, we will have 12 bits to change which lead to 4096 different addresses

•The part of the IP Address shared among the interfaces within the subnet, is expressed as the subnet mask

![image99](https://github.com/user-attachments/assets/c77733d2-a542-4c72-a70c-466c08702309)

**Show Subnet Mask (ifconfig Command)**

**$ ifconfig**

```
$ ifconfig <interface> <IP Address>
$ ifconfig <interface> <IP Address> netmask <netmask>
$ ifconfig <interface> netmask <netmask>
```

Used to statically allocate IP address to an Interface and/or set its net-mask

•Example:

```
$ ifconfig eth1 192.268.0.10
$ ifconfig eth1 netmask 255.255.255.224
$ ifconfig eth1 192.268.0.10 netmask 255.255.255.224
```






**IP Address Allocation**

•IP Address can be allocated in two different ways,

•Statically allocated

1- This is done manually, or via a startup script

2- Address is always the same

•Dynamically allocated via a `DHCP server`

1- At startup, the machine asks a DHCP server to provide it with an IP Address

2- The DHCP server responds with an unused IP address within the proper subnet

3- Hence, the IP address can change every time the machine boots

4- The DHCP server can be configured so it will always assign a specific machine the same IP Address

•Using DHCP address allocation is more convenient and more flexible

•Since the DHCP server needs to be accessed before the IP address is allocated, it should reside within the same LAN as the machines (it is typically located inside the LAN switch)

**Special IP Addresses**

•Some IP Addresses have a special meaning,

•The Address `127.0.0.1` is reserved for the Local Host. This means it is used as a loop back address

•Any address ending with all ones (after the subnet mask), is a broadcast address within this subnet

•Example,

In the Subnet 192.168.224.0/19 the broadcast address would be, 192.168.255.255

•Any address of the format xxx.xxx.xxx.1 is reserved for the default gateway


**So How is Routing Done ??**

•First the destination address is checked to be within the same subnet of the sender or not

•If it is on the same subnet,

1- Then delivering the packet will need to be done based on the `MAC address`

2- This means we will need to know the MAC address of the destination

3- We will not need this now, since the destination address does not belong to the sender subnet

•If it is not on the same subnet,

1- Then we will need to deliver the packet to the proper next hop

2- The next hop is identified based on the Routing Table

3- the routing table is a table of routes that identifies the next hop based on the packet destination

**Show the Routing Table (route Command)**

`$ route ` The route command shows the entries of the routing table

•Each route contains,

•Destination: This is an address, whether a host address or a subnet address

•Network mask: Used when a subnet address is used for destination

•Interface: The used interface for this destination

•Gateway: The next hop for this destination

•Upon the reception of a packet,

•Linux tests the packet destination address to match the destination of the routes

•If a match exists, Linux forwards the packet to the defined interface, towards the specified GW address

```
$ route add <address> dev <interface> gw <address>
$ route add default gw <address>
$ route del <address>
$ route del default
```


•To add a route

```
$ sudo route add 192.56.76.123 dev eth1 gw 192.168.101.1
$ sudo route add -net 192.56.76.0 netmask 255.255.255.0 dev eth0
$ sudo route add default gw 192.168.101.1
```

•To delete a route
```
$ sudo route del default
$ sudo route del 192.168.100.20
```
•Now the router has received the packet

•It should also check its routing table to identify the proper interface to use for forwarding the packet

•The destination is found to belong to the subnet 141.14.2.0/24, and the interface is identified

•Now we need to deliver the packet to its destination within the subnet

•Since delivering the packet within the subnet is based on the MAC Address, we will need to know the MAC address of the destination

**Identifying the MAC Address … (The ARP Protocol)**

•The machine should have a table that maps IP Addresses to MAC addresses within its subnet

•This table is called the ARP table

•If the machine does not have the address in its table, it queries it using the ARP protocol (Address Resolution Protocol)


**Manage the ARP Table (arp Command)**

```
$ arp
$ arp -s <IP Address> <Hardware Address>
$ arp -d <IP Address>
```

•The arp command is responsible for display and management of the ARP table

•To Display the ARP Table `$ arp`

•To manually add an entry to the ARP Table (normally ARP Table entries are filled by the ARP Protocol)

`$ sudo arp -s 192.168.101.105 00:0C:F1:AC:34:F1`

•To manually delete an entry to the ARP Table (normally ARP table entries expire automatically)

`$ sudo arp -d 192.168.101.105`

**Network Address Translation**

•NAT (Network Address Translation) is used to hide internal network from the rest of the network to,

•Reduce the required number of administered IP Addresses

•Protect the internal network from access from the external network

•The NAT Router builds a mapping table between the Internal addresses/ports, and its own 
address/ports (or from some list of administered addresses)


**Domain Names**

•When accessing a server, it is normally identified by a domain name instead of IP Address,

•More readable (www.google.com instead of 134.11.234.102)

•Better portability (we can change the server IP Address)

•Enable High Availability (Using a standby server in case of failure)

•Enable Load sharing (Distribution of load among multiple server)

•We need a way to convert the domain name into the IP Address

•This is achieved through **DNS Server**


**Setting DNS Server Info (/etc/resolv.conf)**

•To set the set of name servers to search for mapping Domain names to IP Address, edit the file /etc/resolv.conf

•Name servers are specified as followsو nameserver 208.67.222.222 nameserver 208.67.220.220

•Any changes made to the file will take effect immediately

**Resolving Domain Names (host command)**

`$ host <Domain Name>`

•This command is used to lookup a domain name and return with its IP Address(es)

•Example:

`$ host www.google.com`

•Note that the dig command can do a similar job
`$ dig www.google.com`












































