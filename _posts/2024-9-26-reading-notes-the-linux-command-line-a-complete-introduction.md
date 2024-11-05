---
layout: post
title: "Reading Notes: The Linux Command Line: A Complete Introduction"
tags: shell
---

### 1. What Is Shell

`Shell`, aka `Command line`, is a program that takes keyboard strokes and passes them to the operating system to carry out.

### 2. File System

Files are organized in a tree-like pattern of directories.

**Commands**

- pwd (Current Working Directory)
- cd (Change Directory)
  - `cd -`: go back to previous working directory.
- ls (List Directory Contents)

**ls Long Format**

| -rw-r--r-- | 1 | yannmm | staff | 2397 | Jul 25 19:59 | Dockerfile |
| -------- | ------- | ------- | ------- | ------- | ------- | ------- |
| Access rights to the file | File's number of hard links | File owner | User group | Size in bytes | Date and time of last modification | File name |


**Pathnames**
- absolute: starting with `/`.
- relative: to current working directory.
  - `.`
  - `..`


### 3. Exploring the System

**Commands**

- `ls`
  - `-l`
  - `-t`: sort by file's modification time.
  - `-A`: list almost all hidden files.
- `file`: determine file type.
- `less`: view file contents.
  - `g`: to beginning
  - `G`: to end
  - `/characters`: search

Commands are
often followed by one or more options that modify their behavior, and further, by one or more arguments, the items upon which the command acts.

```
command -options arguments
```


### 4. Manipulating Files and Directories

- `cp`: copy
  - cp item1 item2
  - cp item... directory
  - `r`: required when copying directories
- `mv`: move or rename
  - mv item1 item2
  - mv item... directory
- `mkdir`: create dir
  - mkdir dir...
- `rm`: remove
  - `r`: required when deleting a directory
- `ln`: create links
  - ln file link
  - hard links: additional name(s) for same data part on disk (inode).
  - ln -s item link
  - symbolic links: text pointer to target file.
  - most file operations are carried out on the link's target, not the link itself. `rm` is an exception.

**Wildcards**

| Wildcard | Meaning |
| -------- | ------- |
| * | Matches any characters |
| ? | Matches any single character |
| [characters] | Matches any character that is a member of the set characters |
| [!characters] | Matches any character that is not a member of the set characters |
| [[:class:]] | Matches any character that is a member of the specified
class |

| Character Class | Meaning |
| -------- | ------- |
| [:alnum:] | Matches any alphanumeric character |
| [:alpha:] | Matches any alphabetic character |
| [:digit:] | Matches any numeral |
| [:lower:] | Matches any lowercase letter |
| [:upper:] | Matches any uppercase letter |


### 5. Working with Commands

**Commands**

- `type`: display command type.
- `which`: display executable's location.
- `man`: display manual page.
  - man ${section} ${search_term}
- `whatis`: brief description of a command.
- `alias`
  - alias ${name}='string'
  - use `unalias` command to remove.

**Shell Command Type**

1. An executable program.
2. A shell built-in command.
3. A shell function.
4. An alias.

**Help Notation**

Square brackets indicates optional items; vertical bar indicates mutually exclusive items.

```
cd [-L|[-P[-e]]] [dir]
```

This notation says that the command cd may be followed optionally by either a “-L” or a “-P” and further, if the “-P” option is specified the “-e” option may also be included followed by the optional argument “dir”.


**Man Page Organization**
1. User commands
2. Programming interfaces kernal system calls
3. Programming interfaces to the C library
4. Special files such as device nodes and drivers
5. File formats
6. Grames and amusements such as screen savers
7. Miscellaneous
8. System administration commands


`bash` doc in `/usr/share/doc/bash/`.


Put more than one command on a line by separating each command with a semicolon character.

```
command1; command2; command3...
```

### 6. I/O Redirection

**Commands**

- `cat`: concatenate and print files.
- `sort`
- `uniq`: report or filter out repeated lines in a file.
- `grep`: print lines matching a pattern.
  - `i`: ignore case
  - `v`: print lines that do not match the pattern.
