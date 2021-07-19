# Bash Glossary

This is a non-exhaustive list of common, helpful bash commands and special characters

## Bash Command Structure

Generally, all bash commands follow the format:

```bash
<executable> <options> <arguments>
```

- `<executable>` is the program that you are running (executing) with the command.
- `<options>` (also known as 'flags') change the way the program works in some way and are usually optional. They are often denoted with a single dash (e.g. `-r`) or double dash (e.g. `--recursive`) with a character/word following it.
- `<arguments>` are provided to the program to give it information, such as a file or string. Most commands take arguments, but not all.

## Special Characters

Some characters in bash have special meanings. Here are some of the most common:

| character | meaning | example |
| --------- | ------- | ------- |
| ` ` | Whitespace is a special character that "tokenises" the command. Essentially, each part (token) of a bash command is defined based on where the spaces are | `echo Hello` – the whitespace in this command tells bash where the executable's name ends and the argument begins. |
| `.` | Represents the current working directory. | `git add .` – stages all files in the working directory for commit |
| `..` | Represents the current parent directory (i.e. the directory that the current working directory is in). | `cd ..` – changes the working directory to the parent directory, essentially allowing you to 'go back' one directory. |
| `*` | Globbing wildcard. On its own, represents all files in the current working directory except hidden files (i.e. files that start with `.`, e.g. `.ssh`). Can be used in expressions to respresent files that fit a pattern. | `cp *.txt my-folder` – copies all files that end in `.txt` in the current directory to the `my-folder` directory.
| `\` | Defines an escape character. | `echo Hello \n World` – prints 'Hello' to one line and 'World' to the next, because `\n` is an escape character representing a newline \
| `$` | Used for both variable (`${variable}`) and command (`$(command)`) substitution. | `PERSON=$(whoami)` – assigns the output of the command `whoami` to the variable `PERSON`. 
| | | `echo ${PERSON}` – prints the value of the `PERSON` variable to the console. |

## Navigation

| command | options | arguments | description |
| ------- | ------- | --------- | ----------- |
| `cd` | | `<file_path>` | `C`hange `D`irectory |
| `pwd` | | | `P`rint `w`orking `d`irectory |
| `ls` | | (optional) `<file_path>` | `L`i`s`ts files in a directory – if no argument is provided, it will list the files in the current working directory |
| | `-l` | (optional) `<file_path>` | Show a detailed list |
| | `-a` | (optional) `<file_path>` | Show all files (files/directories that start with `.` are hidden by default) | 

## Displaying Information

| command | options | arguments | description |
| ------- | ------- | --------- | ----------- |
| `echo` | | `<string>` | Prints a string to the console on the next line |
| `cat` | | `<file_path>` | Prints the contents of a file to the console on the next line |

## Managing Files

### Creating Files

| command | options | arguments | description |
| ------- | ------- | --------- | ----------- |
| `touch` | | `<file_name>` | Creates a new empty file with the name given as an argument |
| `mkdir` | | `<directory_name>` | Creates a new empty directory with the name given as an argument |
| | `-p` | `<directory_name>` | Creates any parent directories specified in `<directory_name>` if they do not exist |

### Moving Files

| command | options | arguments | description |
| ------- | ------- | --------- | ----------- |
| `mv` | | `<source>` `<target>` | `M`o`v`es the file at the `<source>` location to the `<target>` location (also used to rename files) |
| `cp` | | `<source>` `<target>` | `C`o`p`ies the file at the `<source>` location to the `<target>` location |

### Deleting Files

| command | options | arguments | description |
| ------- | ------- | --------- | ----------- |
| `rm` | | `<file_name>` | `R`e`m`oves (deletes) a file |
| | `-r` | `<file_name>` | Delete `recursively` – deletes a directory and all files contained within |
| `rmdir` | | `<directory_name>` | `R`e`m`oves (deletes) a directory |

## SSH

| command | options | arguments | description |
| ------- | ------- | --------- | ----------- |
| `ssh` | | `<user_name>@<host_name>` | Log into a remote machine via SSH. `<user_name>` is the user you are logging in as, `<host_name>` is the location of the machine you're connecting to (typically an IP address). |
| | `-i <private_key_path>` |  `<user_name>@<host_name>` | Specifies the path to the private key. If omitted, it will default to using `~/.ssh/id_rsa`. |
| `ssh-keygen` | | | Generate a new SSH key pair. Leaving each text prompt blank will generate a key pair at `~/.ssh/id_rsa` / `~/.ssh/id_rsa.pub`.

## Users

| command | options | arguments | description |
| ------- | ------- | --------- | ----------- |
| `su` | | `- <user_name>` | `S`witch `u`ser. Typically prefixed with `sudo`. |