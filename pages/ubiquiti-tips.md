---
title: Ubiquiti Tips
description: Tips and things to remember with Ubiquiti, UniFi, UISP, EdgeRouter systems
published: true
categories:
    - References
    - Commands
    - Tips
type: pages
layout: pages
draft: true
date: 2025-01-17T11:12:00
lastmod: 2025-01-19T14:19:38.748Z
---


<!--- cSpell:disable --->
* [UniFi](#unifi)
  * [Logs](#logs)
  * [Monitoring](#monitoring)
* [EdgeRouter](#edgerouter)
  * [MAC Address Searching on command line](#mac-address-searching-on-command-line)
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

<!--
## toolname

### toolname Commands

### toolname Notes

### toolname References

<>
-->
