
## Simple Utilities

**Advanced Navigation Commands**

![image53](https://github.com/user-attachments/assets/8b5d8645-e290-4f5b-8d84-584af45ff1be)

```
$ pushd <directory path>
$ popd
$ dirs

•Linux keeps a stack of directories
```
```
Example:
$ pushd /home/tom is equivalent to :
$ cd /home/tom + push the directory “/home/tom” to the stack
$ popd is equivalent to :
Get the top path from the stack + cd <the selected path>
$ dirs is equivalent to :
List the contents of the directory stack
```

![image54](https://github.com/user-attachments/assets/2a07004b-985b-48c6-9ac1-bb7c346fed0d)

![image55](https://github.com/user-attachments/assets/5a8206e8-8803-4270-8dbe-099ab4f8fc82)

![image56](https://github.com/user-attachments/assets/462cbcd8-c045-49ad-ad97-dcc942abce2f)

![image57](https://github.com/user-attachments/assets/998dbe0a-7a4f-4b31-8854-2c5074f2afd5)

## Simple Commands and Utilities

![image58](https://github.com/user-attachments/assets/2c2cd366-c85a-4140-9312-995086f4a464)

```
$ echo <text string to display>
$ echo $<variable Name>
```

```
$cat <file or files to display>
```

```
$ date (Show current date and time)
```

**This command is very useful when we want to put time- stamps or create directories or files with the time-stamp in the name**

```
You can adjust your date format
$ date +%D
04/30/14
$ date +%F
2014-04-30
$ date +%j
120 (day of the year 001..366)
$ date +%Y
2014
$ date +%m/%d/%Y
04/30/2014
$ date +%m-%d-%Y
04-30-2014
```

```
$ cal (Show the Calendar for the current month)
$ ncal
$ cal 2011 (shows the calendar for the year 2011)
```

**bc Command**

•The bc tool provides a basic math calculator

•It has capabilities from basic math, to assigning variables, to dealing with arrays

•This tool can be very useful to run mathematical formulas on the command line

•Will be even more useful when we build bash scripts

```
$ hostname
$ sudo hostname <new hostname>
```

```
$ uname (Print multiple types of information about the system)
```

```
$ uptime (print the system uptime and load)
```

**reboot Command**

•This command allows the user (must be root) to reboot the system

```
$ reboot (Reboot the system)
```

## Composite Commands

We can build Composite Commands through the following:

•Sequential Commands

•Conditional Commands

•Command Loops

•Input/Output Redirection

•Pipes

•Command Argument Expansion

•Command Argument Quoting


**I/O Streams**

![image59](https://github.com/user-attachments/assets/1622716e-d440-46f5-8424-880730ef991d)

**Command Model**

![image60](https://github.com/user-attachments/assets/570e90dd-4223-40dd-be62-689d5d5719f8)

**Sequential Commands**

We can have multiple commands in the same line as follows

```
$ <first Command> ; <second Command> ; <third Command>
$ echo "One" ; sleep 10; echo "Two"
```

Using sequential commands is useful when the first command takes long time to execute and we don’t want to wait until it is complete

`$ make ; sudo make install`

Note:

The Sequential Commands just run after each other, they have independent Input & Output

**Conditional Commands**

ORing (“||”)

Second command will only execute if the First Returns Failure

`$ cat <filename> || echo “File Not Found”`

Used for Error Handling

ANDing (“&&”)

Second command will only execute if the First Returns Successfully

`$ mkdir dir1 && cd dir1`

Continue as long as you are successful

**Command Loops**

We can build a loop when we want the command to execute multiple times (maybe on different files or so)

Example:
```
$ for file in *.txt
> do
> mv -v $file $file.old
> done
```

Loops are normally used in scripts, but sometimes it is useful to use on the command line


## INPUT/OUTPUT REDIRECTION

* Redirect Output to File
* Redirect Error to File
* Redirect both Output and Error to Files
* Redirect both Output and Error to same File
* Redirect Input from File

**Standard Output Redirection**

```
$ <Command> > file (Redirect Output to file; Overwrite)
$ <Command> >> file (Redirect Output to file; Append)
```

```
$ echo “Hello world” (output goes to screen)
$ echo “Hello world” > greeting.txt (output goes to the file, overwrite)
$ ls -al /usr/bin >> file-listing.txt (output goes to the file, append)
$ cat file1 file2 > combined-file.txt
```

Note:

1.Error Messages Still go to the screen

2.“>“stands for (and can be replaced by) “1>“ which means Redirect Output Stream

**Standard Error Redirection**

```
$ <Command> 2> file (Redirect Error to file; Overwrite)
$ <Command> 2>> file (Redirect Error to file; Append)
$ make (Both Output and Error messages go to screen)
$ make 2> log (Output goes to screen; Error messages go to file, Overwrite)
$ make 2>> log (Output goes to screen; Error messages go to file; Append)
```

**Both Output & Error Redirection**

•Output and Error go to Different Files,

```
$ <command> >file1 2>file2 (output to file1, error to file2)
$ <command> >>file1 2>>file2 (output to file1, error to file2)
```
•Both Output and Error go to the same file,

```
$ <command> >file 2>&1 (both to file)
$ <command> >>file 2>>&1 (both to file)
```

•Short version of the same command

```
$ <command> &>file (both to file)
$ <command> &>>file (both to file)

```

**Standard Input Redirection**

`$ command < file (input to the command is read from the file)`

Examples:

```
$ wc -l < log-file.log
$ sort < log-file > sorted-log-file
$ mail ceo@company.com < resume
$ spell < report.txt > error.log
```

**Common Devices for Redirection**

1.`/dev/stdout` : Standard output device

2.`/dev/stderr`: Standard error device

3.`/dev/stdin`: Standard input device

4.`/dev/null` : This device is useful for being a data sink. This is useful when we want to discard the command `output` (such as compiler long output)

5.`/dev/zero` This device is useful as an` input` device to generate and infinite stream of zeros

6.`/dev/random` This device is useful as an `input` device to generate random bytes. It may block

7.`/dev/urandom` This device is useful as an `input` device to generate quasi-random bytes. It is non blocking

8.`/dev/full` This device is used as an `output` device to simulate a full file. It is used for testing purposes

## USING PIPES

![image61](https://github.com/user-attachments/assets/2fbb2ddf-120e-4c1e-9655-1f280c05f403)

**What is a Pipe ?**

•A Pipe is a mechanism in Linux Kernel that is used to enable one process to send information to the other process

•This is called IPC (Inter Process Communication)

•A Pipe is a unidirectional mechanism, so if you need data to flow in both directions, you will need two pipes (One for each direction)

•Pipes in Linux are a method for Communication between different processes (Inter-Process Communication)

•On the Command line Interface, we can run two commands and connect them with a pipe, so output of one command feeds in the input of another one

•Note that every command runs in a sub-shell of the shell issuing it (child shell)

```
$ <command1 > | <command2> | <command3>
•Examples:
$ cat log-file.log | grep “Error”
$ man gzip | grep -i “compress”
$ cat log-file-1.log log-file-2.log | grep -i “error”
$ cat name-list.txt | sort
$ cat * | grep -i “error” | grep -v “severe” | sort > file.log
$ cat resume | mail bill-gates@microsoft.com
```

## tee Command

![image62](https://github.com/user-attachments/assets/d5e71b1b-93ef-4f5c-b194-b9443bf535e1)


`<Command > | tee <list of Sinks>`

The tee command sends the output to a set of files as well as the standard stdout (default is screen)

•Examples:

```
$ make |tee make.out.txt (output to the screen and the file)
$make |tee -a make.out.txt (same, but uses append mode)
$ date | tee file1 file2 file3 file4 (date is sent to the 4 files & screen)
$ make |tee make.out.txt >> file2 (output goes to make/out.txt and appends file2)
$ make | tee make.out | grep “error”
```

## Commands Arguments Expansion

**Parameter Expansion ( $ and ${ } )**

The Parameter Expansion is used to evaluate shell or environment variables

Examples:

```
$ echo $PATH
$ echo ${PATH}
$ MY_NAME=TOM
$ echo “My Name Is $MY_NAME”
```

**Arithmetic Expansion ( $(( )) )**

The Arithmetic Expansion is used to put arithmetic expressions to be evaluated

Examples:

```
$ echo $((5 + 6)) --> 11
$ echo $(( ((5**2)) * 3)) --> 75
$ echo $((5 % 2)) --> 1
$echo $((5/2)) --> 2
```

**Brace Expansion ( { } )**

The Brace Expansion results in a set of values as described inside the braces

Examples:

```
$ echo abc-{A,B,C}def --> abc-Adef abc-Bdef abc-Cdef
$ echo a{A{1,2} , B{3,4} }b --> aA1b aA2b aB3b aB4b
```

Similarly, you can use the expansions

```
{1..5}
{A..Z}
{Z..A}
```







































