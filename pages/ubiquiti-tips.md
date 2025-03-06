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
lastmod: 2025-03-06T23:42:22.966Z
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
  * [Help Refs](#help-refs)
  * [MAC Address Searching on command line](#mac-address-searching-on-command-line)
  * [EdgeRouter on a stick](#edgerouter-on-a-stick)
* [UISP](#uisp)
  * [Paths](#paths)
  * [Help Refs](#help-refs-1)
  * [UNMS CLI](#unms-cli)
<!--- cSpell:enable --->

## UniFi

### Logs

If you log to the 'Network Application' and not system, you can find the files in `/var/logs/unifi/remote` on linux machines with a file for each device in the format of `ipaddress_macaddress.log`

### Monitoring

Nagios command to check number of process on UniFi Self hosted. In this case, warn when more than 5 and critical when more than 7 but it also reports when there are 0.

`check_procs -a "-a /usr/lib/unifi/lib/ace.jar -w 5 -c 1:7"`

## EdgeRouter

### Help Refs

<https://help.uisp.com/hc/en-us/articles/22591243829911-EdgeRouter-How-to-Update-the-Bootloader>

> [!TIP] Bootloader
> I've noticed that while the new Bootloader image will be put on, it doesn't seem to upgrade itself so its worth checking.

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

## UISP

Used to be called UNMS

### Paths

`/home/unms/data/unms-backups`: UNMS Backups\
`/home/unms/data`: UNMS Data folder\
`/home/unms/data/logs/`: logs folder\
`cat /home/unms/data/control/command-update.log`: update log

### Help Refs

**<https://help.uisp.com/hc/en-us/articles/22591008678039-UISP-First-Time-Setup-Installation>** - also contains `unms-cli` and backup overview.\
<https://help.uisp.com/hc/en-us/sections/22589661169559-UISP-Management-System>\
<https://help.uisp.com/hc/en-us/categories/22589458689175-UISP>\
<https://help.uisp.com/hc/en-us/articles/22590970823959-UISP-How-to-Find-Logs-Report-Bugs>\
<https://help.uisp.com/hc/en-us/articles/22590998733207-UISP-Command-Line-Interface-CLI>\
**<https://help.uisp.com/hc/en-us/articles/22590998718231-UISP-Troubleshooting>**

### UNMS CLI

`sudo /home/unms/app/unms-cli`:

```text
Usage:
  unms-cli [-h] COMMAND [COMMAND_ARGS]

Commands:
  restart
    - Restarts UISP.
  start
    - Starts UISP.
  stop
    - Stops UISP.
  status
    - Check status of UISP.
  ip-whitelist [--show|--clear|--set ADDRESSES]
    - Manage IP addresses that are allowed to access UISP UI.
  version
    - Get installed UISP version.

Troubleshooting commands:
  check-installation
    - Check installation status of UISP Docker images.
  clear-conntrack
    - Clears netflow connections from conntrack table.
  clear-device-backups
    - Use if device backups are using too much disk space.
  disable-two-factor [--username USERNAME]
    - Disable Two-Factor authentication for given user. Prints list of users if the --username argument is omitted.
  factory-reset [--force] [--keep-backups]
    - Clear all configuration and reset UISP to the default post-installation state.
  get-hostname-from-backup [--file BACKUP_FILE]
    - Get hostname of the instance from a UISP backup.
  get-images
    - Print names of Docker images required by the current UISP installation.
  get-metadata-from-backup [--file BACKUP_FILE]
    - Get contents of the metadata file from a UISP backup.
  get-password-reset-link
    - Generate password reset link for given user. Prints list of users if the --username argument is omitted.
  is-configured
    - Check whether UISP is running and configured.
  reduce-device-update-frequency
    - Use if UISP is overwhelmed with device updates and UI is inaccessible. Otherwise change device
      update frequency in UI in 'Settings -> Devices -> Performance -> Device Update Frequency'.
  refresh-certificate
    - Updates Let's Encrypt or custom certificate. Use if certificate expired and UI is inaccessible.
  restore-backup [--file BACKUP_FILE]
    - Restore UISP from the latest backup or from given backup file.
  set-password [--username USERNAME]
    - Reset password for given user. Prints list of users if the --username argument is omitted.
  set-superadmin [--username USERNAME]
    - Change given user to superadmin. Prints list of users if the --username argument is omitted.
  set-workers COUNT
    - Set number of worker processes that are managing device connections. Use this option to better utilize
      multi-core processors.

UISP Console commands:
  get-console-backup [--file BACKUP_FILE] [--output OUTPUT_FILE]
    - Extract UISP Console backup from a UISP backup file.
  restore-console-backup [--file BACKUP_FILE] [--no-stop] [--start-on-failure]
    - Restore backup of UISP and the UISP Console it's running on. Device reboot is needed afterwards.
  restore-console-backup-discard [--no-start]
    - Discard pending UISP Console backup restore.
```
