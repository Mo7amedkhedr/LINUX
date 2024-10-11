
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


