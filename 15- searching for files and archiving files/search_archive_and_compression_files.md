## Searching for Files


**(The which Command)**

`$ which <binary file>`

•If you are able to run a binary file and want to know where does this binary exist

`$ which shutdown`

•Note that this command searches for the binary using the $PATH environment variable

•This means if the $PATH does not have the folder of the binary, which will not be able to find it

•In other words, if you can not run the command, which will not be able to locate it


**(locate Command)**

```
$ locate <filename>
$ locate <part of the path or filename>
```

•The locate command searches for the required file based on a pre-prepared database of all files in the system along with their full path

•When performing a search using locate command, the database is searched for the passed string

•Hence, You can search based on any string, even if it is only a part of the file path

```
$ locate in/zi
This would result in,
/usr/bin/zip
/usr/bin/zipcloak
/usr/bin/zipsplit
```

**Database for “locate”**

•The database used by the locate command is created by the program `updatedb`

•This program runs in a cron job that periodically (such as once daily) updates the database

•Accordingly the database may have incorrect or incomplete info,

1- Newly created files may not be in the database for sometime

2- recently deleted files may still be in the database

3- Recently moved files, may be in the database using its old location

•This means that these changes will be missed in the search

•If you want to update the index manually,

`$ sudo updatedb`

• The locate command is useful for searching for system files or traditional Linux files but can not be used in a lot of other scenarios


**(find Command)**

•The `find` is a very rich command that can search on files using different search filters, for example,

•Search for a file based on its name

•Search for a file based on its size

•Search for a file based on its last modification date

•Search for a file based on its type (normal file, directory, symbolic link, ….)

•Search for a file based on other criteria

•A combination of all of those search criteria

•Limit the search scope to a certain directory (and its subdirectories)

•Skip Some subdirectories from the search scope

•This command also allows for performing an action on all the files that match the search criteria

•For example:

`$ find ~`  This will list all files in the home directory and its subdirectories

`$ find ~ | wc -l` Count files under my home directory

`$ find /` List all files in the system starting from the root directory. You may need to run this command with sudo to be able to search all files

`$ find /bin /sbin /usr/bin` List all files in those 3 directories (scope can contain multiple directories)

`$ find ~/Documents | grep “.pdf”` Find all pdf files under the Documents folder

`$ find . > file-list.txt` Store a list of files under the current directory in the specified file


**Adding Filters to the Search**

•So far, the find command finds all the files in the specified path, and lists them

•To limit the search to some files, we had to pipe the result to the grep command

•This gives a similar effect to the locate command (except that it is up to date)

•But we need more search options than searching by the filename or the path

•To do that, we need to add Search Filters to the find command

$ find <scope> -type <type> 

To generate a list of directories in the user home directory ` $ find ~ -type d`

•To generate a list of files only in the user home directory  `$ find ~ -type f`

•To generate a list for all symbolic links in the system,   `$ find / -type l`

•For Device files

`$ find / -type c (character devices)`
`$ find / -type b (block device)`

**Searching by File Name**

```
$ find <scope> -name <file name pattern>
$ find <scope> -iname <file name pattern>
```
•To search for a file by its name `$ find ~ -name my-file.txt`


•You can use a pattern for the file name (or even a regular expression)

`$ find ~ -name “*.xml”`

`$ find ~ -name \*\.xml`

•For case insensitive search,

`$ find / -iname “*.html”`

`$ find / -iname \*\.html`


**Find & Perform Action**

•The default action for the find command is to print the list of files matching the search criteria (file name with full path)

•However, you can set another action to apply on those files that meet the search criteria

•Print the names with path (Default action) `$ find ~ -type d -print`

•Delete the files `$ find ~ -name “*.pdf” -delete`

•Perform a detailed list of the files `$ find ~ -size +10M -ls`

•Quit the search on the first match. This can be used if the purpose of the search is jut to find if any file meets this criteria

`$ find ~ -size +100M -quit`


**Skipping Files (The -prune Action)**

•The find command performs its search recursively in all sub-directories

•In case we need to skip some search results, we can use a search filter with the -prune action with the other search filters

•Example:

```
$ find ~ -type l -prune -o -name "*.txt" -print
$ find . -path ./misc -prune -o -name '*.txt' -print
$ find . -type d \( -path dir1 -o -path dir2 -o -path dir3 \) -prune -o -print
```

**User Defined Actions (The -exec Action)**

•So far, we have worked with some defined actions for the find command

•What if we want to do another thing with the outcome with our search?

•We will need to pass the outcome of the search as an argument to our command

•This can be achieved using the `-exec option`

•With this option,

•The find command first gets the list of files that meet the search criteria

•Then it will pass these files (one at a time) as an argument to the command

•The find command starts a child shell for each argument, and runs the command inside it

•Example:

`$ find ~ -name “*.BAK” -exec rm {} ‘;’`

•Note, the use of {} and ;

•The {} is a place holder of where to place the file name in the command

•The ; is an indication to the end of the command

•The ; needs to be quoted or escaped to avoid interpretation by the shell

•Note that the {} can be used multiple times in the command,

`$ find ~ -name “*.java” -exec cp {} {}.old \;`

## Archiving Files

•Archiving is to combine a group of files organized in a tree structure into one file

•This enables easier handling, such as for backup or transfer purposes

•This is a separate procedure from compression

•The tool used for archiving files is `tar`

**(tar Command)**

`$ tar <options> <destination archive file> <directories/files to archive>`

•This command is used to archives a group of files/directories into a single tar file

•It is also used to un-archive a tar file into its original directory tree structure

•To archive (tar) a group of files and directories,

