# Notes: Files, Directories, and Permissions (Section 3)

## The Linux file System (Video 1)

### Commands for File Information

- file: determine file type
- stat: display file status

### How Directories Are Organized

- File system keeps track of and represents files on the system's storage
- Filesystem Hierarchy Standard (FHS) defines common locations for files across many Linux distributions

### Notable File System Directories

1. File System Root: /
    - Highest level of the file system hierarchy
    - all other directories are accessible via the root 
2. User home directories: /home
    - where each user's personal directory is stored
    - example: /home/collier/...
    - In bash and other shells, the home directory for a user is represented as ~
3. Root user's home directory: /root
    - **When people refer to the root, they usually mean the root of the file system, not the root home directory**
4. Common configuration files: /etc
5. Common programs or commands: /bin or /sbin
6. shared libraries and modules: /lib
7. standard location for mounting other file systems: /mnt, /media
8. Kernel and System information: /dev, /proc, /sys

## Understanding File Paths (Video 2)

### Paths in Linux

`Path`: a representation of the location of a file or directory

- Paths use the forward-slash character (/) as a seperator between directory or file names
- Two types of Paths: Absolute and Relative

### Absolute Paths

The explicit location of a file or dir in a file system, begining at the root of the file system  
In Linux, an absolute path always begins with a /

Examples Include

- /home/scott/
- /hoome/scott/Documents/test.txt

### Relative Paths

The relative location of a file or dir, often begining at the current working directory

- If the current working directory changes, what the path refers to changes
- the name ".." refers to the parent directory of the current working directory. These can be strung together to move up in the file system hierarchy

### Tilde Expansion

Reminder, the ~ char refers to the current user's home directory

For example, a user's documents folder can be represented as `~/Documents`

The shell expands the ~ to the path of the user's home directory when executing commands  
This abstracts the path to the user's home directory.  
using the ~ is an absolute path, but abstracts the path to the home directory so that it can be used like a relative path

## Navigating the File System (Video 3)

Use the cd command to navigate file system 

- Arguments are in the form of file paths, relative to the current working directory (CWD) or using an absolute path
- for example: `cd ~/Documents` uses the absolute path to the Documents folder in the users home directory
- `cd Exercise\ Files` or `cd "Exercise Files"`

## Exploring the Output of the ls Command (Video 4)

`ls` command lists the contents of the CWD

Options for ls:

- `--color=always` or `-g` ensures the output uses a color scheme
- `-l` displays additional information about files and directories within the cwd
- `-h` displays the output in human readable format

## Create and Remove Directories (Video 5)

### Create Directories

Use mkdir command to make a new directory within the CWD or in a specifc directory by specifying a path

```bash
mkkdir department/custom-dir
mkdir custom-dir-two
mkdir ~/cusom-dir-three
```

To make multiple directories at once  
-p tells bash to create legal dir and create contracts dir inside it

```bash
mkdir departments/customer-service departments/health-human-services
mkdir -p departments/legal/contracts
```

### Remove Directories

Use rmdir command to remove an EMPTY directory

```bash
rmdir departments/legal/contracts/
rmdir departments/legal
```

## Copy, Move, and Delete Files and Directories (Video 6)

### Copy

`cp` is the command for copy

```bash
cp poems.txt poems2.txt
cp text.txt departments/hr/employee\ info/
cp text2.txt departments/hr/employee\ info/new-text.txt
```

### Move

`mv` is the move command  
This command has two functions

- move a file from one directory to another
- rename a file and place it in the same directory

```bash
mv poems2.txt departments/marketing
mv poems1.txt poems11.txt
```

To move a file from a specified dir to the cwd

```bash
mv departments/marketing/poems2.txt .
```

### Wildcard characters

- *: apply the command to every instance that matches the argument
- ?: apply the command to one instance that matches the argument

```bash
mv *.txt ~/Documents/text-files/
mv ~/Documents/text-files/* .
```

### Remove files

`rm` is the remove/delete command  
***This permanently deletes the file, so be carefull with this*** (unless you have special tools that can recover it)

