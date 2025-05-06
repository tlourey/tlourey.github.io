---
title: Bash Tips
description: We're gonna need a bigger boat, I mean tip page
published: true
categories:
    - Tech
type: pages
layout: pages
isdraft: true
date: 2025-01-17T13:05:00
lastmod: 2025-05-06T01:04:22.524Z
tags:
    - Language
    - Linux
    - References
    - Tips
    - MacOS
---


<!--- cSpell:disable --->
* [Bash Scripts](#bash-scripts)
  * [Running as a user](#running-as-a-user)
  * [debugging bash scripts](#debugging-bash-scripts)
  * [If statements](#if-statements)
  * [Misc](#misc)
* [Other pages](#other-pages)
<!--- cSpell:enable --->

## Bash Scripts

### Running as a user

Don't check via UID, check via username

```bash
SPECIALUSERNAME="myusername"
if [ "$(id -un)" != "$SPECIALUSERNAME" ]; then
  echo "Run as special user"
  exit
fi
```

If you really really want to check via UID

```bash
if [ "$EUID" -ne 1 ]; then
  echo "Please run as root, maybe via sudo"
  exit
fi
```

### debugging bash scripts

Based off: <https://unix.stackexchange.com/questions/155551/how-to-debug-a-bash-script>

`bash -x ./script.sh` OR\
add `set -x` in your script to see debug output. You can also use `set` to only debug sections:

```bash
set -x
echo "this is the part of the script I want to debug."
set +x
```

In Bash 4.1 or later you can put the debug output into a separate file by adding the below into your script:

```bash
exec 5> debug_output.txt
BASH_XTRACEFD="5"
```

If you want line numbers add this:

```bash
PS4='$LINENO: '
```

See <https://unix.stackexchange.com/questions/155551/how-to-debug-a-bash-script> for examples of using the logger command in your script.

If you really want better logging in your bash script, you could look into [log4bash](https://github.com/fredpalmer/log4bash)

TLDP Debugging Guide: <https://tldp.org/LDP/Bash-Beginners-Guide/html/sect_02_03.html>

### If statements

Form: <https://www.gnu.org/software/bash/manual/html_node/Bash-Conditional-Expressions.html>

```text
-a file
True if file exists.

-b file
True if file exists and is a block special file.

-c file
True if file exists and is a character special file.

-d file
True if file exists and is a directory.

-e file
True if file exists.

-f file
True if file exists and is a regular file.

-g file
True if file exists and its set-group-id bit is set.

-h file
True if file exists and is a symbolic link.

-k file
True if file exists and its "sticky" bit is set.

-p file
True if file exists and is a named pipe (FIFO).

-r file
True if file exists and is readable.

-s file
True if file exists and has a size greater than zero.

-t fd
True if file descriptor fd is open and refers to a terminal.

-u file
True if file exists and its set-user-id bit is set.

-w file
True if file exists and is writable.

-x file
True if file exists and is executable.

-G file
True if file exists and is owned by the effective group id.

-L file
True if file exists and is a symbolic link.

-N file
True if file exists and has been modified since it was last read.

-O file
True if file exists and is owned by the effective user id.

-S file
True if file exists and is a socket.

file1 -ef file2
True if file1 and file2 refer to the same device and inode numbers.

file1 -nt file2
True if file1 is newer (according to modification date) than file2, or if file1 exists and file2 does not.

file1 -ot file2
True if file1 is older than file2, or if file2 exists and file1 does not.

-o optname
True if the shell option optname is enabled. The list of options appears in the description of the -o option to the set builtin (see The Set Builtin).

-v varname
True if the shell variable varname is set (has been assigned a value).

-R varname
True if the shell variable varname is set and is a name reference.

-z string
True if the length of string is zero.

-n string
string
True if the length of string is non-zero.

string1 == string2
string1 = string2
True if the strings are equal. When used with the [[ command, this performs pattern matching as described above (see Conditional Constructs).

‘=’ should be used with the test command for POSIX conformance.

string1 != string2
True if the strings are not equal.

string1 < string2
True if string1 sorts before string2 lexicographically.

string1 > string2
True if string1 sorts after string2 lexicographically.

arg1 OP arg2
OP is one of ‘-eq’, ‘-ne’, ‘-lt’, ‘-le’, ‘-gt’, or ‘-ge’. These arithmetic binary operators return true if arg1 is equal to, not equal to, less than, less than or equal to, greater than, or greater than or equal to arg2, respectively. Arg1 and arg2 may be positive or negative integers. When used with the [[ command, Arg1 and Arg2 are evaluated as arithmetic expressions (see Shell Arithmetic).
```

### Misc

* It's good practice to not have the tailing slash on directories. Some tools distinguish between directories with a trailing slash and without
* Use exit codes. It stops error propagating. See `man errno` for standard numbers
* Use stderr for error messages, eg `>&2 echo "ERROR: ..."`

## Other pages

See [Aliases in Linux Commands](linux-commands.md#aliases)\
See [Builtin Bash Commands in Linux Commands](linux-commands.md#built-in-bash-commands)\
See Bash Reference Manual in [HTML Book form](https://www.gnu.org/software/bash/manual/html_node/index.html) or [Other forms](https://www.gnu.org/software/bash/manual/)

[Linux Bash Shell Scripting Tutorial Wiki](https://bash.cyberciti.biz/guide/Main_Page)
