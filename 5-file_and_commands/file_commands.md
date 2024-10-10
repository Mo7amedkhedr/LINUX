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













