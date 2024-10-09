## What is the main purpose of shell ?

A shell provides a command-line interface, allowing users to interact with the operating system and execute commands
The shell serves as an interpreter for running programs and scripts. It can execute both system-level commands and user-created scripts

![image19](https://github.com/user-attachments/assets/3580460c-e022-4b79-86d4-b2f9df4615b3)

## ELF file 

the executable file may be .elf , .exe , .out ,.....

![image20](https://github.com/user-attachments/assets/4a3c27ec-f3ef-4c4d-a7cc-455ebb361baf)

![image21](https://github.com/user-attachments/assets/ffd50252-e68a-4177-ba65-80b78770b440)

**when the process run the first system-call run is execve**

![image22](https://github.com/user-attachments/assets/87401b2e-8fc6-418d-af5d-0a699ac88616)

**by using the loader or interpreter (/lib64/ld-linux-x86-64.so.2), it load the shared libraries**

![image23](https://github.com/user-attachments/assets/7b103af3-79fd-43a1-be29-19017cfed719)

**Headers**

![image24](https://github.com/user-attachments/assets/715459fe-3b1a-4b74-9049-79e34d595ba9)

**Elf may be dynamic or static**

**if it dynamic**

* mean more system calls
* less size
* there is loading to the shared libraries (dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2)

![image25](https://github.com/user-attachments/assets/94fd6cf8-40e5-4ddc-9e92-a104d796a27e)


**if it static**

* less system calls
*  more size
*  there is no loading to the shared libraries (statically linked)

![image26](https://github.com/user-attachments/assets/02ffe29d-06ce-4df5-9027-aa7aed9379f6)

##  dynamic loader

**Elf needs ld-linux as dynamic Linker to load libraries**

![image27](https://github.com/user-attachments/assets/646d3aa8-be8d-4482-be69-c64ae9f4b388)

![image28](https://github.com/user-attachments/assets/5bc42af1-0a06-4caf-a65b-421ed0d14cd2)

**Elf file has info about what is the shared is needed**

![image29](https://github.com/user-attachments/assets/1c37a146-5392-461d-b4f2-589e7d2f7013)

![image30](https://github.com/user-attachments/assets/f9b27d2a-7499-45c7-8e92-338e544b9e98)

## create Bash

**Fork system call**

fork() creates a new process by duplicating the calling process. The new process is referred to as the child process. The calling process is referred to as the parent process.

![image31](https://github.com/user-attachments/assets/21630ede-d5e2-44ab-9b8c-a04eadcae26f)

```
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <time.h>
#include<unistd.h>
#include <sys/wait.h>


int main()
{
    const char *cmd="/usr/bin/sleep";
     char *args[] = {"sleep", "10", NULL};
    char *envp []={NULL};
    pid_t pid;
    pid = fork();

    if (pid < 0) {
        perror("Fork Failed");
        exit(1);
    }
    if (pid == 0) {
        // Child process
        printf("Child Process: My PID is %d, My Parent's PID is %d\n", getpid(), getppid());
        execve(cmd, args, envp);
        perror("execve");
        exit(1);    
        
    } else {
        // Parent process
        printf("Parent Process: My PID is %d, My Child's PID is %d\n", getpid(), pid);
       int status;
       waitpid(pid, &status, 0);
       printf("Child Process  %d terminated with status %d\n",pid, status);
    }
    return 0;
}

```

## execve

int execve(const char *pathname, char *const argv[],char *const envp[]); execve() executes the program referred to by pathname.

* pathname must be either a binary executable,
* argv is an array of pointers to strings passed to the new program as its command-line arguments. By convention, the first of these strings (i.e., argv[0]) should contain the filename associated with the file 
    being executed. The argv array must be terminated by a NULL pointer.(Thus, in the new program, argv[argc] will be NULL.)
* envp is an array of pointers to strings, conventionally of the formkey=value, which are passed as the environment of the new program. The envp array must be terminated by a NULL pointer.

![image32](https://github.com/user-attachments/assets/fe8c4dea-a20c-4490-a170-38df9d5d3658)


## what is meant by file ?

**Inode**

every file and directory has it's own directory entry contain (name , inode[pointer to i node structure]).

if it file the blocks will be a pointer to the data if it directory the blocks will point to the Directory entry to the content of this directory there is direct blocks which point direct to the data and indirect block if the data is very big ,it point to another block and every block has (name , inode) that point to the inode structure. it may be single indirect , double or triple indirect .....

![image33](https://github.com/user-attachments/assets/cb6fcddb-974d-47c2-ad24-6c54b7bbeef0)


## Linux Command

![image34](https://github.com/user-attachments/assets/46be301f-9b15-4e2d-a9ed-37eaa3f34633)

![image35](https://github.com/user-attachments/assets/7c22658f-7bd4-419d-81bb-ccb27f4cf586)

**General form of Commands**

`$ <command> [options] [arguments]`

**Commands can be issued on their own**

$ ls

$ pwd

$ cd

The Options are normally optional (by definition)

The usually start with ‘-’ or ‘--’

‘-’ used with the short name for the option

`$ ls -a`

‘--‘ used with the long name for the option

`$ ls --all`

**If we want to use multiple options Sometimes we join options or keep them separate**

`
$ ls -a -R
$ ls -aR
$ ls --all --recursive
`

## Basic Commands

![image36](https://github.com/user-attachments/assets/8cc1f596-f179-45e8-81c8-f8e63791f717)

```$ ls [options] [<dir or file> ..]```

```
$ ls (list current directory)
$ ls -a (all: show hidden files)
$ ls -l (long: show file details)
$ ls -t (timestamp: sort based on timestamp)
$ ls -S (Size: sort based on file size)
$ ls -r (reverse: make the sort in reverse order)
$ ls -d (directories: Only show directories)
$ ls -R (Recursive: list files inside subdirectories)
$ ls <dir> (List the contents of the mentioned directory)
$ ls <file> (List the mentioned)
$ ls <dir or file> <dir or file> <dir or file> (list selected dirs or files)
```

**Displaying the Directory Tree (tree Command)**

```
$ tree [options] [<dir or file> ..]
$ tree (display the full tree starting from current dir)
$ tree -d (only show directories)
$ tree -a (show all files; including hidden ones)
$ tree <dir> (show the tree starting from a different point)

```

**Print Working Directory**

```$ pwd (Display Current Directory)```


**Moving Around (cd Command)**

$ cd [destination]

```
$ cd /etc/network (absolute path)
$ cd ../project/ (relative path)
$ cd ./project (relative path)
$ cd project (relative path, same as ./project)
$ cd ~ (go to my home directory /home/aelarabawy/)
$ cd ~user_name (go to /home/user_name)
$ cd (same as cd ~)
$ cd .. (go to parent directory)
$ cd - (go to previous directory)
```


**Making New Directories (mkdir Command)**

```$ mkdir <new directory name with path>```

```
mkdir project1 (create a new directory from current location)
$ mkdir project1 project2 (create 2 directories)
$ mkdir /home/khedr/lectures (absolute path)
$ mkdir ../projects/project1 (relative path)
$ mkdir -p ../projects/project1 (create intermediate folders if needed)
```

**Copying Files & Directories (cp Commands)**

```
$ cp <existing file or dir> <new destination>
$ cp file1 file2 (copy file1 to a new file file2 same location)
$ cp file1 ../projects/ (copy file1 to the new location)
$ cp -r folder1 ../projects/ (copy the folder with its contents)
$ cp -r folder1 ../projects/folder2 (copy the folder with new name)
$ cp /etc/passwd . (copy the file …to here )
```

**Moving/Renaming Files & Directories (mv Command)**

```
$ mv <existing file or dir> <new destination>
$ mv file1 file2 (rename file1 to file2)
$ mv file1 ../projects/ (move file1 to the new location)
$ mv -r folder1 ../projects/ (move the folder with its contents)
$ mv -r folder1 ../projects/folder2 (move with new name)
```

**Removing files and Directories (rm Command)**

```
$ rm [options] <file or dir list>
$ rm file1 file2 (remove file1 and file2)
$ rm -r ../projects/folder1 (remove the folder with its content)
$ rm -i file1 file2 (interactive, ask me before you remove)
$ rm -f ../projects/folder1 (force, force remove)
```

> [!NOTE]  
> To remove directories you need always to use ‘-r’


> [!NOTE] 
> You can not remove your current directory (or any of its parents)

## Wild Cards

Sometimes you will need to execute a command on a group of files instead of a single file

**Examples:**

• You want to delete all log files

• You want to list all image files

• You want to copy old files (ending with .old) to a different place The solution for that is to use Wild Cards (also called Globbing)

• Wild cards are patterns that work as placeholders in file names and directory names that are used to apply the command on a group of files/directories that share something in their name

• Remember wild cards are used for file names and directory names ONLY ….. For normal text another patterns are used (Regular Expressions)

**The “*” Wild Card**

The `*` can replace any set of characters (including none) in the file/directory name

**Example**

```
$ rm *.php
$ rm p*
$ rm *.*htm*
$ rm -r *.*
$ rm -r *
```

**The “?” Wild Card**

The “?” wild card stands for any single character

**Example**

```
$ rm 40?.shtml
$ rm ?0?.shtml
```

**[<chars>] and [!<chars>]**

We can have more restriction than the use of “?” by specifying a limited set of options for the character

```
“[ars]” : Stands for a Single character from the list a,r,s
“[!ars]” : Stands for any Single character except for the list a,r,s
“[2-5]”: Stands for a Single character from the range 2 to 5
“[!2-5]”: Stands for any Single character except for the list 2 to 5
“[a-l]” : Stands for a Single character from range of ‘a’ to ‘l’
“[!a-l]”: Stands for any Single character except for the list a to l
“[1-37-9]”: Stands for 1,2,3,7,8,9
“[a-chk]”: Stands for a,b,c,h,k
```

**Examples:**

```
$ rm -r ab[c-fh-j]
removes the files/folders named abc,abd,abe,abf, abh,abi,abj
```

```
$ ls results-[0-9][0-9].log
lists the files named results-00.log to results-99.log
```

**[[:< ClassName >:]]**

 “[[:<classname>:]]” stands for a single character belonging to the specified class

Some of used classes
```
[[:alnum:]] Alpha Numeric characters (a-z, A-Z, 0-9)
[[:alpha:]] Alphabets (a-z, A-Z)
[[:digit:]] Digits (0-9)
[[:lower:]] Lower case character (a-z)
[[:upper:]] Upper case character (A-Z)
```

**Examples:**
$ cp results-[[:digit:]][[:digit:]]-[[:alpha:]].log ~/log



**Use of Curly Brackets “{ }”**

Curly brackets are used to group selections

**Examples,**

```
$ rm {*.log,*.txt}
$ cp {*.pdf,*.doc} ~/documents/
```

**note:**

```
This also works
$ rm *.log *.txt
$ cp *.pdf *.doc ~/documents/
```


**Escape Sequence “\”**

• Some special letters has a meaning (such as space, *, “, ‘, (, …)

• It is not recommended to use these letters in file/directory names But, if we have to then there is a special way of dealing with them,

• If we need to delete a file named “my results.txt”

```
$ rm my results.txt
$ rm my\ results.txt
```

•This is called “Escaping the space letter” which means changing its default meaning from a separator letter into a general letter inside the filename

**Examples of Escape Sequence**

![image37](https://github.com/user-attachments/assets/9f669426-5393-4d5e-a806-7818b8327910)

