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



