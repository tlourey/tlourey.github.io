---
title: Bash Tips
description: There are more. much more.
published: true
categories:
- References
- Tips
- Language
type: pages
---

[home](/) [up](./)

* [Bash Scripts](#bash-scripts)
  * [Running as a user](#running-as-a-user)
  * [Misc](#misc)

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

### Misc

* It's good practice to not have the tailing slash on directories. Some tools distinguish between directories with a trailing slash and without
* Use exit codes. It stops error propagating. See `man errno` for standard numbers
* Use stderr for error messages, eg `>&2 echo "ERROR: ..."`
