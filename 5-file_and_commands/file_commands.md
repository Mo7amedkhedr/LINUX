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