- `wc`: word, line, character, and byte countq
  - lines, words, bytes count
- `head`: display the first 10 lines of a file.
- `tail`: display the last 10 lines of a file.
  - `tail -f /var/log/system.log` to view the system logs.
  - `log stream` will show a unified log on MacOS.
  - `n`: specify numbers, default is 10.
  - `f`: don't stop when EOF is reached, but wait for additional data.
- `tee`: duplicate standard input
  - ls /usr/bin | tee ls.txt | grep zip


To redirect standard output:

- `>`: overwrite a file.
  - ls /usr/bin > output.txt
- `>>`: append to the end of a file.
  - ls /usr/bin >> output.txt


To redirect standard error:
- `2>`:
  - ls /usr/bin 2> output.txt
- `2>>`:

To redirect both standard output and error to the same file:

- `&>`
- `&>>`
  - ls -l /bin/usr &>> ls-output.txt

To supress error messages from a comand:

- `/dev/null`
  - ls -l /bin/usr 2> /dev/null

In the absence of filename arguments, cat copies standard input to standard output. To create a short text file:

```
cat > some_file.txt
This is the content of text file.(Ctrl-d, Ctrl-c)
```

**Pipelines**

The standard output of one command can be `piped` into the standard input of another:

```
command1 | command2
```

- command1 `>` file: redirection operator connets a command with a file.
- command1 `|` command2: pipeline operator connects t he output of one command with the input of a second command.



(`l` seems a shortcut to `ls -lh`)


### 7. Seeing the World as the Shell Sees It

**Commands**

- `echo`: write arguments to the standard output

**Expansion**

Use `echo` to print expanded argument(s).

```
echo *
echo D*
echo [[:upper:]]*
echo /usr/*/share
```

- `~` (tilde exapnsion): expands to home directory.
  - `~tom`: tom's home directory

- `$((expression))`: arithmetic expansion
  - echo $((2 + 2))

- `{list or range}` (brace expansion):
  - Number_{1..5}
  - {01..015}
  - a{A{1,2},B{3,4}}b
  - `mkdir -p playground/dir-{001..100}`: create 100 directories
  - `touch playground/dir-{001..100}/file-{A..Z}`: create 26 files under each directory

- `$PARAMETER`: parameter expansion

- `$(command)`: command substitution
  - ls -l $(which cp)

**Quoting**

- double quotes: supress part of expansions.
unify a string with spaces and newlines into a single argument.
  - echo "$(cal)"

- single quotes: supress all expansions.

