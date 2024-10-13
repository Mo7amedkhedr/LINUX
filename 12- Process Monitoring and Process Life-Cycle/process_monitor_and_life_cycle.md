## Process Attributes

`Process Id (PID)` A unique identification number used to refer to the process

`Parent Process ID (PPID)` The process ID of the parent process

`Process Group ID (PGID)` The ID for the process group that this process belong to. Will be equal to PID if the process is a Process Group Leader

`Session ID (SID)` The ID for the session that this process belong to The same for the PID if this process is the Session Leader

`Terminal Number` The number of the terminal that is associated with the process. Only applicable for interactive processes. Batch processes and Daemons have the value of 0


**Process Priority**

•Each process will have a priority value

•The process priority affects the scheduler behavior in the Linux Kernel

•A Process with higher priority may,

```
•Receive more processor time by the kernel
•Get scheduled more often
•Preempt processes with lower processes
```

•Process priority is defined by,

```
•User Controlled value (nice Value)
•Kernel calculated value (based on the process behavior)
   •Processing bound
   •I/O bound
```

**The “nice” Value**

•This is a value between -19 to 20 assigned by the user

•The kernel uses this value as a factor in calculating the process priority

•The higher the “nice” value of the process, the more it is accommodating other processes (less aggressive), which means lower priority


![image95](https://github.com/user-attachments/assets/b8dbc517-a186-4754-9cd3-97e3145851eb)


**Set Process Priority (nice Command)**

`$ nice -<value> command`

`$ nice -n <value> command`

This command sets the nice value to manipulate the process priority

•To increase priority, nice should be decreased and vice versa

1-nice value vary between -20 to +19

2-Default nice value is “0”

•Example:

```
To set nice to value 5 for a new process,
$ nice -5 processCommand &
$ nice -n 5 processCommand &
```

```
•To set nice to value -10 for a new process
$ nice --10 processCommand &
$ nice -n -10 processCommand &
```

•Note: non-root users can only do 1-19 nice values


**Modify Process Priority (renice Command)**

`$ renice <value> <pid of process>`

This command changes the “nice” value of a process

Example:

$ renice 10 1002

•Non-root users can only increase the processes nice value (decrease its priority)

•The passed value is the new nice value and not a increment/decrement value

**Displaying Process Info**


![image96](https://github.com/user-attachments/assets/34344adf-5d82-4c4e-9f8a-ab126e3aed90)


**Display Process Info (ps Command)**

`$ ps <options>`

Display Information about the running processes

•The ps command is a very powerful and diverse command

•It has a lot of options to change the ways to display process info,

1- Some options are used to define the scope of which processes to show

2- Other options are used to define the format of the listing and which information to show


`$ ps` Display info about processes under the current shell

```
$ ps -e
$ ps -A

Display all processes in the system
```

`$ ps a` Display all processes in the system except those which are not attached with a terminal

`$ ps ax` Display all processes in the system including those which are not attached with a terminal


You can use different options to define the format of the output (what columns to show)

•Some of the common usages

`$ ps -f`

`$ ps -F`

•To specify which fields to show use “-o” option

`$ ps -o pid,ppid,pgid,sid,command`

```
$ ps aux
a : don’t limit to same tty but have to be attached to a tty
x : Remove the tty restriction
u : Long Format (more fields)
```






























