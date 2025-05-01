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

## Navigating the File System (Video 3)

## Exploring the Output of the ls Command (Video 4)

## Create and Remove Directories (Video 5)

## Copy, Move, and Delete Files and Directories (Video 6)

## Find Files from the Command Line (Video 7)

## Understand User Roles and Sudo (Video 8)

## Understand File Permissions (Video 9)

## Create Hard and Symbolic Links (Video 10)

## Challenge & Solution: Fix Broken Syntax (Video 11 & 12)

## Challenge & Solution: Practice working with files (Video 13 & 14)