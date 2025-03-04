---
title: Ubiquiti Tips
description: Tips and things to remember with Ubiquiti, UniFi, UISP, EdgeRouter systems
published: true
categories:
  - Tech
type: pages
layout: pages
isdraft: true
date: 2025-01-17T11:12:00
lastmod: 2025-03-04T11:22:33.544Z
tags:
  - Commands
  - References
  - Tips
  - Ubiquiti
---


<!--- cSpell:disable --->
* [UniFi](#unifi)
  * [Logs](#logs)
  * [Monitoring](#monitoring)
* [EdgeRouter](#edgerouter)
  * [MAC Address Searching on command line](#mac-address-searching-on-command-line)
  * [EdgeRouter on a stick](#edgerouter-on-a-stick)
<!--- cSpell:enable --->

## UniFi

### Logs

If you log to the 'Network Application' and not system, you can find the files in `/var/logs/unifi/remote` on linux machines with a file for each device in the format of `ipaddress_macaddress.log`

### Monitoring

Nagios command to check number of process on UniFi Self hosted. In this case, warn when more than 5 and critical when more than 7 but it also reports when there are 0.

`check_procs -a "-a /usr/lib/unifi/lib/ace.jar -w 5 -c 1:7"`

## EdgeRouter

### MAC Address Searching on command line

`sudo arp -n | grep -i ab:cd:ef:12:34:56`

### EdgeRouter on a stick

[Hardware Offloading](https://help.ui.com/hc/en-us/articles/115006567467-EdgeRouter-Hardware-Offloading)\
[Archiving and Managing the Configuration Files](https://help.ui.com/hc/en-us/articles/204960084)\
[Backup and Restore Configuration](https://help.ui.com/hc/en-us/articles/360002535514)\
[Configuration and Operational Mode](https://help.ui.com/hc/en-us/articles/204960094-EdgeRouter-Configuration-and-Operational-Mode)\
[VLAN-Aware Switch](https://help.ui.com/hc/en-us/articles/115012700967)\
[How to Create a Guest/LAN Firewall Rule](https://help.ui.com/hc/en-us/articles/218889067)\
[Router on a Stick](https://help.ui.com/hc/en-us/articles/204959444-EdgeRouter-Router-on-a-Stick)\
[Hardware Offloading](https://help.ui.com/hc/en-us/articles/115006567467-EdgeRouter-Hardware-Offloading)\
[Packets Process (aka order of operations)](https://help.ui.com/hc/en-us/articles/204976664-EdgeRouter-Packets-Processing)