```
$ tar cvf <archiveFile.tar> <a set of files and directories>
•‘c’ for create
•‘v’ for verbose
•‘f’ for file
```

•Examples:

`$ tar cvf my-docs.tar ~/Documents/pdfs/`

`$ tar cvf selected-files.tar ~/file-1.txt ~/Documents/file-2.txt ~/*.pdf`

•Now we have the tar file, and we can do the following with it,

•To un-archive (un-tar) a file into all of its original components

`$ tar xvf <archiveFile.tar>`
`‘x’ for extract`

•To extract some of the files/dirs from a tar file

`$ tar xvf <archiveFile.tar> <files/dir to untar>`

•To show the contents of a tar file

`$ tar tvf <archiveFile.tar>`

```
•Examples:
$ tar cvf tar-file.tar *.pdf *.txt
$ tar tvf tar-file.tar
$ tar xvf tar-file.tar *.pdf
$ tar xvf tar-file.tar
```

•Let us say, we need to archive all pdf files in our home directory.

•We will need the find command to search for those files

•The outcome of the find command is then passed to the tar command

•This can be achieved by using a pipe,

`$ find ~ -name ‘*.pdf’ | tar cvf file.tar`

•Another way to achieve the same target is to use the tar command as the user defined command to be executed inside the find command

`$ find ~ -name ‘*.pdf’ -exec tar cvf file.tar ‘{}’ ‘+’`

**Compressing Files**

•Compressing files is the procedure of reducing the size of the file by a tool that removes any redundant data in the file

•There are multiple formats for compressed files,

•‘.gz’  use the tools gzip, and gunzip

```
$ gzip <file> file is compressed into file.gz
$ gunzip <file.gz> file.gz is flattened into file
```

•Better compression ‘.bz2’  use the tools bzip2 and bunzip2

```
$ bzip2 <file>
$ bunzip2 <file.bz2>
```

•Even better compression ‘lzma’  use the tools lzma and unlzma
```
$ lzma <file>
$ unlzma <file.lzma>
```

•Note that these tools,

•They deal with a single file and not a group of files, to be able to compress a group of file in a directory tree, you need to archive them first

•They replace the file with its compressed/flattened version. The original file is deleted

**Accessing Compressing Text Files**

•If a text file is compressed to a .gz format, we can still access it without uncompressing it using a set of tools (Z-tools) `$ gzip my-file.txt`

•To view the file contents, we use the zcat command (similar to cat command for uncompressed text files) `$ zcat my-file.gz`

•If the file is long, and we need to view it page by page, we can use the commands zmore and zless (similar to more and less commands for uncompressed text commands)

```
$ zless my-file.gz
$ zmore my-file.gz
```

•We can also search inside the compressed text document via the zgrep and zegrep commands (similar to grep & egrep)


**Mixing Archive and Compression**

•Archiving means combining multiple files organized in a tree structure into a single file

•Compression is to reduce the size of a single file

•So if we want to perform both, we can do this in two steps,

```
$ tar cvf pdf-files.tar *.pdf (this will generate the pdf-files.tar)
$ gzip pdf-files.tar (this will generate the pdf-file.tar.gz)
```


•We can replace the gzip with any other compression tool (depending on the desired compression format)

•We can perform both tasks (archiving and compression) in a single step


**Using tar for Archive + Compress**

```
$ tar <options> <compressed file> <files or folders>
$ tar <options> <compressed file>
```

•With the right set of options to the tar command, we can perform both archiving and compression (to the desired compression format)

1.Add the option `z` to perform gzip or gunzip

2.Add the option `j` to perform bzip2 or bunzip2

3.Add the option `--lzma` to perform lzma or unlzma

```
•Examples:
$ tar cvzf my-file.tar.gz ~/Documents/*.doc
$ tar xvzf my-file.tar.gz
$ tar xvjf file.tar.bz2
$ tar cvf --lzma my-file.tar.lzma ~/my-project/
$ tar tzvf my-file.tar.gz
```


**(the rar Command )**

•The rar tool can be used to archive + compress or extract + deflate files to/from the .rar format archive file

•The tool need to be installed first

`$ sudo apt-get install rar`

•The rar tool is very powerful tool, we will only cover the basics of it

•To add a file (group of files) to a rar archive

`$ rar a my-archive.rar ~/project/*.pdf`

•This will add the pdf files to the my-archive.rar archive.

•If the archive does not exist, it will be created

•If archive exists, it will be appended with these files

•To lock the archive to stop more file additions

`$ rar k my-archive.rar`

•To list the contents of the archive, `$ rar l my-archive.rar`

•To delete a file from the archive `$ rar d my-archive.rar my-file.pdf`

•To extract the files in the current directory without maintaining the original hierarchy (flat set of files, without creating subdirectories

```
$ rar e my-archive.rar
$ rar e my-archive.rar file-1.pdf
```

•To extract the files in the proper file hierarchy (to maintain the directory structure). This created subdirectories inside the current directory

```
$ rar x my-archive.rar
$ rar x my-archive.rar file-2.pdf
```

•Let us assume we are archiving all your project files `$ rar a my-archive.rar ./my-project`

•Then we modified some of the files that has been archived

•Now we need to update the archive with the new modified files

```
$ rar f my-archive.rar (only refreshes the local files)
$ rar f my-archive.rar * (refreshes all subdirectories as well)
```

**(the zip/unzip tool)**

•The tools `zip`  and `unzip` can perform windows format ‘.zip’

•Note that those tools perform both archiving and compression

```
$ zip -r file.zip ~/my-documents/ (r for recursive)
$ unzip file.zip
```

•Note:

•If we use ‘zip’ on a directory to file.zip and that file already exists, then file.zip will be updated,

•New files added

•Modified files updated



















































