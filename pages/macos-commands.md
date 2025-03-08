---
title: Mac OS Commands
description: Commands to remember for Mac OS
published: true
categories:
    - Tech
type: pages
layout: pages
isdraft: true
date: 2025-01-11T11:50:00
lastmod: 2025-03-07T12:11:57.133Z
tags:
    - Commands
    - MacOS
    - References
mermaid: false
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

`sudo powermetrics --samplers smc |grep -i "CPU die temperature"`\
`sudo powermetrics --samplers smc |grep -i "GPU die temperature"`\
`sudo powermetrics --samplers smc -i1 -n1`: a single instant sample of SMC sensor readings, including CPU and GPU temprature and fan speed

<https://apple.stackexchange.com/questions/54329/can-i-get-the-cpu-temperature-and-fan-speed-from-the-command-line-in-os-x>

## Directory Services

`dscacheutil`

Ref: [https://ss64.com/mac/dscacheutil.html](https://ss64.com/mac/dscacheutil.html)

## References

[https://ss64.com/mac/](https://ss64.com/mac/)\
[Advanced macOS Command-Line Tools](https://saurabhs.org/advanced-macos-commands)
