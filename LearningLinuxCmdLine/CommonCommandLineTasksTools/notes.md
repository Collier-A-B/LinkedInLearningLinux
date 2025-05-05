# Notes: Common Command-Line Tasks and Tools (Section 4)

## The Unix Philosophy (Video 1)

### UNIX Philosophy

1. Tools should do one thing and do it well
2. Tools should use text interfaces (text input and output)
3. Tools should be designed to be used together in different ways
4. Standard GNU coreutils follow this pattern
5. Use each tool for it's dedicated function, and combine tools to accomplish the specific task

Analogy: A well stocked kitchen with specialty tools instead of multi-purpose instruments  
OR  
Assembly Line with each person/robot having one job

## Use Pipes to Connect Commands Together (Video 2)

### Pipes

Take output of one command and send it to another

- chain/link commands together to accomplish a complex task

Pipe Character: | ( or shift-\\ )

```bash
echo "Hello World From the Command Line" | wc
```

## View Text Files With Cat, Head, Tail, and Less (Video 3)

### Tools for Text

`cat`:

- Concatenate or link together
- Can be used to output text-files to screen or another program

```bash
cat poems.txt
```

`head` & `tail`:

- View lines from beginning or end of file

```bash
head poems.txt
tail poems.txt

head -n5 poems.txt
tail -n3 poems.txt

cat poems.txt | cat -n | tail -n5
cat poems.txt | tail -n5 | cat -n
```

`less`:

- Displays text on one page or screenful at a time
- includes navigation controls to view different pages

```bash
less poems.txt

cat poems.txt | less
```

## Search for Text In Files and Streams With Grep (Video 4)

### Searching for Text

`grep` command searches files for text patterns

- patterns can be explicit/specific or use expressions
- -n: display line number of lines that contain "the"
- -i: case insensitive option ("the", "THE", "The", etc.)
- -v: drop lines that contain "the"
- -E: regex option
- [hijk]: search for chars 'h', 'i', 'j', 'k'
- \w{6,}: search for words that contain at least 6 chars

```bash
grep "the" poems.txt
grep -n "the" poems.txt
grep -i "the" poems.txt
grep -v "the" poems.txt

grep -E "[hijk]" poems.txt
grep -E "\w{6,}" poems.txt
```

### Using Regular Expressions

- Powerful way of searching for matching text

## Manipulate Text With Awk, Sed, and Sort (Video 5)

### Tools for working with Text

1. `awk`
    - Often used to extract specific text from a file according to provided rule
    - awk programs can be written at cmd line or stored in file
2. `sed`
    - Is a stream editor
    - Often used for modifying text in cmd pipeline or in place
3. `rev`
    - Prints text in reverse sequence
4. `tac`
    - Concatenates/displays files in reverse
5. `tr`
    - translates/modifies individual chars according to parameters

### awk