```bash
rm ~/Documents/test-dir/duplicate-text.txt

cp poems.txt poems1.txt
cp poems.txt poems2.txt
cp poems.txt poems3.txt
rm poems?.txt
```

TO remove multiple files from a directory  
-r option tells the command to go to the /test-dir and recursively delete everything in it

```bash
rm -r Documents/test-dir/
```

## Find Files from the Command Line (Video 7)

`find` command is used to search for files and directories

```bash
find . -name "poe*"
find ~/Documents/ -name "poe*"
```

## Understand User Roles and Sudo (Video 8)

### Multiuser Environments

Systems that allow users' to seperate their files from other users

`su` command allows us to switch/substitute users at command line

Two types of users on Linux: 

1. Normal User
    - Can modify their own files
    - Cannot make system-wide changes (i.g. install software)
2. Superuser (root)
    - Can modify any file on system
    - Can make system-wide changes
    - It's not recommended to use a root account for normal activities, and is often disabled on modern Linux systems
    - System administrators can temporarily borrow root's priviledges with the sudo command

`sudo` command allows an administrator to exercise root priviledges in the command line

```bash
sudo ls /root
```

To relinquish root priviledges, use -k option  
To enable root priviledges indefinitely, use -s option  

- This will change the apperance of the command line

Otherwise, sudo will expire after a couple of minutes

## Understand File Permissions (Video 9)

### File Permissions

rwx  rwx   rwx     file1  
user group others

rwx: read, write, execute

### Changing File Permissions

`chmod`: changes permission mode string

```bash
chmod 644 test.sh
chmod a-x test.sh
```

`chown`: changes file owner

`chgrp`: changes file group

### Octal File Permissions

|      |read(4)|write(2)|Execute(1)|Result|
|------|-------|--------|----------|------|
|User  |   r   |    w   |     x    |   7  |
|Group |   r   |    -   |     x    |   5  |
|Others|   r   |    -   |     -    |   4  |

Based on binary number system  
Letter indicates a 1, - indicates a zero  
therefore, rwx == 111 == 7

| Octal Value | Mode | Octal Value | Mode |
|-------------|------|-------------|------|
|      0      |  --- |      4      |  r-- |
|      1      |  --x |      5      |  r-x |
|      2      |  -w- |      6      |  rw- |
|      3      |  -wx |      7      |  rwx |

### Symbolic File Permissions

|         |read(r)|write(w)|Execute(x)|Mode |
|---------|-------|--------|----------|-----|
|User(u)  |   +   |    +   |     +    |u+rwx|
|Group(g) |   =   |        |          | g=r |
|Others(o)|   -   |        |          |o-rwx|
|All(a)   |   =   |    =   |     =    |a=rwx|

- +: adds permission (only changes specified values)
- -: removes permission (only changes specified values)
- =: removes previous mode and sets to new mode

|Octal Value|Symbolic Value|  Result |
|-----------|--------------|---------|
|    777    |     a=rwx    |rwxrwxrwx|

## Modify File Permissions (video 10)

`cat` command ouptuts(reads) contents of a file

```bash
cat test.sh
```

To write in a file, open it in a text editor (vim, nano, etc.)

## Create Hard and Symbolic Links (Video 11)

### Links

Links are files that reference other files

- Avoids duplication of files
- Establishes a ptr in one place to a destination in another

Two types of Links:

1. Hard Link: points to specific data (inode) on the disk
2. soft/symbolic link (symlink): points to another file

```bash
ln -s poems.txt writing.txt
ln poems.txt words.txt
```

-s creates a symbolic link

## Challenge & Solution: Fix Broken Syntax (Video 12 & 13)

Correct the following commands and describe errors in each

1. cd ~/home/scott
2. LS /home
3. mv ~/log.tar.gz home scott
4. chmod ~/log.tar.gz

Answers

1. ~/ -> /home/scott is redundant in the original
2. ls /home -> LS not valid command
3. mv ~/log.tar.gz /home/scott -> home scott is invalid path
4. chmod 644 ~/log.tar.gz  -> missing octal mode argument

## Challenge & Solution: Practice working with files (Video 14 & 15)