- use `\` to escape special meaning characters, this is done in double quotes.


### 8. Advanced Keyboard Tricks

**Commands**

- clear
- history

**Cursor Movement Commands**

- `Ctrl-a`: to the beginning of line.
- `Ctrl-e`: to the end of line.
- `Ctrl-l`: clear the screen, same as `clear` command.
- `Alt-f`: move forward one word.
- `Alt-b`: move backward one word.

**Modifying Text**

- `Ctrl-d`: delete the character at the cursor location.

**Cut & Paste**

- `Ctrl-u`: kill the whole line.
- `Ctrl-k`: kill text from the cursor location to the end of line.
- `Ctrl-y`: yank text from the kill-ring and insert it at the cursor location.

**History**

- `history`: whole search
  - `!number`: repeat list item number.

- `ctrl-r`: incremental search

- `script`: makes a typescript of everything printed on your terminal.


### 9. Permissions


- `id`: show user identity.
- `chmod`: change permissions of a file or directory (owner or superuser).
  - octal: `chmod 600 foo.txt`
  - symbolic: `chmod u=rw,go-rwx`
- `umask`: remove default permissions.
- `sudo`: execute a command as another user.
  - `/etc/sudoers` file defines specific commands that particular users are permitted to execute.
  - `sudo -l`: view privileges granted by sudo.
- `chown`: change file owner / group (superuser previleges required).
- `passwd`: change password.
  - `passwd [user]`

**Owner, Group And Everybody Else**

A user may own files and directories. Users can belong to a group who are given access to files and directories by their owners. Owner may also grant some set of access rights to everybody else.

- `/etc/passwd`: where users defined.
- `/etc/group`: where groupds defined.
- `/etc/shadow`: where users' password defined.

**Read, Write and Execution Access**

```
-rw-rw-r-- 1 me me 0 2008-03-06 14:52 foo.txt
```

First 10 characters of above string is the `file attribute`.

The first one is file type:

- `-`: regular file.
- `d`: directory.
- `l`: symbolic link.
- `c`: character special file, like terminal.
- `b`: block special file, like a hard drive.

Rest of them is `file mode`, representing the read, write and execute permissions for file's owner, group and everybody else.

| Owner | Group | World |
| -------- | ------- | ------- |
| rwx | rwx | rwx |


Permission Attributes:

| Attribute | Files | Directories |
| -------- | ------- | ------- |
| r | open and
read. | list contents (x) |
| w | write and truncate, but cannot be
renamed or deleted. | files within can be created, deleted, and
renamed (x) |
| x | treated as a
program and execute. for program
files written in scripting
languages (r) | enter into |
| s (replace x) | setuid | setgid |
| t | _ | sticky bit |

### 10. Processes

Processes are how Linux organizes the different programs waiting for their turn at the CPU.

- `ps`:
  - `ps x`: shoow all of our processes regardless of any terminal they are controlled by.
- `top`: real-time sorted information about processes.
- `jobs`:
- `bg`:
- `fg`:
- `kill`: terminate or signal a process.
  - kill [-signal] PID...
  - If not signal is specified on the commandline, then `TERM` (Terminate) signal is sent by default.
  - `kill -INT 13061` = `kill -2 13061`
- `killall`: kill processes by name
  - killall [-u user] [-signal] name
- `shutdown`:


Processes have:

- PID
- memory assigned
- owner
- user ids
- effective user ids

**Process States**

| State | Meaning |
| -------- | ------- |
| R | Running |
| S | Sleeping |
| s | Session leader |
| D | Uninterruptible Sleep |
| T | Stopped |
| Z | A defunct or “zombie” process. |
| < | A high priority process. |
| N | A low priority process. |

For `ps aux`, we have below column headers:

| Header | Meaning |
| -------- | ------- |
| USER | User ID. This is the owner of the process. |
| %CPU | CPU usage in percent. |
| %MEM | Memory usage in percent. |
| VSZ | Virtual memory size. |
| RSS | Resident Set Size. The amount of physical memory (RAM) the
process is using in kilobytes. |
| START | Time when the process started. For values over 24 hours, a date is
used. |


**Common Process Actions**

- `Ctrl-c`: interrupt a process. (politely asked the program to terminate.)
  - `INT`: Interrupt signal.

- Put in background: `command &`
  - `[1] 91594`: job No.1, PID 91594
  - `jobs`: list the jobs that have been launched.

- Return to foreground: `fg %jobspec`
  - If there is only 1 job, jobspec is optional.

- Pause a process: `Ctrl-z`
  - `fg %jobspec` or `bg %jobspec` a program to make it continue.
  - `TSTP`: Terminal Stop signal.


  **Common Signals**

Processes, like files, have owners. You must be the owner of a process (or the superuser) in order to send it signals with `kill` or `killall`.

| Number | Name | Meaning |
| -------- | ------- | ------- |
| 1 | HUP | Hangup |
| 3 | QUIT | Quit |
| 2 | INT | Interrupt |
| 9 | KILL | Kill |
| 11 | SEGV | Segmentation Violation |
| 15 | TERM | Terminate. This is the default signal sent by the
kill command. |
| 18 | CONT | Continue |
| 19 | STOP | Stop |
| 20 | TSTP | Terminal Stop |
| 28 | WINCH | Window Change |


### 11. The Environment

- `printenv`: show environment variables.
  - `printenv USER` = `echo $USER`
- `set`: set environment, shell variables and shell functions.
- `export`: export environment to subsequently executed programs.
- `alias`: show all or create an alias for a command.
- `source`: force bash to re-read `~/.bashrc` file, since it's only read at the beginning of a session.

There are  `shell variables` (bits of data placed there by bash) and `environment variables` (everything else).


**Some Interesting Variables**

| Variable | Contents |
| -------- | ------- |
| SHELL | The name of your shell program. |
| HOME | The pathname of your home directory. |
| PAGER | The name of the program to be used for paging output. This is often
set to /usr/bin/less. |
| PATH | A colon-separated list of directories that are searched when you
enter the name of a executable program. |
| PWD | The current working directory. |
| USER | Your username. |
| TERM | The name of your terminal type. |


**How Envrionment Is Established**

When we log on to the system, the bash program starts, and reads a series of configuration scripts called startup files, which define the default environment shared by all users.

For `login shell`:
- /etc/profile
- ~/.bash_profile, ~/.bash_login or ~/.profile

For `non-login shell`:
- ~/.bashrc


The `PATH` variable is often set by the `/etc/profile` startup file and with this code:

`PATH=$PATH:$HOME/bin`

which means adding the directory $HOME/bin to the end of the list.

`export PATH` means making the contents of PATH available to child
processes of this shell.


**Text Editor**

`vim file_name`: If the file does not already exist, the editor will assume that you want to create a new file.


### 12. A Gentle Introduction to VI

- `:q`: exit
- `:q!`: force to exit.


- `command mode`
- `insert mode` - i
  - `Esc` to exit


| Key | Cursor Movement in Command Mode |
| -------- | ------- |
| l | right |
| h | left |
| j | down |
| k | up |
| J | join current line with the one below it. |
| 0 | To the beginning of the current line. |
| o | open a new line below the current line and switch to insert mode |
| O | open a new line above the current line and switch to insert mode |
| A | Move the cursor to the end of the current line and switch to insert mode. |
| ^ | To the first non-whitespace character on the current
line. |
| $ | To the end of the current line. |
| w | To the beginning of the next word or punctuation
character. |
| b | To the beginning of the previous word or punctuation
character. |
| Ctrl-f | down one page |
| Ctrl-b | up one page |
| G | To the last line of the file. |
| numberG | To line number. For example, 1G moves to the first
line of the file. |
| u | undo last change. |
| x | delete one character. |
| d+movement | cut specifiied range. |
| y+movement | copy specifiied range. |
| p | paste after the cursor. |
| P | paste before. |
| f | search for a character within a line. (; to repeat) |
| / | search within entire file. (n to repeat) |
| : | starts an ex command |
| :n / N | change file when multiple files are opended |
| :buffers | view a list of files being edited. |
| :r file_name | insert whole file into current position. |
| ZZ | save current file and exit |


**Global Serach-And-Replace**

for `:%s/Line/line/g`:

| Item | Meaning |
| -------- | ------- |
| : | starts an ex command |
| % | Specifies the range of lines for the operation. % is a shortcut
meaning from the first line to the last line. |
| s | Specifies the operation. In this case, substitution (search-and-
replace). |
| g | global. If
omitted, only the first instance of the search string on each line
is replaced. |

with user confirmation, `:%s/line/Line/gc`:

| Key | Action |
| -------- | ------- |
| y | Perform the substitution. |
| n | Skip this instance of the pattern. |
| a | Perform the substitution on this and all subsequent instances
of the pattern. |
| q | Quit substituting. |
| l | Perform this substitution and then quit. |
| Ctrl-e, Ctrl-y | Scroll down and scroll up, respectively. Useful for viewing the context of the proposed substitution. |


### 13. Customizing the Prompt

Skip this chapter since it's not applicable to MacOS.

### 14. Package Management

Skip this chapter since it's not applicable to MacOS.

### 15. Storage Media

- `mount`: attach a stroage device to the file system tree.
- `umount`: Unmounting a device entails writing all the remaining data to the device so that it can be safely removed.
- `fsck`
- `fdisk`
- `mkfs`
- `fdformat`
- `dd`
- `genisoimage`
- `wodim`
- `md5sum`


A file named `/etc/fstab` lists the devices (typically hard disk partitions) that are to be mounted at boot time.

**Fields**

| Sequence | Field | Description |
| -------- | ------- | ------- |
| 1 | Device | device or partition to mount, you can use UUID, LABEL or Path to specify. |
| 2 | Mount Point | The directory where the device is attached to the file system tree. Must be created first. |
| 3 | File System Type | such as hfs, apfs, ntfs, ext4. |
| 4 | Options | Mount options, often a comma-separated list. |
| 5 | Dump | This field is used for backup utilities. It’s usually set to 0 for macOS, meaning no backups by the dump command. |
| 6 | Pass | Determines the order in which filesystems are checked during boot by fsck. |


Use `mount` without any arguments to view a list of devices.

The format is: `device` on `mount_point` type `file_system_type` (`options`).



**Stop as Determining Device Names** since it's not quite relevant to MacOS.

TBD


### 16. Networking

- `ping`: send ICMP ECHO_REQUEST packets to network hosts.
- `traceroute`: print the route packets take to network host.
- `netstat`: show network status.
- `ftp`: can be replaced by `curl`
- `wget`: can be replaced by `curl`
- `ssh`: remote shell login.
  - an encrypted tunnel is created between the local and remote systems.
  - I can note down more ssh-related articles here in the future...


`netstat -r`: show the kernel's network routing table:

| Column | Description | Description |
| -------- | ------- | ------- |
| Destination | destination address for a route. | can be an IP address, hostname or a special designation. |
| Gateway | next-hop address for the route. | The next-hop address for the route, indicating the IP address of the next device (typically a router) that data should be sent to on its way to the destination. |
| Flags | Flags describe the characteristics of each route. | U: The route is “up” and currently active. G: The route uses a gateway. |
| Netif | The name of the network interface used to reach the destination, such as en0 (Ethernet), en1 (Wi-Fi), or lo0 (loopback interface). |  |
| Expire | For routes with time-limited entries (e.g., routes that will expire after a certain time), this shows the expiration time. If there is no expiration, this field might be blank. | |


### 17. Searching for Files.

- `locate`: find filenames quickly via a database called `/var/db/locate.database`.
  - it has `tests` and `actions`.
- `find`: recursively descends the directory tree of a file hierarchy, euvaluating an expression, which composed of the "primaries" and "operators" in terms of each file in the tree.
  - `test` and `operator` order matters.
  - By changing the trailing semicolon character to a plus sign, we activate the ability of find to combine the results of the search into an argument list for a single execution of the desired command.
  - 
- `xargs`: build and execute command lines from standard input.
  - `find . -type f | xargs ls -la`
- `touch`: change file access and modification times
- `stat`: display file status


file types for `find`.

| File Type | Description |
| -------- | ------- |
| b | block device |
| c | character device |
| d | directory |
| f | regualar files |
| l | symbolic link |

`find ~ -type f -name "*.JPG" -size +1M`: find all the regular files that match the wildcard pattern “*.JPG” and are larger than one
megabyte.


operators for `find`:

| Operator | Description |
| -------- | ------- |
| -and | both sides of the operator are true. |
| -or | either side of the operator is true. |
| -not | following is false |
| () | to group |

eg: `find . (-type f -and -not -perm 0600) - or (-type d -not -perm 0700)`

predefined actions for `find`:

| Action | Description |
| -------- | ------- |
| -delete | delete matching file. |
| -ls | Perform the equivalent of `ls -dils` on the matching file |
| -print | print, the default action |
| -quit | Quit once a match has been made. |

user-defined action for `find`:

- `-exec comand {} ;`
- `-ok comand {} ;`, will prompt user before going on.

`find . -type f -exec ls -l '{}' ';'`