Line nums:  
(don't count blank lines)

1. prints columns 2 & 1, in that order
2. pipes output of line1 to sort command (numeric sort of id column)

```bash
awk '{print $2 "\t" $1}' simple_data.txt

awk '{print $2 "\t" $1}' simple_data.txt | sort -n
```

### sed

Line nums:  
(don't count blank lines)

1. change every occurence of "Orange" with "Red" ("s/" means substitute)

```bash
sed s/Orange/Red/ simple_data.txt
```

### sort

Line nums:
(don't count blank)

1. alphabetical sort of first column
2. numerical sort of second column
3. sort only unique lines

```bash
sort simple_data.txt

sort -k2 -n simple_data.txt

sort -u dupes.txt
```

## Edit Text With Vim (Video 6)

### Editing Text with Vim

- Vim is an improved version of vi tool text editor that is available at the cmd line
- Compared to modern, graphical text editors, it has a steep learning curve to master
- VIM: Vi IMproved

### Vim in Ubuntu

`vi` or `vim` are the commands to open vim, depending on linux distro in use

- Two open an existing file, add the file name as a parameter
- To create a new file, no param is necessary

There are two main modes when working in vim

1. Insertion: equivilent to an edit mode, where changes can be made to a file
2. Command: equivilent to a toolbar with save, quit, and other commands

To enter command mode, press the Escape key  
To enter insertion mode(at cursor location), press the i key  
To enter insertion mode(at begining of line), press Shift-i  
To enter insertion mode(at next line), press o key

### Common Commands Within Vim

1. `:w file_name.txt`
    - saves the changes to a newly created file of name "file_name.txt"
    - if the file has already been created, `:w` is sufficient
2. `:q!`
    - quit command that exits vim
    - ***NOTE***: This does not automatically save any changes made or create new files. This must be combined with or preceded by `:w` to save changes

    ```vim
    :wq
    
    :w
    :q
    ```

## Edit Text With Nano (Video 7)

### Editing Text with Nano

- Nano is a lightweight and user-friendly txt editor
- preinstalled on some linux distros (such as Ubuntu Desktop)

### Nano in Ubuntu

`nano` command opens a file in the editor

- enter file-name as param to open an existing file
- commonly used commands are displayed at the bottom of the editor
- To page up and down, use ^v and ^y

### Which is better

Whichever one enables you to complete the task a hand

- Text editors, IDE's, Programming Languages, etc. are tools, and each has it's advantages and disadvantages. There is no simple answer to which is better or worse in the vast majority of cases.

## Working With Tar and Zip Archives (Video 8)

### Tape Archives

The idea is to store multiple files on one large file, since this is more space efficient than storing each file seperately

- .tar files are example of this type of file archive
- .tar files don't always use data compression, but it is an option
- Compresses .tar formats include: **.tar.gz**, **.tgz**, and **.tar.bz2**
- more commonly used in linux distros than other major operating systems

### Tar Archives in cmd line

Line Nums

1. Creates a tar archive of the files in MyDirectory/
    - -c: option to create an archive
    - -v: option to list out every file added to archive
    - -f: creates a file from the output
    - myfiles.tar: name of file archive to create
    - MyDirectory: name of directory to archive (can add multiple directories and files after this param to add more stuff to archive)
2. Creates a compressed tar archive
    - -a: option for compression
    - -z: option to specify a compression format (not used in line, but useful info)
3. same as line2, with different compression format
4. move archive
    - (since you may not know what is in an archive, it's a good idea to unpack archives in their own dir, so you differentiate the new files from your existing ones)
5. change dir
6. unpacks the archive into the cwd
7. change dir
8. unpacks archive into specified dir
    - -C: specify a dir to unpack files to

```bash
tar -cvf myfiles.tar MyDirectory/
tar -caf myfiles.tar.gz MyDirectory/
tar -caf myfiles.tar.bz2 MyDirectory/

mv myfiles.tar.bz2 unpack1/
cd unpack1/
tar -xf myfiles.tar.bz2

cd ..
tar -xf myfiles.tar.gz -C unpack2
```

### Data Compression

zip files are a type of archive that uses data compression

- often more compatible across various OS's

### Zip files in Ubuntu

Line nums

1. creates zip archive of MyDirectory/
    - -r: option to include directory to zip
2. move archive
3. change dir
4. unpack the archive
5. change dir
6. unpack archive to specified dir
    - -d: option to specify the directory to unpack files to

```bash
zip -r exfiles.zip MyDirectory/

mv exfiles.zip unpack3
cd unpack3
unzip exfiles.zip

cd ..
unzip unpack3/exfiles.zip -d unpack4
```

## Challenge & Solution: Create and Share a File (Video 9 & 10)

### Challenge

1. Create a .txt file
2. Ensure that any user can read and write it
3. Compress the file using tar or zip

```bash
touch hello_world.txt
nano hello_world.txt

stat hello_world.txt
chmod a+w hello_world.txt
chmod a+r hello_world.txt

zip -r archive.zip hello_world.txt
unzip archive.zip -d unpack
```

### Solution

```bash
vi newfile

stat newfile
chmod a+rw newfile
stat newfile

tar -czf mynewfile.tgz mynewfile
```

## Output Redirection (Video 11)

### Redirection

- Text in a shell travels through one of three streams
- Text can be redirected to screen or to files

|         Stream         |Number|    Usage   |
|------------------------|------|------------|
| Standard Input (stdin) |   0  | Text Input |
|Standard Output (stdout)|   1  | Text Output|
| Standard Error (stderr)|   2  | Error Text |

Line nums

1. redirect ouptut of command (stdout) to filelist.txt
2. same as line1

```bash
ls 1> filelist.txt
ls > filelist.txt

ls notreal 2> filelist_error.txt

ls > filelist2.txt
echo "appended txt" >> filelist2.txt
cat filelist2.txt
```

## Exploring Environment Variables and PATH (Video 12)

`env` command displays environment variables (PATH is most important for now)

### PATH

PATH is a list of paths or directories where the shell is told to look for programs/executables/etc. it may need to run

Examples:

- various linux commands in this course
- Programming language interpreters/compilers installed on a machine

### Editing the $PATH Variable

- We can modify where the system looks for executables
- This is most commonly needed when a program is stored in a non-standard location in a file system
- Edit the shell profile file in ~/.bash_profile (a hidden dir in user's home dir)

`ls -a` shows all directories within the cwd (including hidden ones)

## Challenge & Solution: Extract Information from a Text File (Video 13 & 14)

### Challenge

1. Extract log.tar.gz
2. Look for unauthorized connection attempts
3. Extract the usernames attackers tried to use
4. Create a file containing these names (Organize it)
5. Use various tools to explore/process the log

### Solution

```bash
tar -xf Exercise\ Files/log.tar.gz -C CommonCommands/challenge_two/

less auth.log
cat auth.log | grep "input_userauth_request" | awk '{print $9}' | sort -u > invalid_users.txt
```
