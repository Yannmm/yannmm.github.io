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


# 5. Working with Commands

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