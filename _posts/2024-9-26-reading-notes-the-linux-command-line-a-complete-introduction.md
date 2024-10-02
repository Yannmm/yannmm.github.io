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