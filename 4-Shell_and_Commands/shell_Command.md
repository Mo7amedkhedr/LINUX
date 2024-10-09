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






