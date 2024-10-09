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






