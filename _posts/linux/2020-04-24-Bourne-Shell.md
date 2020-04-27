---
layout : post
category : Linux
title : "The Bourne Shell: /bin/sh"
author : pu71n
---
The shell is one of the most important parts of a Unix system. A shell is a program that runs commands, like the ones that users enter. The shell also serves as a small programming environment. There are many different Unix shells, but all derive several of their features from the Bourne sell (/bin/sh), a standard shell developed at Bell Labs for early versions of Unix. Every  Unix system need the Bourne shell in order to function correctly. Linux uses an enhanced version of the Bourne shell called **bash** or the "Bourne-again" shell. The bash shell is the default shell on most Linux distributions, and /bin/sh is normally a link to bash on a linux system. 

### Standard Input and Standard Output 

Unix processes use I/O streams to read and write data. Processes read data from input streams and write data to output streams. Streams are very flexible. For example, the source of an input stream can be a file, a device, a terminal, or even the output stream from another process. Standard input and output are often abbreviated as **stdin** and **stdout**. There is a third standard I/O stream called standard error abbreviated as **stderr**. 

### Shell Globbing (Wildcards)

The shell can match simple patterns to file and directory names, a process known as *globbing*. This is similar to the concept of wildcards in other systems. The simplest of these is the glob character \*, which tells the shell to match any number of arbitrary characters. For example, this command "echo \*" prints a list of files in the current directory.
The shell matches arguments contaning globs to filenames, substitutes the filnames for those arguments, and then run the revised command line. The substituions is called **expansion** because the sehell subtitutes all matching filenames. Here are some ways to use \* to expand filenames : 
* at\* expands to all filenames that start with at. 
* \*at expands to all filenames that end with at. 
* \*at\* expands to all filenames that contain at. 

Another shell glob charcter, the question mark '?', instructs the shell to match exactly one arbitrary character. 

