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
lastmod: 2025-03-21T06:55:45.641Z
tags:
    - Commands
    - References
    - Tips
    - Ubiquiti
keywords:
    - EdgeRouter
    - Ubiquiti
    - Unifi
    - UNMS
    - UISP
---

<!--- cSpell:words UniFi macaddress UISP UNMS --->
<!--- cSpell:ignore procs WiFiman lcire1 RSSI --->
<!--- cSpell:disable --->
* [UniFi](#unifi)
  * [Software Logs](#software-logs)
  * [Device Logs](#device-logs)
  * [Searching AP Log files](#searching-ap-log-files)
  * [Monitoring](#monitoring)
  * [Control Commands](#control-commands)
  * [Code Names](#code-names)
  * [Odd Issues](#odd-issues)
    * [AP/Client Signal Balance: Poor](#apclient-signal-balance-poor)
* [EdgeRouter](#edgerouter)
  * [Strange issues when uploading firmware](#strange-issues-when-uploading-firmware)
  * [MAC Address Searching on command line](#mac-address-searching-on-command-line)
  * [EdgeRouter Help Refs](#edgerouter-help-refs)
* [UISP](#uisp)
  * [When restoring to another device](#when-restoring-to-another-device)
  * [Paths](#paths)
  * [Help Refs](#help-refs)
  * [UNMS CLI](#unms-cli)
* [WiFiman](#wifiman)
<!--- cSpell:enable --->

## UniFi

### Software Logs

`/usr/lib/unifi/logs/server.log`
`/usr/lib/unifi/logs/mongod.log`

> [!NOTE] SymLink
> `/usr/lib/unifi/logs/` is a symlink pointing to /var/log/unifi on ubuntu (and maybe others)

If your application is running on a Unix/Linux based system, then you will require superuser (sudo) privileges to access these log files.

### Device Logs

If you have your devices log to the 'Network Application' and not syslog, you can find the files in `/var/logs/unifi/remote` on ubuntu linux machines with a file for each device in the format of `ipaddress_macaddress.log` where ipaddress is the IP Address of the access point / UniFi device.

If you are having trouble accessing that folder you may need to use `sudo` or `sudo -s`

### Searching AP Log files

`cat 192.168.1.2_abcdef123456.log | grep 2025-03-19 | grep 12:34:56:ab:cd:ef`: search a UniFi AP log file for a mac address on a specific date

Other commands for searching logs and compressed files in [Linux Commands](linux-commands.md)

### Monitoring

Nagios command to check number of process on UniFi Self hosted. In this case, warn when more than 5 and critical when more than 7 but it also reports when there are 0.

`check_procs -a "-a /usr/lib/unifi/lib/ace.jar -w 5 -c 1:7"`

### Control Commands

To stop the UniFi service: `sudo service unifi stop`
To restart the UniFi service: `sudo service unifi restart`
To see the status of UniFi service: `sudo service unifi status`

From <https://help.ui.com/hc/en-us/articles/220066768-Updating-and-Installing-Self-Hosted-UniFi-Network-Servers-Linux>

### Code Names

Copied from <https://help.ui.com/hc/en-us/articles/220066768-Updating-and-Installing-Self-Hosted-UniFi-Network-Servers-Linux> at <ins>21/03/25</ins>.

> [!IMPORTANT] Old
While it may be helpful I think the table below on the above link is out of date.

Note: We strongly recommend staying with the stable release.\
"Testing" refers to the next generation release, which is not released to the general public yet. "Stable" refers to the current stable release, which is supported by Ubiquiti and described in this article. "Old Stable" is the previous stable release, which has been replaced by the new stable release.

|Suite Name|Code Name|Archived Code Names|
|-|-|-|
|oldstable|unifi-5.10|These code names have been archived and are no longer supported|
|stable|unifi-5.11|These code names have been archived and are no longer supported|
|testing|*| unifi3, unifi4, unifi-5.3, unifi-5.4, unifi-5.5, unifi-5.6, unifi-5.7, unifi-5.8, unifi-5.9|

*testing is empty at the moment

### Odd Issues

#### AP/Client Signal Balance: Poor

Answer 1: <https://community.ui.com/questions/AP-Client-Signal-Balance-Poor/921859fe-98eb-4677-a385-0e657030fed6#answer/7bf03596-b7d8-47ea-8997-df06bcc541ab>\
More details: <https://community.ui.com/questions/AP-Client-Signal-Balance-Poor/921859fe-98eb-4677-a385-0e657030fed6#answer/1483eb78-2c5f-4ead-9e8e-b90ddce534a1>\
Full post: <https://community.ui.com/questions/AP-Client-Signal-Balance-Poor/921859fe-98eb-4677-a385-0e657030fed6>

Post is more detailed and better written but very briefly summarised:

* Reduce Output Power of Aps that are near each other
* Use WiFiman app on phone to see exactly what APs
* Increase Channel width (more so for 5Ghz than 2.5Ghz)
* Consider Minimum RSSI on some APs for 2.5 or 5Ghz (will force clients with lower signals to disconnect)
* Run Optimise
* Read the post especially those by user 'lcire1'

## EdgeRouter

### Strange issues when uploading firmware

Getting this when uploading a config: "There was an error upgrading the configuration" or similar?

Something like this: [Restore Config - Upload failed](https://community.ui.com/questions/Restore-Config-Upload-failed/29cab3a5-4220-4d29-a398-e0c624b10260)

1. Try a different browser (not safari - either firefox or chrome.)
2. Try turning off dark mode in browser and/or OS
3. Try clearing cache

If all else fails you can look into [uploading a config using SSH/SFTP](https://help.uisp.com/hc/en-us/articles/22591188157079-EdgeRouter-Archiving-and-Managing-the-Configuration-Files)

### MAC Address Searching on command line

`sudo arp -n | grep -i ab:cd:ef:12:34:56`

### EdgeRouter Help Refs

[Hardware Offloading](https://help.ui.com/hc/en-us/articles/115006567467-EdgeRouter-Hardware-Offloading)\
[Archiving and Managing the Configuration Files](https://help.ui.com/hc/en-us/articles/204960084)\
[Backup and Restore Configuration](https://help.ui.com/hc/en-us/articles/360002535514)\
[Configuration and Operational Mode](https://help.ui.com/hc/en-us/articles/204960094-EdgeRouter-Configuration-and-Operational-Mode)\
[VLAN-Aware Switch](https://help.ui.com/hc/en-us/articles/115012700967)\
[How to Create a Guest/LAN Firewall Rule](https://help.ui.com/hc/en-us/articles/218889067)\
[Router on a Stick](https://help.ui.com/hc/en-us/articles/204959444-EdgeRouter-Router-on-a-Stick)\
[Hardware Offloading](https://help.ui.com/hc/en-us/articles/115006567467-EdgeRouter-Hardware-Offloading)\
[Packets Process (aka order of operations)](https://help.ui.com/hc/en-us/articles/204976664-EdgeRouter-Packets-Processing)\
If all else fails you can look into [uploading a config using SSH/SFTP](https://help.uisp.com/hc/en-us/articles/22591188157079-EdgeRouter-Archiving-and-Managing-the-Configuration-Files)\
[How to Update the Bootloader](https://help.uisp.com/hc/en-us/articles/22591243829911-EdgeRouter-How-to-Update-the-Bootloader)

> [!TIP] Bootloader
> I've noticed that while the new Bootloader image will be put on, it doesn't seem to upgrade itself so its worth checking.

## UISP

Used to be called UNMS

### When restoring to another device

If you download a backup from UISP you have to select if you are restoring it do different hardware or not.

[Backup and Restore using UNMS](https://help.uisp.com/hc/en-us/articles/22591243898519-EdgeRouter-Backup-and-Restore-Configuration#3)

Also, when you restore it you may have to adopt the replacement device in UISP

<https://help.uisp.com/hc/en-us/articles/22590956342295-UISP-Add-Devices-to-UISP-Application>

### Paths

`/home/unms/data/unms-backups`: UNMS Backups\
`/home/unms/data`: UNMS Data folder\
`/home/unms/data/logs/`: logs folder\
`cat /home/unms/data/control/command-update.log`: update log

### Help Refs

**<https://help.uisp.com/hc/en-us/articles/22591008678039-UISP-First-Time-Setup-Installation>** - also contains `unms-cli` and backup overview.\
<https://help.uisp.com/hc/en-us/sections/22589661169559-UISP-Management-System> - UISP Console help page\
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

## WiFiman

Its not *that* great a speed test but it does give good network details, port scan and AP details.

Web Browser Version: <https://wifiman.com>\
Desktop Clients (Windows, Mac, Linux): <https://ui.com/download/app/wifiman-desktop>\
WiFiman App for iOS: <https://itunes.apple.com/AU/app/id1385561119>
WiFiman App for Android: <https://play.google.com/store/apps/details?id=com.ubnt.usurvey&hl=AU>

UISP is supposed to have some integration with wifiman but I can't find any info about it.
