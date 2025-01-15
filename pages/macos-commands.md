---
title: Mac OS Commands
description: Commands to remember for Mac OS
published: true
categories:
- References
- Commands
- MacOS
type: pages
---

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

Ref: [https://ss64.com/mac/dscacheutil.html]

## References

[https://ss64.com/mac/]
