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
lastmod: 2025-04-23T11:15:08.513Z
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

### Misc

* It's good practice to not have the tailing slash on directories. Some tools distinguish between directories with a trailing slash and without
* Use exit codes. It stops error propagating. See `man errno` for standard numbers
* Use stderr for error messages, eg `>&2 echo "ERROR: ..."`

## Other pages

See [Aliases in Linux Commands](linux-commands.md#aliases)
See [Builtin Bash Commands in Linux Commands](linux-commands.md#built-in-bash-commands)

[Linux Bash Shell Scripting Tutorial Wiki](https://bash.cyberciti.biz/guide/Main_Page)
