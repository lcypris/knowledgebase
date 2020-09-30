# The Unix Shell
The following notes summarize the [Onlinekurs](http://swcarpentry.github.io/shell-novice/)

## Introducing the Shell
* command-line interface (CLI) and scripting language
* repl console – read, evaluate, print, loop

|Command||
|-|-|
|`%`|**promt** indicating that the shell is waiting for input|
|`ls`|**listing** list the content of the current directory|
|`Ctrl`+`A`|moves to the beginning of a line|
|`Ctrl`+`E`|moves to the end of a line|

## Navigating Files and Directories
* **file system** part of the operating system responsible for managing files and directories
* **files** hold information
* **directories** (also called 'folders') hold files or other directories
* **root directory** holds everything else, refered to by using `/`
* `bin` where some built-in programs are stored
* `data` for miscellaneous data files
* `Users` where users' personal directories are located
* `tmp` for temporary files that don't need to be stored long term

|Command||
|-|-|
|`pwd`|**print working directory** prints current working directory|
|`ls -F`|**`-F option`** classifies the output|
||`/` indicates a directory|
||`@` indicates a link|
||`*` indicates an executable|
||*no classification symbol* files|

### General syntax of a shell command

example `ls -F`

|Component||
|-|-|
|`ls`| **command**|
|`-F`|**option** (also calles **switches** or **flags**), changes behavior of command|
|`/`|**argument**, tells command what to operate on (e.g. files and directories|

* sometimes options and arguments are referred to as **parameters**
* a command can be called with more that one option and more than one argument but doesn't always require an argument or an option
* each part is seperated by spaces
* capitalization can be important

### Getting help

* `man ls`- description of the command and its accepted options
* **navigate** with arrow up/down to move line-by-line or `B`and `Spacebar`to skip up/down by a full page
* **search** for character/word in the `man`page by using `/` followed by the character/word
* move between hits using `N` (forward) and `Shift`+`N` (backward)
* **quit** press `Q`

### Exploring Other Directories

|Command||
|-|-|
|`ls Desktop`|lists contents of other directory that the current working directroy|
|`cd`|change working directory (only to sub-directories inside current directory)|
|`cd ..`|go to the directory containing current directory| 
|`.`|current directory| 

* **relative path** specifies a location from current working directory
* **absolute path** specifies a location from the root of the file system/ 
e.g. `cd /Users/lcypris/Desktop/data-shell/data`
* `TILDE`- the current user's home directory (`/Users/lcypris)
* `cd -` - previous directory I was in
* `cd ../..`- goes up two levels

## Working with Files and Directories

### Creating directories

|Command||
|-|-|
|`mkdir name`|creates new directory called name; created in the current working directory|
|`mkdir -p name/chapter_1/section_1/subsection_1`|creates a directory with any number of nested subdirectories|

### Create a text file

|Command||
|-|-|
|`nano draft.txt`|runs text editor Nano if file doesn't exist, it will be created|
|`touch my_file.txt`|generates new file in current working directory|

* **filename extension** indicates what type of data the file holds

### Moving files and directories

|Command||
|-|-|
|`mv old new`|renames/moves file; overwrites any existing file with the same name|
|`mv -i`|asks for confirmation before overwriting|


### Copying files and directories

|Command||
|-|-|
|`cp old new`|copies file|
|`cp -r thesis thesis_backup`|copies a directory and all its contents|

### Removing files and directories

|Command||
|-|-|
|`rm quotes.txt`|removes file – no trash bin!|
|`rm -r thesis`|removes directory and all its contents|

### Operations with multiple files and directories

* given more than one file name followed by a directory name (i.e. the destination directory must be the last argument), cp copies the files to the named directory

#### Using wildcards for accessing multiple files at once

* `*` matches zero or more characters
* `?` matches exactly one character

## Pipes and Filters
* programming model called *pipes and filters* – creating lots of simple tools that each do one job well, and work well with each other
* **filter** transforms a stream of input into a stream of output

|Command||
|-|-|
|`wc`|counts lines, words, and characters in its inputs|
|`command > file`|**redirect** the command's output to a file instead of printing it to the screen; creates or overwrites file|
|`command >> file`|writes to a file, but appends the string to the file if it already exists|
|`cat`|'concatenate' i.e. join together, prints the contents of files one after another|
|`less`|displays a screenful of the file; go forward/backward with `spacebar`/`b`; quit with `q`|
|`sort`|alphanumerical sort|
|`sort -n`|numerical sort|
|`head -n 1`|prints the first line of the file (by default 10)|
|`tail -n 3`|prints the last three lines of the file|
|`echo`|prints strings|
|`|`|**pipe** tells the shell to use the output of the left command as the input of the right command; can be chained consecutively|
|`cut -d, -f 2`|cuts out second column; -d, **delimiter** defined as comma, by default space; -f specifies second column|
|`uniq`|filters out adjacent matching lines in a file|
|`cut -d , -f 2 animals.txt | sort | uniq -c`|shows total count of each type of animal in the file|
|`*[AB].txt`|'A or B'|

## Loops
* **loops** are a programming construct which allows us to repeat a command or a set of commands for each item in a list
* `echo` the commands which a loop would run before executing

|Command||
|-|-|
|`for thing in list_of_things
do
    operation_using $thing
done`||
|`history|tail -n 5|lists the last five executed commands (by default 100)|
|`!123`|repeats command #123|

## Shell Scripts
* **shell script** – a bunch of commands saved in a file

* `nano file` – creates and opens text file
* `head -n "$2" "$1" | tail -n "$3"`– in nano
* `bash file file number number` – arguments can be changed
* add comments with `#`at the top
* `$@`– all the command-line arguments to the shell script
* `bash -x`– causes `bash`to run in debug mode (prints out each command as it is run)

## Finding Things
* **grep** – contraction of *global/regular expression/print*, a common sequence of operations in early Unix text editors

|Command||
|-|-|
|`grep pattern file`|finds and prints lines in files that match a pattern|
|`grep -w`|limits matches to word boundaries|
|`grep -n`|numbers the lines that match|
|`grep -i`|makes search case-insensitive|
|`grep -v`|iverts search, i.e., outputs the lines that do not contain the pattern|
|||
|||
|`find`|finds files with specific properties that match patterns|
|`find .`|displays the names of every file and directory under the current working directory
|`find . -type d`|displays all directories|
|`find . -type f`|displays all files|
|`find . -name "*.txt"`|displays all text files; paranthesis prevent the shell from expanding the `*`wildcard|
|`wc -l $(find . -name ".txt")`|gives a list of all text files in or below the current directory and counts the lines in those files|
||`$()` gets executed first
