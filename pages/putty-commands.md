---
title: PuTTY Commands
description: description
published: false
categories:
- References
- Commands
type: pages
---

[home](/) [up](./)

* [Latest Download Links](#latest-download-links)
* [Basics](#basics)
* [Port Fowrarding](#port-fowrarding)
* [More Help](#more-help)

## Latest Download Links

<https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html>\
<https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe>\
<https://the.earth.li/~sgtatham/putty/latest/w64/putty.zip>\
<https://the.earth.li/~sgtatham/putty/latest/w64/plink.exe>\
<https://the.earth.li/~sgtatham/putty/latest/w64/pscp.exe>\
<https://the.earth.li/~sgtatham/putty/latest/w64/psftp.exe>\
<https://apps.microsoft.com/store/detail/putty/XPFNZKSKLBP7RJ>

## Basics

putty.exe [-ssh | -ssh-connection | -telnet | -rlogin | -supdup | -raw] [user@]host
<https://the.earth.li/~sgtatham/putty/latest/htmldoc/Chapter3.html#using-cmdline>

## Port Fowrarding

To forward a local port (say 5110) to a remote destination (say popserver.example.com port 110), you can write something like one of these:

`putty -ssh user@host -L 5110:popserver.example.com:110`\
`putty -ssh user@host -L 8080:webserver.example.com:80`\
`putty -ssh user@host -L 8443:192.168.1.1:443`\
`putty -L 5110:popserver.example.com:110 -load mysession`\
`plink mysession -L 5110:popserver.example.com:110`

To forward a remote port to a local destination, just use the -R option instead of -L:

`putty -ssh user@host -R 5023:mytelnetserver.myhouse.org:23`\
`putty -R 5023:mytelnetserver.myhouse.org:23 -load mysession`\
`plink mysession -R 5023:mytelnetserver.myhouse.org:23`

To specify an IP address for the listening end of the tunnel, prepend it to the argument:

`plink -L 127.0.0.5:23:localhost:23 myhost`

To set up SOCKS-based dynamic port forwarding on a local port, use the -D option. For this one you only have to pass the port number:

`putty -D 4096 -load mysession`

## More Help

<https://www.chiark.greenend.org.uk/~sgtatham/putty/>\
<https://the.earth.li/~sgtatham/putty/latest/htmldoc/>\
<https://the.earth.li/~sgtatham/putty/latest/htmldoc/Chapter7.html#plink>
