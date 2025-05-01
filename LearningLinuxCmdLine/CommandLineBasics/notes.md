# Notes: Command-Line Basics (Section 2)

## What is the command line (video 1)

### Command-Line Interface

A text only user interface used to interact with computer systems that were not designed with a graphical user interface (GUI)

- Allows user to interact with programs via text commands
- Reads text inputs and outputs text to the screen
- can read and write from files and network

### What is Bash

A widely used shell (command-line interpreter)

- released in 1989 and is named the Bourne Again SHell
- builds upon earlier shells like Bourne and Thompson shells
- Many other shells to learn

### Where Can I use Bash

Bash is the default shell for many Linux distributions

- Available on Windows via Windows Subsystem for Linux
- Available on macOS, however it is an outdated version

### Using a Terminal

- A shell runs in a terminal application
- Common to work with more than one shell instance open at the same time and/or in conjunction with a GUI
- Often included in software applications or development tools (e.g. IDE)

### Terminal Terms

1. **Command-Line Interface (CLI)**: any place where a user can enter text commands
2. **Shell**: A piece of software that interprets typed/text commands and runs them
3. **Terminal**: Software that a shell program runs inside of

## Understand How Commands Are Structured (Video 2)

### General Command Syntax

General structure follows the ... format:

1. command ***Required***
    - ls
    - sort
    - grep
2. option(s) ***Optional***
    - -lh
    - -u
    - -i "needle"
3. argument(s) ***Optional***
    - /usr/bin
    - users.txt
    - haystack

```Bash
ls -lh /usr/bin
sort -u users.txt
grep -i "needle" haystack
```

### What Are Commands

Commands are programs that are available on a system (instructions for the shell in how to do something)

- When a command is run, the sytem will perform a specific action
- Many commands have shortened names in order to save typing
- Common commands include: ls, du, cat, df, grep, etc.

### What are Options

Options tell a command how to operate (provide additional instruction)

- Often begin with a dash (e.g. -e or -s)
- Most commands have multiple options that can be used individually or together
- example: `ls -l -a -h` or `ls -lah` (order dosen't always matter for some combinations of options)
- Some options start with 2 dashes, and cannot be truncated together
- example: `ls --group-directories-first --human-readable`

### What are arguments

Arguments tell the command what to operate on

## Write Commands in a Shell at the Prompt (Video 3)

```Bash
~$ ls
```

returns list of contents of current directory

```Bash
~$ ls -l
```

changes the format of output to display additional information (Long Listing)

```Bash
~$ list
```

outputs an error: "Command 'list' not found, did you mean:" and a list of available commands

### Troubleshooting Commands

Spelling must be exact when entering commands into terminal

- spacing(whitespace) matters
- spelling of command names, options, and arguments matters
- Misspelled commands usually just fail, and usually won't cause catastrophic problems
- Mistyped options or argument ***CAN*** cause unexpected outcomes or data loss
- ***ALWAYS DOUBLE CHECK SPELLING BEFORE RUNNING A COMMAND***

### What Commands Can I Use

Most commands are programs installed on the system

- Many common utilities come from GNU coreutils
- System provides ways for finding programs

## Finding help for commands (Video 4)

It isn't Neccessary to memorize every shell command or option, there are resources that contain that information

### Manual Pages

The `man` command opens the manual pages

- These are built-in documentation for commands
- example: `man ls` to open manual page for ls command

The `--help` option gives a brief explanation of the command, and refers to other resources if still stuck

- example: `ls --help`
- Also a generic `help` command

The `apropos` command is a command search program that uses provided argument to look for commands

- example: `apropos list`

It is helpful to keep a personalized refference sheet of commands and options that you use relatively often

## Helpful Keyboard Shortcuts in the Terminal (Video 5)

### Usefule Keyboard Shortcuts

1. Tab completion: Automatically completes a file/dir/command name
    - example: `ls -l Desk` can be tabbed to autocomplete Desktop/ if a directory of that name exists
    - This will not work if there are multiple files or directories that are similarly named
    - can also be used with commands
2. Text Navigation
    - Ctrl-A (^A): Move to begining of line
    - Ctrl-E (^E): Move to end of line
    - ^U: Delete from cursor to line start
    - ^K: Delete from cursor to line end
    - Ctrl-Shift-C: Copy selected text to clipboard
    - Ctrl-Shift-V: Paste text from clipboard
    - Up arrow: Recall previous command
    - Down Arrow: scroll other direction as up arrow
    - ^R: Search command history
    - ^C: Cancel command

### What is a line in terminal

A line is any text we type into prompt before pressing return

- Long commands can wrap at the window boundary, but are still one line

## Challenge & Solution: Find Command Information (Videos 6 & 7)

### Challenge: Answer following Questions

1. What does the command `stat myfile.txt` do?
2. What does `df -h /` do?
3. What command searches for files in a directory hierarchy?
4. Which option for ls ouputs a comma-separated list of files and directories?

### Solutions

1. Displays status and statistics of myfile.txt
2. shows disk utilization of root file system in human readable format
3. apropos "search for files", which returns the **find** command
4. ls -m
