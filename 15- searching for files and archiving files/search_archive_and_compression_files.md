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
































