---
title: Cisco IOS Commands to Remember
description: ""
published: false
categories:
    - Tech
type: pages
layout: pages
date: 2025-09-29T03:01:17.705Z
lastmod: 2025-10-17T00:48:30.871Z
tags:
    - Cisco
    - Commands
isdraft: true
fmContentType: pages
mermaid: false
preview: ""
---
<!--- cSpell:words -->
<!--- cSpell:ignore -->
<!--- cSpell:disable --->
* [Old Classics](#old-classics)
* [Reload in or at](#reload-in-or-at)
* [Version](#version)
* [Hardware and Parts](#hardware-and-parts)
* [Cellular](#cellular)
<!--- cSpell:enable --->

## Old Classics

```cisco
show interfaces summary
sh int sum

show ip interface brief
sh ip int bri

show logging
```

## Reload in or at

<https://www.cisco.com/E-Learning/bulk/public/tac/cim/cib/using_cisco_ios_software/cmdrefs/reload.htm>

`reload [text | in [hh:]mm [text] | at hh:mm [month day | day month] [text] | cancel]`

```cisco
! tell it to reload in 10 minutes
reload in 10

! unless you type in reload cancel it will reload itself in 10 minutes. Don't save unless your sure
reload cancel
```

```cisco
! tell it to reload at 11:30 PM
reload at 23:30
```

## Version

```cisco
show version
show sysinfo
```

```cisco
! show bootflash file system
show bootflash: all

show bootvar

show bootlog
```

## Hardware and Parts

```cisco
show inventory

show hardware

show environment
```

## Cellular

```cisco
show cellular 0/2/0 radio

show cellular 0/2/0 all
```

<!-- cSpell:ignore toolname -->
<!--
## toolname

### toolname Commands

### toolname Notes

### toolname References

<>
-->
