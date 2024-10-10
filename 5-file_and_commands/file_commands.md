## File Viewing and Editing

**Write(Editors)**

* Vi/ vim
* nano
* cat ---> (Ctrl+d)
* gedit
* Code/notepad


## vim

Vim is an advanced and highly configurable text editor built to enable efficient text editing. It supports most file types and vim editor is also known as a programmer’s editor. We can use its plugin based on our
needs. 

**In Vim, you can make the help documentation take up the entire screen by using the :help command with the :only command**

**modes**

1. Command Mode(Normal Mode)

2. Command-Line Mode
 
3. Insert Mode
  
4. Visual Mode


**Exit from terminal**

```
:q    quit
:wq   write and quit
:!q   quit without saving
:x like :wq
:exit
```

## Moving Around in Vim

![image38](https://github.com/user-attachments/assets/52e5c480-71bc-4b93-a94f-0d1884b05682)

```
● w, b,e for word navigation
● gg, G for moving to the beginning and end of a file
● { } for paragraph
● 0 -> first line
● $-> end of line
● % -> () {}
● Number G / number gg-> goto line
● 2w -> moves two words
● 10$ move 10 lines
● H - move to top of screen
● M - move to middle of screen
● L - move to bottom of screen
```
**if you need any help you will find it in Vim cheat sheet**

## Inserting Mode

```
● i - insert before the cursor
● I - insert at the beginning of the line
● a - insert (append) after the cursor
● A - insert (append) at the end of the line
● o - append (open) a new line below the current line
● O - append (open) a new line above the current line
● Ctrl + t - indent (move right) line one shiftwidth during insert mode
● Ctrl + d - de-indent (move left) line one shiftwidth during insert mode
● Esc or Ctrl + c - exit insert mode
```

## Editing Text

```
● r – replace a single character (and return to command mode)
● R - replace more than one character, until ESC is pressed.
● ciw - change (replace) entire word
● cc – replace an entire line (deletes the line and moves into insert mode)
● C / c$ – replace from the cursor to the end of a line
● cw – replace from the cursor to the end of a word
● u – undo
● Ctrl + r – redo
● . – repeat last command
● p - put (paste) the clipboard after cursor
● P - put (paste) before cursor
● yy - yank (copy) a line
```

## Marking text (visual mode)

```
● v - start visual mode, mark lines, then do a command (like
y-yank)
● V - start linewise visual mode
● Ctrl + v - start visual block mode
● aw - mark a word
● ab - a block with ()
● aB - a block with {}
● at - a block with <> tags
● ib - inner block with ()
● iB - inner block with {}
● it - inner block with <> tags

```

## commands

```
● :3,5d - delete lines starting from 3 to 5
● :g/{pattern}/d - delete all lines containing pattern
● :g!/{pattern}/d - delete all lines not containing pattern
● :%s/searchword/replaceword/g
● :%s/searchword/replaceword/gc
● set number ,set relativenumber
● Set mouse=a
● /pattern – search forward for the specified pattern
```

## Controls

```
Redirection > 2> <
Piping |
Wild card *,? ,()
```

![image39](https://github.com/user-attachments/assets/27827486-668a-46e7-bda2-e3ea14db0b26)

## Piping

![image40](https://github.com/user-attachments/assets/1ece20e1-0b67-4f1d-81de-40f634b285bc)


## Wild Card

In Linux, a wildcard is a character or a sequence of characters used to represent one or more other characters. Wildcards are mainly used with commands like ls, cp, mv, and find to perform operations on multiple files or directories that match a certain pattern.

**Example**

```
Asterisk(*) : The asterisk (*) represents zero or more characters. For example:
   *.txt matches all files ending with ".txt".
   file* matches all files starting with "file".
   *pattern* matches all files or directories containing "pattern" anywhere in their names.
```

```   
 Question Mark (?): The question mark (?) represents a single character. For example:
 file?.txt matches "file1.txt", "fileA.txt", but not "file10.txt".
```

```
Square Brackets[] and,ranges:Square brackets allow you to specify a range or a set of characters for asingle position in the pattern
For example:
 [0-9]* matches all files or directories starting with a digit.
 [aeiou] matches any single vowel
```

```
 Brace Expansion {} or : Brace expansion allows you to generate multiple strings by specifying a comma-separated list inside curly
 braces. For example:
 file{1,2,3}.txt expands to "file1.txt", "file2.txt", "file3.txt".
 {apple,banana,orange} expands to "apple", "banana", "orange".
```

```
 Exclamation Mark (!) not: The exclamation mark (!) can be used to negate a pattern. For example:
 ls !(*.txt) lists all files and directories that do not end with ".txt".
```

## Regex

**Literal && Meta-Characters**

**Literal**

are those characters that represent themselves in the search pattern .

**Meta-Characters**

are those characters that have special meaning(^ $ . [ ] { } - ? * + ( ) | \ )

Meta characters can be treated as literals if they are escaped, i.e. preceded by a back slash Examples, ^ { $ \ ==>The back slash can also convert some of the literal characters into a meta-characters 
examples : \d \w


**Types of Regular Expressions**

* Basic Regular Expressions ==> . ^ $ [ ] *
* Extended Regular Expressions ==> ( ) { } ? + | The tool ‘grep’ uses BRE To access ERE, use ‘egrep’ or ‘grep –E ‘

**Basic Regular Expressions**

```
 Any Character (.)
At the beginning (^)
At the end ($)
Any value from group [ ]
Any value not from group [^ ]
range [ - ]
```

**Extended Regular Expressions**

```
Alternation (|)
Quantifier ‘?’ ==> zero or one time
Quantifier '*' ==> zero or More times
Quantifier ‘+’ ==> One or More times
```

## File Permissions (chmod, chown)

chmod allows you to set Read, Write, Execute Permissions, chown enables you to change who the owner of the file is

![image41](https://github.com/user-attachments/assets/02f13d55-f55c-4cd4-868b-fca06020557a)


![image42](https://github.com/user-attachments/assets/d9e7e639-8d43-4e17-aad4-dbab367dbdbf)


![image43](https://github.com/user-attachments/assets/acfc3295-3a5d-420a-b9e8-4475f192dafd)


## File Compression and Archiving

* Tar
* Bz2
* 7z
* Gz


**Tar**

The Tar command, short for Tape Archive, is a powerful tool that allows users to create compressed and archived files

```tar [options] [archive-file] [file or directory to be archived]```

Here ,
tar: The command itself.

[options]: Optional flags or settings that modify the behavior of the tar command.

[archive-file]: The name of the archive file you are creating or working with.

[file or directory to be archived]: The file or directory you want to include in the archive.


|    Options    | Description   |
| ------------- | ------------- |
| -c  | Creates an archive by bundling files and directories together.  |
| -x  | Extracts files and directories from an existing archive.  |
| -f  | Specifies the filename of the archive to be created or extracted.  |
| -t  |Displays or lists the files and directories contained within an archive.  |
| -u  | Archives and adds new files or directories to an existing archive.  |
| -v  |Displays verbose information, providing detailed output during the archiving or extraction process.  |
| -A  | Concatenates multiple archive files into a single archive. |
| -z  | Uses gzip compression when creating a tar file, resulting in a compressed archive with the ‘.tar.gz’ extension.  |
| -j  | Uses bzip2 compression when creating a tar file, resulting in a compressed archive with the ‘.tar.bz2’ extension. |
| -W  |Verifies the integrity of an archive file, ensuring its contents are not corrupted. |
|-r | Updates or adds files or directories to an already existing archive without recreating the entire archive.  |

**Examples**

1. Creating an uncompressed tar Archive using option -cvf

```
tar cvf file.tar *.c

‘-c’: Creates a new archive.
‘-v’: Displays verbose output, showing the progress of the archiving process.
‘-f’: Specifies the filename of the archive

OUTPUT:
os2.c
os3.c
os4.c
```

2. Extracting files from Archive using option -xvf

```
tar xvf file.tar

‘-x’: Extracts files from an archive.
‘-v’: Displays verbose output during the extraction process.
‘-f’: Specifies the filename of the archive.

Output :  

os2.c
os3.c
os4.c
```

3. gzip compression on the tar Archive, using option -z

```

tar cvzf file.tar.gz *.c

‘-z’: Uses gzip compression.
‘-j’: Uses bzip2 compression.
‘-J’: Uses xz compression.

```

4. Extracting a gzip tar Archive *.tar.gz using option -xvzf :

This command extracts files from tar archived file.tar.gz files.  

```tar xvzf file.tar.gz```

5. Creating compressed tar archive file in Linux using option -j

This command compresses and creates archive files less than the size of the gzip. Both compress and decompress take more time than gzip.  

```
tar cvfj file.tar.tbz example.cpp
Output:  

tar cvfj file.tar.tbz example.cpp
example.cpp

tar tvf file.tar.tbz
-rwxrwxrwx root/root        94 2017-09-17 02:47 example.cpp
```

6. Untar single tar file or specified directory in Linux:

This command will Untar a file in current directory or in a specified directory using -C option.  

```
tar xvfj file.tar 
or 
tar xvfj file.tar -C path of file in directory
```


## Text Processing

**grep**

Grep, short for “global regular expression print”, is a command used for searching and matching text patterns in files contained in the regular expressions.

![image44](https://github.com/user-attachments/assets/667c8180-5570-4d92-ac1e-d6f3d381dfd8)


**sed**

* SED is a powerful text stream editor. Can do insertion, deletion, search, and replace(substitution).
* SED command in UNIX supports regular expression which allows it to perform complex pattern matching.

`$sed 's/unix/linux/' file.txt`

Here the “s” specifies the substitution operation. The “/” are delimiters. The “unix” is the search pattern and the “linux” is the replacement string. By default, the sed command replaces the first occurrence of the pattern in each line and it won’t replace the second, third…occurrence in the line.


`$sed 's/unix/linux/2' file.txt`

Use the ‘/1’, ‘/2’ etc. flags to replace the first, second occurrence of a pattern in a line


`$sed 's/unix/linux/g' file.txt`

The substitute flag /g (global replacement) specifies the sed command to replace all the occurrences of the string in the line.


`$sed 's/unix/linux/3g' file.txt`

Use the combination of /1, /2 etc and /g to replace all the patterns from the nth occurrence of a pattern in a line. The following sed command replaces the third, fourth, fifth… “unix” word with “linux” word in a line


`$sed '3 s/unix/linux/' file.txt`

The above sed command replaces the string only on the third line.


`$sed 's/unix/linux/p' file.txt`

The /p print flag prints the replaced line twice on the terminal. If a line does not have the search pattern and is not replaced, then the /p prints that line only once

`$sed '1,3 s/unix/linux/' file.txt`

Here the sed command replaces the lines with range from 1 to 3

**To Delete a particular line say n in this example**

```
Syntax:
$ sed 'nd' filename.txt
Example:
$ sed '5d' filename.txt
```

**To Delete a last line**

```$ sed '$d' filename.txt```




## File Handling Internals

![image45](https://github.com/user-attachments/assets/1a1a30d3-9d7c-445b-8fa0-d885345eb6ac)

![image46](https://github.com/user-attachments/assets/08ef5773-1e7d-4582-8ed5-38886270cf3d)

![image47](https://github.com/user-attachments/assets/b2c88763-3118-407b-9622-cf58d549d9e6)

**What is a File ??**

•A file is a set of bytes that represent some content (pdf document, excel sheet, binary executable, … )

•The file is stored in a (partition in a) storage device as a single data block or fragmented into a group of data blocks (within the same partition)

•The fileSystem is responsible for managing the data block(s), and their representation to the user

•For this management, the fileSystem needs to maintain some extra info about the file which is called file Meta-data

   •File Size
   
   •File Owner (user & group)
   
   •File Permissions
   
   •Data of creation/last modification
   
   •Pointers to the file content data blocks
   
    •etc …
    
•These meta-data are stored in an “inode” structure

•Note: the inode does not contain the file name or its location

•This means that the filesystem maintains a table of inode structures (one structure per file)

•The The “inode” structure will contain all file meta-data (except its filename)

•The “inode” structure will also point to the data blocks of the file

•Each data node has a unique number across the filesystem (the inode number)

•Inode numbers are unique per filesystem (and not across the system)

•Directories are a special type of files, accordingly, they are treated the same way

•The inode structure does not have knowledge about the filename or its location

•Instead, each file or directory has another structure named “dentry”, this structure maps a file/directory to its “inode#”

•The “dentry” structure forms the directory tree


![image48](https://github.com/user-attachments/assets/bf75bdbb-fbeb-4250-a536-19aebf315f25)

## Listing Files/Directories (ls Command, stat Command, df Comand )

```
$ ls -i (List with showing the inode#)
$ ls -il (List with showing the inode# with long format)
$ stat (Show File Status info)
$ df (Show FileSystem Disk Space Usage)
$ df -i (Show FileSystem inode Usage)
```

## FILE OPERATIONS

**Hard Links**

•The decision of not including the filename and path in the “inode” structure was to enable the use of hard links

•Hard links were introduced from the early days of Unix

•A hard link

•Not a new file

•Same file content

•Same inode

•Just an additional “dentry” with a different filename/path, but with the same inode#

•This is useful if we need to have the same file with two names, or in two locations

•Hard links are not very common these days, they have some limitations,

•Only applicable for files, not used for directories After implementing it for directories, a security hole was found Can cause loops of links which result in system faults So it was disabled in latest releases

•Does not work across filesystems

We link using the inode# But inode# is only unique within the same filesystemHence, we can not link to a file in a different filesystem This is very limiting, specially Linux merges all the FS in a unified tree

![image49](https://github.com/user-attachments/assets/7f03b679-0afe-45ad-8cce-4c1cf881185f)


**Symbolic Links**

•A symbolic link is introduced to fix the problems of Hard Links

•A symbolic Link is not just a dentry structure; it is a file with an inode structre

•The inode structure The type is set to ‘l’ for a symbolic link

•Two types of Implementation:

•Slow Symbolic Links:

       •The data block of the new file include the path of the file it is linking to
       
•Fast Symbolic Links:

•A field in the inode points to the path and name of the file/directory it is pointing to

•Faster, no need to read the data block

•Not possible if the path is too long to fit in the inode structure

•Since a symbolic link it has its own inode, with an obvious indication that it is a link,

•Some commands is able to treat it differently

•Avoid the security hole in hard links with linking directories

•We can link to a file/directory in a different file system

•Symbolic links are like shortcuts in windows

•You can have a symbolic link to a file or a folder


![image50](https://github.com/user-attachments/assets/c4db1e92-eb1a-409c-bd9a-a7df6a226da6)




## Hard Link Vs Symbolic Link Abstracted View


![image51](https://github.com/user-attachments/assets/93df247d-c233-4a2f-86f8-ec3bf02d597f)


## Creating File Links (ln Command)

•To create a Hard Link

```
$ ln <File to link to> <link name & location>
$ ln file.log ~/log-files/a.log
```
•To create a Symbolic Link

```
$ ln –s <File to link to> <link name & location>
$ ln -s ~/file.log ~/log-files/a.log
```

**Important Note: Always use absolute paths for the file to link to when creating symbolic links …. Never use relative path format**


## Help Commands

![image52](https://github.com/user-attachments/assets/6a248203-e55c-4460-90dd-f74e96283f0a)

**man Command**

`$ man <command> (Read the man page for a Command)`

•The`man` command reads from the manual pages stored in your distribution

•The location of these pages may differ slightly based on the distribution

•Use the command `manpath` to know the location of the man pages on your machine

$ manpath

•This command identify the location of the man pages based on the configuration file `/etc/manpath.cfg`

•Sometimes we will have an Environment variable MANPATH for that purpose too

$ echo $MANPATH

•Typically they are located in /usr/share/man/

**The “whatis” Database**

The `whatis` database is a database containing a selected parts of the man pages

•Title

•Section Number

•Name field

•This database is used with the commands,

$ whatis

$ apropos

$ whatis <keyword> (find the man pages which has keyword in title)

**apropos Command**

•The `man` command assumes that you know the command name

•What if you don’t know the command name and just have a keyword ??

•The solution is to use `apropos` command

•`apropos` command receives a keyword, and searches both the ‘title’ and the ‘Name’ field in the whatis database for this keyword

•It then prints a single line (the Name field) for each command matching the keyword

$ apropos <keyword>

•Examples:

$ apropos process (Searches for all commands dealing with process)

$ apropos proce (even a part of a word can be used)

•Note, the same output can be achieved via,

$ man -k <keyword>

**info Command**

$ info <Command> (Display the Info pages on the command)

•Info pages are similar to man pages but created by the GNU project for the GNU applications

$ info gzip

$ info emacs

•To know more about this command

$ info info

•The GNU commands will have both man pages and info pages

•The info pages are usually more recent and are somewhat easier to use

•Sometimes, the man pages refer to the Info pages








