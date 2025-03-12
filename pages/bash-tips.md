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
lastmod: 2025-03-12T02:47:02.469Z
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
  * [Misc](#misc)
* [Aliases](#aliases)
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

### Misc

* It's good practice to not have the tailing slash on directories. Some tools distinguish between directories with a trailing slash and without
* Use exit codes. It stops error propagating. See `man errno` for standard numbers
* Use stderr for error messages, eg `>&2 echo "ERROR: ..."`

## Aliases

See [Linux Commands](linux-commands.md#aliases)