### Intermediate Commands 
* **grep** : The grep (Acronym for 'Global Regular Expressions Print') command prints the lines from a file or input stream that match an expression. Two of the most important *grep* options are -i (for case-insensitive matches) and -v (which inverts the search, that is, prints all lines that don't match).

* **less** : The *less* command comes in handy when a file is really big or when a command's output is long and scrolls off the top of the screen. Note that the less command is an enhanced version of an older program named *more*.  You can also search for text inside **less** or you can open a text editor by pressing v. 
* **diff** : To see the differences between two text files, use **diff**. 
* **file** : If you see a file and are unsure of its format, try using the *file* command to see if the system can guess. 
* **find and locate** : as expected, find is used to find files. The find command accepts special pattern-matching characters such as \*, but you must enclose them in single quote ('\*') to protect the special characters from the shell's own globbing feature. Most systems also have a **locate** command for finding files. The locate utility works better and faster than the find command counterpart because instead of searching the file system when a file search is initiated, it would look through a database. This database contains bits and parts of files and their corresponding paths on your system. By default, locate command does not check whether the files found in the database still exist and it never reports files created after the most recent update of the relevant database.
* **head and tail** : To quicky view a portion of a file or stream of data, use the *head* and *tail* commands. For example, *head* /etc/passwd shows the first 10 lines of the password file, and *tail* /etc/passwd shows the last 10 lines. To change the number of lines to display, use the -n options. 
* **sort** : The sort command quickly puts the lines of a text file in alphanumeric order. If the file's lines start with numbers and you want to sort in numercial order, use the -n option. The -r ioption reverses the order of the sort.

### Dot Files
Change to your home directory, take a look around with ls, and then run ls -a. Do you see the difference in the output? When you run ls without -a, you won't see **the configuration files called dot files**. These are files and directories whose names begin with a dot (.). Common dot files are .bashrc and .login, and there are dot directories, too, such as .ssh. 
There is nothing special about dot files or directories. Some programs don't show them by default so that you won't see a complete mess when listing the contents of your home directory. In addition shell globs don't match dot files unless you explicitly use a pattern such as .\*. 
### Environment and Shell Variables 
The shell can store temporary variables, called shell variables, containing the values of text strings. Shell variables are very usefull for keeping track of values in scripts, and some shell variables control the way the shell behaves. (For example; the bash shell reads the PS1 variable before displaying the prompr.)
To assign a value to a shell variable, use the equal sign (=). 
An *environment variable* is like a shell variable, but it's not specific to shell. Al processes on Unix systems have environment variable storage. The main difference between environment and shell variables is that the operating system passes all of your shell's environment variables to program that shell runs, whereas shell variables cannot be accessed in the commands that you run. Assign an environment variable with the shell's *export* command. Environment variables are useful because many programs read them for configuration and options. 
### The Command Path 
**PATH** is a special environment variable that contains the *command path*. A command path is a *list* of system directories that the shell searches when trying to locate a command. For example, when you run *ls*, the shell searches the directories listed in **PATH** for the ls program. If programs with the same name appear in several directories in the path, the shell runs the first matching program. If you run echo $PATH, you'll see that the path components are seperated by colons (:). To tell the shell to look in more places for programs, change the PATH environment variable.
### Special Characters 

<pre>
| Character | Name                         | Uses                                        |
|-----------|------------------------------|---------------------------------------------|
| \*         | Asterisk                     | Regular expression, glob character          |
| .         | dot                          | Current directory, file/ hostname delimiter |
| !         | bang                         | Negation, command history                   |
| |         | pipe                         | Command pipes                               |
| /         | (forward) slash              | Directory delimiter, search command         |
| \         | backslash                    | Literals, macros  (never directories)       |
| $         | dollar                       | Variable denotation, end of line            |
| '         | tick, (single) quote         | Literal strings                             |
| \`         | backtick, backquote          | Command substitution                        |
| "         | double quote                 | Semi-literal strings                        |
| ^         | caret                        | Negation, beginning of line                 |
| ~         | tilde, squiggle              | Negation, directory shortcut                |
| #         | hash, sharp, pound           | Comments, preprocessor, substitutions       |
| [ ]       | (square) brackets            | Ranges                                      |
| { }       | braces, (curly) brackets     | Statement blocks, ranges                    |
| \_         | underscore, under            | Cheap substitute for a space                |


</pre>

### Command-Line Editing
As you play with the shell, notice that you can edit the command line using the left and right arrow keys, as well as page through previous commands using the up and down arrows. This is a standard on most Linux systems. However, it's a good idea to forget about the arrow keys and use control key sequences instead. 

<pre>
| Keystroke     | Action                                            |
|---------------|---------------------------------------------------|
| Ctrl-B        | Move the cursor left                              |
| Ctrl-F        | Move the cursor right                             |
| Ctrl-P        | View the previous command (or move the cursor up) |
| Ctrl-N        | View the next command (or move the cursor down)   |
| Ctrl-A        | Move the cursor to the beginning of the line      |
| Ctrl-E        | Move the cursor to the end of the line            |
| Ctrl-W        | Erase the preceding word                          |
| Ctrl-U        | Erase from cursor to beginning of line            |
| Ctrl-K        | Erase from cursor to end of line                  |
| Ctrl-Y        | Paste erased text (for example, from Ctrl-U       |


</pre>

### Getting Online Help
Linux systems comes with a wealth of documentation. For basic commands, the manual pages (or *man pages*) will tell you what you need to know. Most manual pages concentrate primarily on reference information, perhaps with some examples and cross-references, but that's about. Don't expect a tutorial, and don't expect an engaging litery style. When programs have many options, the manual page often lists the options in some systematic way (for example, in alphabetical order), but it won't tell you what the important ones are. To search for a manual page by keyword, use the -k option.
Manual pages are referenced by numbered sections. When someone regers to a manual page, the section number appears in parentheses next to the name.

<pre>
| Section   | Description                                                          |
|-----------|----------------------------------------------------------------------|
| 1         | User commands                                                        |
| 2         | System calls                                                         |
| 3         | Higher-level Unix programming library documentation                  |
| 4         | Device interface and driver information                              |
| 5         | File descriptions (system configuration files)                       |
| 6         | Games                                                                |
| 7         | File formats, conventions, and encodings (ASCII, suffixes and so on) |
| 8         | System commands and servers                                          |

</pre>

You can select a manual page by section, which is sometimes important because *man* displays the first manual page that it finds when matching a particular search term. 

### Shell Input and Output
To send the output of *command* to a file instead of the terminal, use > redirection character.
---
$ command > file
---
The shell creates file if it does not already exist, If it exists, the shell erases (clobbers) the original file first. (Some shells have parameters that prevent clobbering. For example, enter set -C to avoid clobbering in bash)
You can append the output instead of overwriting it with the >> redirection syntax: 
---
$ command >> file
---
This is a handy way to collect output in one place when executing sequences of related commands. 
To send the standard output of a command to the standard input of another command, use the pipe character (|).
### Standard Error
Occasionally, you may redirect standard output but find that the program still prints something to the terminal. This is called **standard error** (stderr); it's an additional output stream for diagnostics and debugging. 
For example : 
- - - 
ls /pu71n > f
ls: cannot access /pu71n: No such file or directory
- - - 
After compilation, f should be empty, but you still see the following error message on the terminal as standard error. You can redirect it to an another file with (2> e); The number 2 specifies the stream ID that the shell modifies. Stream ID 1 is standard output (the default), and 2 is standard error. 

### Standard Input Redirection
To channel a file to a program's standard input, use the < operator: 
- - -
$ head < /proc/cpuinfo
- - -
You will occasionally run into a program that requires this type of redirection, but because most Unix commands accept filenames as arguments, this isn't very common. For example, the preceding command could have been written as head /proc/cpuinfo

### Understanding Error Messages
When you encounter a problem on a Unix-Like system such as Linux, you must read the error message. Unlike messages from other operating systems, Unix errors usually tell you exactly what went wrong. 
Many errors that you'll encounter in Unix programs result from things that can go wrong with files and processes. Here's an error message hit parade: 
* No such file or directory
* File exists
* Not a directory, Is a directory 
* No space left on device
* Operation not permitted
* Segmentation fault, Bus error : This error essentially means that the person who wrote the program that you just ran screwed up somewhere. The program tried to access a part of memory that it was not allowed to touch.

### Listing and Manipulating Processes
A *process* is a running program, each process on the system han a numeric process ID (PID). To list the running processes, run **ps** on the command line. 
- - -
  PID TTY   STAT    TIME     CMD
30313 pts/4 R 	    00:00:00 ps
31693 pts/4 R       00:00:00 bash
- - -
The fiels are as follows : 
* **PID** : The process ID.
* **TTY** : The terminal device where the process is running. 
* **STAT** : THe process status, that is, what the process is doing and where its memory resides. For example, S means Sleeping and R means running. (See the ps(1) manual page for a description of all the symbols.)
* **TIME** : The amount of CPU time in minutes and seconds that the process has used so far. In other words, the total amount of time that the process has spent running instructions on the processor. 
* **CMD** : "Command" - This one might see obvious, but be aware that a program can change this field from its original value.

**Comand Options** :
1. *ps x* : Show all of your running processes. 
2. *ps ax* : Show all processes on the system, not just the ones you own.
3. *ps u* : Include more detailed information on processes. 
4. *ps w* : Show full command names, not just what fitls on one line.

To check a specific process, add its PID to the argument list of the ps command. For example, to inspect the current shell process, you could use ps u$$, because $$ is a shell variable that evaluates to the current shell's PID. 

### Killing Processes
To terminate a process, send it a *signal* with the **kill** command. A signal is a message to a process from the kernel. When you run kill, you're asking the kernel to send a signal to another process. In most casesn all you need to do is this: 
---
$ kill pid
--- 
There are many types of signals. The default is *TERM*, or terminate. You can send different signals by adding an extra option to *kill*. For example, to freeze a process instead of terminating it, use *Stop* signa: 
---
$ kill -STOP pid
---
A stopped process is still in memory, ready to pick up where it left off. Use the CONT signal to continue running the process again:
---
$ kill -CONT pid
---
Note : Using the CTRL-C to terminate a process that is running in the current terminal is the same as using *kill* to end the process wiht the *INT* (interrupt) signal.
The most brutal way to terminate a process is with the *KILL* signal. Other signals give the process a change to clean up after itself, but *KILL* does not. The operating system terminates the process and forcibly removes it from memory. Use this as a last resort.
You may see other users entering numbers instead of names with *kill*; for example, *kill -9* instead of *kill -KILL*. This is because the kernel uses numbers to denote the different signals.

### Background Processes
Normally, when you run a Unix command from the shell, you don't get the shell prompt back until the program finished executing. However, you can detach a process from the shell and put it in the "background" with the *ampersand* (&); this gives you the prompt back. For example, if you have a large file that you need to decompress with **gunzip**, and you want to do some other stuff while it's running, run a command like this one: 
---
$ gunzip file.gz &
---
The shell should respond by printing the PID of the new background process, and the prompt should return immediately so that you continue working. The process with continue to run after you log out.The dark side of running background processes is that they may excpect to work with the standard input (or worse, read directly from the terminal). If a program tries to read something from the standard input when it's in the background, it can freeze or terminate.

### Files Modes and Permissions
Every Unix file has a set of *permissions* that determine whether you can read, write, or run the file. Running *ls -l* displays the permissions.
The file's mode represents the file's permissions and some extra information. There are four parts to the mode : **Type**: It's the first character of the mode. It can be a dash **(-)** which means it's a **regular** file, nothing special about it. This is by far the most common kind of file. Directories are also common and are indicated by a **(d)**. The rest of a file's mode contains the permissions, which break down into three sets: **user**, **group**, and **other**, in that order.
Each permission set can contain four basic representations:
* **r** : Means that the file is readable
* **w** : Means that the file is writable
* **x** : Means that the file is executable (you can run it as a program)
* **-** : Means nothing.
 
  
