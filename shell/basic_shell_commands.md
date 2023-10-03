## Basic Shell Commands

Note: Please look carefully through the commands and try to find examples of their usage on practice

**manual**

man – main UNIX help. This is a command for working with system manual. Each page argument given to man is normally the name of a program, utility or function. A section, if provided, will direct man to look only in that section of the manual. The default action is to search in all of the available sections.

- man cat - Get full guide for “cat” command
- man man - Prints a list of options and description of man command
- man -k - list Prints a list of commands contains “list” in description
- man -f ls  - Get short description of “ls”

**information**

info – information pages for commands, developed by GNU project.

- info cat - Get full guide for “cat” command
- info info - Prints a full description of info command

**list of files**

ls – view information about files or directories (list).

- ls -la - List files, use a long listing format,do not ignore entries starting with.
- ls -lh - List files, use a long listing format, print human readable sizes (e.g., 1K 234M 2G).
- ls -lt - List files, use a long listing format, sort by modification time, newest first.
- ls -lSh - List files, use a long listing format,sort by file size (largest first),print human readable sizes.

```bash
ls -lSh
```
total 16M
-rw-r--r-- 1 vagrant vagrant 10M Aug 23 15:55 file10
-rw-r--r-- 1 vagrant vagrant 5.0M Aug 23 15:55 file5
-rw-r--r-- 1 vagrant vagrant 1.0M Aug 23 15:55 file1

**pwd**

pwd – print working directory - shows full path for current directory.

```bash
pwd
```
/home/vagrant

**cd** – change current directory

Environment variable $HOME is the default dir. The variable $CDPATH defines the search path for the directory containing dir. Alternative directory names in $CDPATH are separated by a colon (:). A null directory name in $CDPATH is the same as the current directory, i.e., ".". If dir begins with a slash (/), then $CDPATH is not used.

cd / - change current directory to / - roof folder of a filesystem

cd .. - change current directory the parent of the previous one directory

cd ~ - change current directory to user's home dir.

cd - - change current directory to the previous one

```bash
pwd
```
/home/vagrant

```bash
cd /tmp
```

```bash
 pwd
```
/tmp

```bash
cd -
```
/home/vagrant

```bash
pwd
```
/home/vagrant 

```bash
cd - 
```
/tmp 
```bash
pwd
```
/tmp

**touch** - create an empty file / change time label for given file with parameter:

    -d, --date=STRING

parse STRING and use it instead of current time. STRING is a mostly free format human readable date string such as "Sun, 29 Feb 2004 16:21:42 -0800" or  
"2004-02-29 16:21:42" or even "next Thursday"

```bash
touch newfile.txt
ls -l newfile.txt
```
-rw-rw-r-- 1 vagrant vagrant 0 Aug 23 16:16 newfile.txt
```bash
touch -d "next Friday" newfile.txt
ls -l newfile.txt
```
-rw-rw-r-- 1 vagrant vagrant 0 Aug 30 2019 newfile.txt  

**mkdir** - make directory - create an empty directory  

    -m, --mode=MODE  

set file mode (as in chmod), not a=rwx - umask  

    -p, --parents  

no error if existing, make parent directories as needed  

```bash
mkdir empty
ls -l
```
total 0  
drwxrwxr-x 2 vagrant vagrant  6 Aug 23 16:26 empty

```bash
mkdir -p dir/test{1..3}/empty
tree
```
.  
└── dir  
    ├── test1  
    │   └── empty  
    ├── test2  
    │   └── empty  
    └── test3  
        └── empty  

**cp** - copy file / directory with all subdirectories  

    -p same as --preserve=mode,ownership,timestamps  

    --preserve[=ATTR_LIST]  

preserve the specified attributes (default: mode, ownership, timestamps), if possible additional attributes:  context,  links, xattr, all

    -R, -r, --recursive  

copy directories recursively  

    -i, --interactive

prompt before overwrite (overrides a previous -n option)

```bash
cp -r dir dir2/
tree dir2/
```
dir2/  
└── dir  
    ├── test1  
    │   └── empty  
    ├── test2  
    │   └── empty  
    └── test3  
        └── empty  

**mv** – move or rename file / directory.

    -i, --interactive

prompt before overwrite

    --backup[=CONTROL]

make a backup of each existing destination file, like --backup but does not accept an argument

    -S, --suffix=SUFFIX

override the usual backup suffix

    -u, --update

move only when the SOURCE file is newer than the destination file or when the destination file is missing

```bash
tree
```
.  
├── dir  
│   └── newfile  
└── newfile  

```bash
mv -b -S ".old" newfile dir/
tree 
```
.
└── dir
    ├── newfile
    └── newfile.old

**cat** – concatenation - display content of file or combine files into a single file.

```bash
echo 1 > 1.txt
echo 2 > 2.txt
cat 1.txt 2.txt > 3.txt
cat 3.txt 
```
1  
2  

**rmdir** - remove directory - remove empty directory  

**rm** - remove file or directory, remove (unlink) the FILE(s).  

Note: that if you use rm to remove a file, it might be possible to recover some of its contents, given sufficient expertise and/or time. For greater assurance that the contents are truly unrecoverable, consider using shred.

    -f, --force

ignore nonexistent files and arguments, never prompt

    -r, -R, --recursive

remove directories and their contents recursively

```bash
rm -v ~/1.txt 
```
removed '/home/vagrant/1.txt'
```bash
rm -rfv dir/
```
removed 'dir/newfile.old'  
removed 'dir/newfile'  
removed directory: 'dir  

### Work with environment variables

There are several commands available that allow you to list and set environment variables in Linux:

**env** – The command allows you to run another program in a custom environment without modifying the current one.  
Note: When used **without** an argument it will print a list of the **current environment variables**.  

**printenv** – The command **prints all** or the **specified** environment variables.  

**set** – The command sets or unsets shell variables.  
Note: When used **without an argument** it will print a list of **all variables including environment and shell variables, and shell functions.**  

**unset** – The command deletes shell and environment variables.  

**export** – The command sets environment variables.  

Please run through the expamples by the [link](https://linuxize.com/post/how-to-set-and-list-environment-variables-in-linux/).  

### View file content

**more** is an old utility. When the text passed to it is too large to fit on one screen, it pages it. You can scroll down but not up.  

**less** was written by a man who was fed up with more's inability to scroll backwards through a file. He turned less into an open source project and over time, various individuals added new features to it. less is massive now. That's why some small embedded systems have more but not less.  

    /pattern

**Search forward** in the file for the N-th line containing the pattern.  N defaults to 1.  The pattern is a regular expression, as recognized by the regular expression library supplied by your system.  The search starts at the first line displayed.  

    ?pattern

**Search backward** in the file for the N-th line containing the pattern. The search starts at the line immediately before the top line displayed.  

n - Repeat dprevious search, for N-th line containing the last pattern.  

N - Repeat previous search, but in the reverse direction.  

**head** - output the first 10 lines of a file.  

    -n, --lines=[-]K

print the first K lines instead of the first 10; with the leading '-', print all but the last K lines of each file  

**tail** - output the last 10 lines of a file.  

    -n, --lines=K

output the last K lines, instead of the last 10; or use -n +K to output starting with the Kth  

    -f, --follow[={name|descriptor}]

output appended data as the file grows  
