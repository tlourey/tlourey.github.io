---
title: Mac OS Commands
description: Commands to remember for Mac OS
published: true
categories:
    - Tech
type: pages
layout: pages
draft: true
date: 2025-01-11T11:50:00
lastmod: 2025-03-01T13:40:35.507Z
tags:
    - Commands
    - MacOS
    - References
---


<!--- cSpell:disable --->
* [Networking](#networking)
* [Admin](#admin)
* [Hardware](#hardware)
* [Directory Services](#directory-services)
* [References](#references)
<!--- cSpell:enable --->

## Networking

`ifconfig`
`netstat -nr -f inet`: show the routing table (ipv4)

> [!NOTE] netstat
> netstat is a cross platform command existing in Unix, Linux, Mac and Windows but nearly all of them have different options/switches/parameters
`scutil --dns | grep 'nameserver'`: Show the name servers

## Admin

`su <username who has admin rights>`

## Hardware

`sudo powermetrics --samplers smc |grep -i "CPU die temperature"`

## Directory Services

`dscacheutil`

Ref: [https://ss64.com/mac/dscacheutil.html](https://ss64.com/mac/dscacheutil.html)

## References

[https://ss64.com/mac/](https://ss64.com/mac/)\
[Advanced macOS Command-Line Tools](https://saurabhs.org/advanced-macos-commands)
