
## Learning About the Shell

**What is the “Shell”**

•The Shell is a user space program that accepts text input

•It performs parsing and some expansion of the input

•It uses the `readline library` for text parsing

•It is accessed through a terminal or terminal emulator program

•It then passes control to appropriate functionality (within the shell or outside it)

• "a shell manages the interaction between the system and its users"

•A shell will come with some builtin functionality, other functionality will be provided by separate binaries

![image85](https://github.com/user-attachments/assets/b1f94a02-ca33-4aa2-8f20-005ea6e9092b)

## Types of Shells

•Supported shells will be listed in the file `/etc/shells`

•Default shell for the user will be stated in `/etc/passwd`

•To switch to a different shell, call its binary, for example if you are running with a different shell and want to use bash, `$ bash`

Then you can exit to the original shell by, `$ exit`

•To know what shell you are using, `$ echo $SHELL`

## Commands Categories

Commands can be one of the following

1.Built-in command within the shell program (such as ‘cd’)

2.A binary or executable in the system, that is called by the shell program. This binary should be in the PATH to be accessible (they normally reside in `/usr/bin`)

**type Command**

$ type <Command> 

This identifies the category of the <command>

•Examples:

```
$ type cd
cd is a shell builtin
```

```
$ type rm
rm is /bin/rm
```
```
$ type ls
ls is aliased to `ls --color=auto`
```

**Builtin Commands**

•Those are functionality implemented inside the shell binary

•No separate binary for it

•Very limited set, and for very basic commands only

•Examples,

$ cd

$ pwd

•Since they don’t have a separate binary, you can not do

$ cd --help

Instead you can use the shell built in command

`$ help cd`

## Aliases

•Aliases are an abbreviation of another command (with options/arguments)

•To make an alias command

`$ alias newCommand=‘long command’ (Make sure no spaces)`

Example:

`$ alias ll=‘ls -al’`

```
•To remove an alias command
$ unalias <alias command>
```

Example:

$ unalias ll

•To list all of aliases

$ alias

•If the new command is a used command, it will still work (the new command will override the old one)

`$ alias ls= ‘ls --color=auto’`

•Make sure you don’t do this by mistake, check the existence of a command with the alias name before you do the aliasing

`$ type <alias candidate>`

It should tell you it is not found

## Command History

•When you enter a command, Linux stores it in a history file ~/.bash-history

•To browse through command history

`$ history`

•Now you can do the following,

```
$ !! (to enter the last command)
$ ! <n> (to enter the command # n in the histroy
$ ! abc (to enter the last command starting with ‘abc’)
$ ^abc ^def (enter the last command but replace ‘abc’ with ‘def’)
$ command2 !* (run command2 with all arguments from the last command)
$ command2 !$ (run command2 with only last argument from the last command)
$ command2 !^ (run command2 with only the first argument from the last command)
```

**script Command**

$ script <file>

To write commands and their output to a file
```
$ script file
$ script -a file (append the existing file)
$ script -t file (put time stamp in front of each command)
$ script -f file (flush after each command)
```

## Shell Types

•Shells belong to two categories

    •Login shell
    
       •Shells that require login before starting
       
•Non-Login shell

     •Those shells don’t require a login
     
     •They are children of login shells
     
•To exit a shell,

•For Login shell  ` $ logout`
   
•For non-login Shells
`
   $ exit`


## Shell Startup --Login Shells

When the Login Shell starts up, it goes through these steps to set the proper environment

•System Wide Configurations

•It reads `/etc/profile` for global configurations (for all users)
    
•User Specific Configurations

•Then it reads one of the following for user specific extensions/overrides (if it finds one of the files starting from the first, it will read it and skip the rest)
    
 ``` 
   ~/.bash-profile
       
   ~/.bash-login
       
   ~/.profile
```
       
•Note that those files normally call` ~/.bashrc` internally



## Shell Startup – Non-Login Shells

Non-Login Shells build their environment as follows,

•First, they inherit the environment from their parent Login Shells

•On top of that, it reads the following configuration files,

•For Global settings they read the files:
```
/etc/.bashrc
/etc/bash.bashrc
```

•For user specific settings, they read,

`~/.bashrc`

## Updating ~/.bashrc

•Each user can put his own settings in ~/.bashrc such as,

•Set environment Variables

•Set Command Aliases

•Define Shell Functions

•The new settings in ` ~/.bashrc` will not take effect in the current shell, since it is only read at shell startup

```
•Solution,

•Start a new shell

•Manually Force a ~/.bashrc read
```

## Running the ~/.bashrc Script (source Command)

•Normally, scripts are run by calling them from the prompt
`$ <script name>`

•We can not just call the script in `~/.bashrc` like normal script … WHY??

•When a script is run, it runs in a child shell

•When the script completes, the child shell closes, and control gets back to the original shell

•This means, anything that was set in the script will apply to the child shell, and when it is closed, these settings will be lost

•We need a new way to force the script to run in the current shell, and not in a child shell, so settings will apply to the current shell
```
$ source .bashrc
$ . .bashrc
```

## Protecting from File Over-Write (Setting noclobber)

•Clobbering a file means over-writing a file (normally in an unintentional way) This happens very often through output redirection

`$ echo “Good Morning” > file.txt`

•To avoid that we adjust the noclobber settings in` ~/.bashrc`

•Example:
```
$ set -o noclobber (this will protect files from being over-written)
$ set +o noclobber (this will remove the protection)
```

•Note

•If files are protected from over-writing, you can still force an over-write

$ echo “Good Morning” >| file.txt


## What are Environment Variables ??

•Environment Variables are variables that store information about the system

•They can be used to store data, set configuration options and customize the shell environment under Linux

•Can be divided into,

•System Environment Variables

      •Standard Names
      
      •Used by the Shell
      
      •Normally they are All Caps
      
      •More can be added by the users for their usage

      
•Local Variables

     •User selected names
     
     •Local to a shell (not passed to children shells or programs)
     
     •Convention is to avoid all caps to differentiate them

**•Examples of use of Environment Variables (not a full list) :**

•Configure look and feel of shell such as colors and bash prompt

•Time zone, host name,…

•Search path for executables, or any types of files

•Default values for some system configurations

•Some configuration options for specific programs

•Always keep in mind that Linux **does not** maintain or store a global set of environment variable for the system

•Each running program (process) will have its own environment settings

•This means different processes may have different environment settings

•The environment settings for each running process in the system can be listed by viewing the file ` /proc/<pid>/environ`

•Where pid is the Process ID 

•Keep in mind that the shell is a process, and hence it has its own environment settings as well

## So How does Processes receive their Environment Settings ??

**By inheritance**

•Each process will have a parent process that started it

•The child process inherits the **environment settings**of its parent process

•Keep in mind that each program (process) that is started inside the shell, is a child of that shell, hence processes started from the shell, inherit the shell environment settings

•Also keep in mind that, a non-login shell is a child of a login shell, hence it inherits its environment settings at startup

•Note that local variables are not inherited to child shells or processes

**By Startup Scripts**

•Some programs source some scripts at startup

•These scripts may include some environment settings that is added to the process settings inherited from its parent We have already discussed this for login/non-login shell startup

•Login Shells

```
/etc/profile
~/.bash-profile or ~/.bash-login or ~/.profile
```

•Non-Login Shells

```
/etc/.bashrc or /etc/bash.bashrc
~/.bashrc
```

**/etc/profile**

•To add settings that will apply to all shells, and all users… we need to put it in `/etc/profile`

•In most distributions, it is preferred not to edit `/etc/profile` directly

•To enable that, `/etc/profile` has a loop that sources all scripts with extentions *.sh in the folder `/etc/profile.d`

•Accordingly, all we need to do is to put our settings in a new script file inside this folder and call it `something.sh`then make it executable

•Our script will be called from `/etc/profile` and hence our settings will be read by login shells, and inherited by non-login shells


**By Passing them as Arguments at start**

•If you want to run a program with some environment variables settings

```
$ env VAR=VALUE Command
OR
$ VAR=VALUE Command
```

•Examples:

```
$ env EDITOR=vim xterm
$ EDITOR=vim PATH=$PATH:~/projects myScript.sh
```

**By Adding them Manually**

•If you want to add a local variable in the shell

`$ VARIABLE=VALUE`

•If you want to add an Environment variable in the shell

`$ export VARIABLE=VALUE`

•Note that the value can be surrounded by quotes

•Optional in general

•Mandatory if it contain spaces

•Examples:

```
$ Source_Dir=“/usr/share”
$ export EDITOR=vim
$ export Project_Dir=“~/my project/docs”
```

**More About “export”**

•To Set a local variable in the shell

`$ My_Var=5`

This way My_Var will not be inherited to any child or process of the current shell

•To Convert it into an Environment Variable

`$ export My_Var`

This way My_Var will be inherited to any child shell or process of current shell

•To bring it back to be just a local variable

`$ export -n My_Var`

•To reset an Environment variable

`$ export My_Var=`

•To Completely remove the variable

`$ unset My_Var`


•Now to access the value of a variable,

```
$ echo $VAR_NAME
$ echo ${VAR_NAME}
```

•Note that we can do the following,

```
$ PATH=$PATH:$HOME/projects
$ PATH=${PATH}:${HOME}/projects
```

•Sometimes the {} is optional, and sometimes it is mandatory

```
$ echo $HOME_and_$USER (Wrong)
$ echo ${HOME}_and_${USER}
```

**the set Command**

`$ set` The set command lists all variables (both local and environment vars) seen by the shell


**the printenv Command**

```
$ printenv
$ env
```
•Print a list of all Environment Variables (not including Local Vars)

`$ printenv <variable>`

•Note that we put the variable without the dollar sign

•Examples:

```
$ printenv PATH
$ printenv
```









     
     







