---
title: Ubiquiti Tips
description: Tips and things to remember with Ubiquiti, UniFi, UISP, EdgeRouter systems
published: false
categories:
- References
- Commands
- Tips
type: pages
---

* [UniFi](#unifi)
  * [Logs](#logs)
  * [Monitoring](#monitoring)

## UniFi

### Logs

If you log to the 'Network Application' and not system, you can find the files in `/var/logs/unifi/remote` on linux machines with a file for each device in the format of `ipaddress_macaddress.log`

### Monitoring

Nagios command to check number of process on UniFi Self hosted. In this case, warn when more than 5 and critical when more than 7 but it also reports when there are 0.

`check_procs -a "-a /usr/lib/unifi/lib/ace.jar -w 5 -c 7"`

<!--
## toolname

### toolname Commands

### toolname Notes

### toolname References

<>
-->
