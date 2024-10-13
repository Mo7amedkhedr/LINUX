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

**Showing Threads**

•To show threads for multithreaded applications, use one of the following options

```
$ ps -H
$ ps -L
$ ps -T
$ ps -m
```

A common practice, is to do a full listing and pipe the output to a search filter to limit the list to what we are interested in

`$ ps -ef | grep root ` This shows all processes owned by the root user


`$ ps aux | grep “pts/2”` This shows all processes attached to the tty pts/2

**Display Process Resource Usage (top Command)**

`$ top `  Displays a dynamic view of the resource usage of system processes

**Manipulating Output**

```
•While the “top” tool is running,
•Push ‘M’ to sort by memory usage
•Push ‘P’ to sort by CPU processing usage
•Push ‘T’ to sort by Time
•Push ‘k <pid>’ to kill process by its pid
•Push ‘h’ for getting a help page for all options
•Push ‘H’ to enable/disable showing threads separately
•Push ‘q’ to quit the tool
```

**Display System Resource Usage (vmstat Command)**

`$ vmstat` The ‘vmstat’ Command displays the system resource usage

**Display Memory Usage (free Command)**

`$ free <options>` This command displays amount of free and used memory in the system


## PROCESS CREATION

**Fork-Exec Procedure**

•Creating a new process happens in two steps

•Fork:

In this step the new process (child process) is created and inherits its features from its parent

•Execute:

In this step the new process (child process) separates from its parent and move on with its functionality

**Fork**

•The Job of “Fork” in is to create a new process (child process) and prepare it with what it needs to be able to run….

•This includes,

•Assign it a new pid

•Creates associated Structures in the Kernel

•Sets the ppid, pgid, sid, and any other attributes

•Add it to the Kernel scheduler queue to give it time slots to run

•Copy parent memory space (all memory associated with the parent process) to the child process memory space

•Copy Other parent process resources,

•Normal file handlers

•Socket handlers

•Shared memory handlers ...

**Exec**

•The job of “Exec” is to send the child process on its own to do its assigned job

•This means the child process will be loaded with,

•New memory space instead of its parent

•Will lose access to parent process resources

•A pointer to the new program to run

•This command separates the child process from its parent, and the child process runs now on its own, using its own memory address space, and running its own executable and 
creating/reserving its own system resources


**Process Vs. Thread**

•Both processes and threads are threads of execution that enable parallel operation (multi-tasking) with the help of the scheduler in the kernel

•In both cases, the Linux kernel assigns time slots for the process/thread to execute before another one is assigned

•In Linux a thread is a process with some special differences:

1- When creating a thread, the address space (and some other resources) are not copied from the parent. They are shared with the parent

2- This means threads run within the same address space of its parent and never get a new address space

•Other than that, threads are treated exactly the same as processes

1-For example the kernel scheduler deals with each thread independently

•So, threads created by the same process are multiple processes that share the same address space and resources of their parent process

**Process Termination**

•A process is terminated by

1- Normal termination (reaching the end of its operation)

2- Receiving a Signal that cause it to terminate itself

3- Terminated by the kernel

•When the process is terminated, some of its resources are not yet released, and it changes its state to the `Zombie` state.

•The parent process must be waiting for its children processes to perform the required cleanup of resources

•Once the parent process perform the required cleanup, the process state is no longer in Zombie

•This is why every process must have a living parent, and if its parent process terminates, the child processes are re-parented to the `init` process

**Process States**


![image97](https://github.com/user-attachments/assets/3c9fff62-a96b-43b6-9c01-80b6f88512f3)























