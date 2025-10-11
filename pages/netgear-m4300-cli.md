---
title: Netgear Fully Managed Switch M4300 CLI Reference
description: Commands to remember for Netgear Switches
categories:
    - Tech
type: pages
layout: pages
published: true
isdraft: false
date: 2024-11-02T11:39:00
lastmod: 2025-10-11T04:22:12.873Z
tags:
    - Commands
    - Networks
    - References
---

> [!CAUTION] M4300 Only
> These commands are based on M4300's only. Do not use on older models. Use the commands below with caution. Make sure you backup beforehand. Some commands can cause Netgear's to lockup if done incorrectly.

Contents:
<!--- cSpell:disable --->
* [CLI Environment Command Modes and Basic commands](#cli-environment-command-modes-and-basic-commands)
* [Config/Device Management](#configdevice-management)
  * [Non-disruptive Configuration Management feature (CLI only)](#non-disruptive-configuration-management-feature-cli-only)
* [Firmware Upgrades and Image Management](#firmware-upgrades-and-image-management)
* [Port Commands](#port-commands)
  * [Up, Down, PoE Commands](#up-down-poe-commands)
  * [Counters and Stats](#counters-and-stats)
  * [Cable Status](#cable-status)
  * [Port Security](#port-security)
  * [Link Debouncing](#link-debouncing)
  * [Interface browsing / searching](#interface-browsing--searching)
  * [MAC Address browsing / searching](#mac-address-browsing--searching)
  * [Bulk Changes](#bulk-changes)
* [Switching and Routing Commands](#switching-and-routing-commands)
  * [Trunk Changes](#trunk-changes)
  * [VLAN](#vlan)
  * [Static Routing Changes](#static-routing-changes)
* [Stacking](#stacking)
  * [Exec Level](#exec-level)
  * [Stack Level](#stack-level)
* [Services](#services)
  * [DHCP Info](#dhcp-info)
* [Management, Monitoring and Misc](#management-monitoring-and-misc)
  * [Syslog](#syslog)
  * [Port Mirroring](#port-mirroring)
    * [RSPAN VLAN](#rspan-vlan)
  * [Crypto](#crypto)
  * [Settings in Exec mode](#settings-in-exec-mode)
* [References](#references)
  * [Useful manuals](#useful-manuals)
<!--- cSpell:enable --->

## CLI Environment Command Modes and Basic commands

Command Modes:

* User Exec: When you are login
* Privileged Exec aka Enable Level:
  * Type `enable` or just `en` to go to enable level. There may be a password.
  * Type `exit` to go back to ??? level
* Global Configure Level:
  * Type `configure` to go to configure level, must be in enable level to get to configure
  * Type `exit` to go back to enable level
* Interface config:
  * specific interface or range
* vlan config:
  * Type `vlan database` to edit the VLAN Database. Can only be done from enable level, not configure
* stack level:
  * Type: `stack` to go to stack level must be in configure level
  * Type `exit` to exit

More Modes in CLI ref under Table 5: CLI Command Modes (Page 19 - 23)

Help:

* When partially typing a command you can press Tab or press the `?` key and you will see help info

Searching Output of the previous command:

* you can type `|` then use one of the search options to find text in a commands Output
* Search options are:
  * begin: Begin with the line that matches
  * exclude: Exclude lines that matches
  * include: Include lines that matches
  * section: Display portion of lines

## Config/Device Management

Quickly backup config:

```cisco
en
copy nvram:startup-config nvram:backup-config
```

> [!CAUTION] M4300 Only
> Do not use the following commands on any other Netgear switches except **M4300** or switch will reboot

Backup and export:

```cisco
en
ping management-server.local
copy nvram:startup-config nvram:backup-config
copy nvram:backup-config scp://user@management-server.local/home/user/DEVICENAME-YESTERDAYSDATE.txt
copy nvram:running-config nvram:startup-config
copy nvram:startup-config scp://user@management-server.local/home/user/DEVICENAME-TODAYSDATE.txt
```

Backup and export using TFTP if SFTP/SCP fails:

```cisco
en
ping management-server.local
copy nvram:startup-config nvram:backup-config
copy nvram:backup-config tftp://192.168.1.1/DEVICENAME-YESTERDAYSDATE.txt
copy system:running-config nvram:startup-config
copy nvram:startup-config tftp://192.168.1.1/DEVICENAME-TODAYSDATE.txt
```

> [!TIP] TFTP Path
> If using XXX TFTP Package on Ubuntu the default path for TFTP files is: `/var/lib/tftpboot`

Restart:

```cisco
en
reload
```

Log viewing:

```cisco
en
show logging buffered
show logging traplogs
```

Log searching:

```cisco
en
show logging buffered | include SEARCHTEXT\
```

> [!NOTE] Include Command
> `include` command on Netgear's is **case sensitive**.

Viewing configs:

```cisco
show startup-config
show backup-config

show running-config
```

Note that `show running-config` has extra options the others don't:

```cisco
<scriptname>             Script file name for writing active configuration.
all                      Show all the running configuration on the switch.
interface                Display the running config for specified interface on
                         the switch.
```

> [!TIP] show running-config all
> This command can show you the full config including defaults that are not specified in your config file, which can be **very very useful**

### Non-disruptive Configuration Management feature (CLI only)

Will apparently resolve differences rather than sending deltas or a full reload.

```cisco
copy tftp://<<IPADDRESS>>/Filename.txt nvram:script scriptname.scr
reload configuration scriptname.scr
```

## Firmware Upgrades and Image Management

> [!NOTE] Upgrade Prep
>
> 1. You will need to substitute text between << and >> per the instructions inside. eg:
>       1. `<<DEVICENAME>>` is the name of the switch
>       1. `<<YYYYMMDD>>` is for the date with 4 digit year, eg: 20231201 or 20240119
>       1. `<<YYMMDD>>` is date with 2 digit year, normally only needed when there are file name restrictions. eg: 231201, 240119
> 1. You should have pre-read the release notes for the firmware you are upgrading too.

This procedure assumes that :

* the new firmware is already located in on the server in the tftp folder
* that you are familiar with using common CLI's either via serial, telnet or ssh
* that a technical resource is onsite near the switch
* You have reviewed the release notes

While build and minor version upgrades are mostly a BAU activity, you should discuss with Tim about increasing the logging level if there are any concerns.

Firmware Upgrade Preparation Steps:

```cisco
# NB: If Core Switch that does IP routing, consider if Primary Route is a PoE Device and if you may need to change to Telstra for Quicker Service Restoration

# Take extra backups
copy nvram:backup-config scp://user@management-server.local/home/user/<<DEVICENAME>>-BACKUP-<<YYYYMMDD>>.txt
copy nvram:startup-config scp://user@management-server.local/home/user/<<DEVICENAME>>-STARTUP-<<YYYYMMDD>>.txt
copy nvram:startup-config nvram:backup-config
write memory
copy nvram:startup-config scp://user@management-server.local/home/user/<<DEVICENAME>>-<<YYYYMMDD>>.txt


# create a new tech support and download *BEFORE UPGRADE* - note don't use full year eg 2024, just last two digits, eg 24
show tech-support
copy nvram:tech-support scp://user@management-server.local/home/user/<<DEVICENAME>>-TecSupPre-<<YYMMDD>>.txt

# check and note down which image *current active* and which image is *next active*
show bootvar

# copy new firmware to image that is not 'current-active'. Change <<XX>>.<<YY>> to the version and image<<N>> to the one that is not 'current-active'
copy scp://user@management-server.local/var/lib/tftpboot/m4300v12.0.<<XX>>.<<YY>>.stk image<<N>> verify

# follow Updates and Change Management for specific switch if any - refer to change management section on switches wiki page

# use below boot image commands to swap over to new image and reboot
```

boot image commands:

```cisco
# show boot image versions and active image
show bootvar

# boot to a different image (and set as default) - NB: You will only issue one of these commands not both
boot system image2
# OR
boot system image1

# reload after changing boot image (you may be prompted to save and will you be prompted to confirm you are reloading the stack) - *THIS WILL REBOOT SWITCH*
reload
# Optional - *not* normally needed: boot a specific switch unit to image2 in a stack
boot system 2 image2
```

Post reboot commands:

```cisco
# create a new tech support and download *AFTER UPGRADE*
show tech-support
copy nvram:tech-support scp://user@management-server.local/home/user/<<DEVICENAME>>-TecSupPost-<<YYMMDD>>.txt

```
<!-- cSpell:ignore CMDB DCIM -->
> [!TIP] Update Records
> Unless automated, make sure you update the firmware version in your CMDB/DCIM/IPAM/Spreadsheet/Ticket/Asset Management/etc

## Port Commands

### Up, Down, PoE Commands

PoE Info:

```cisco
en
show poe port info 1/0/X
show poe port info all

show poe port configuration 1/0/X
show poe port configuration all
```

poe reset:

```cisco
en
configure
interface 1/0/X
poe reset
exit
exit
```

port status commands:

```cisco
# see port status (enabled / disabled)
show port all
show port 1/0/X

show port status all

show port advertise
```

> [!NOTE] NOTE
> You may be asked to save if you logout. You can ignore this but you will be asked again in the future. for some reason poe reset is considered a change

port shutdown:

```cisco
en
show running-config interface 1/0/X
configure
interface 1/0/X
shutdown
description 'DD/MM/YY-IT-XXXXX-Shutdown reason here'
exit
exit
write memory
```
<!-- markdownlint-disable MD032 -->
> [!NOTE] NOTE
> * always do `show running-config interface 1/0/X` of the interface you are going to shut to make sure its not an uplink, downlink, trunk or something special. Also be cautious if its an access point.
> * review the existing description from the show running config step above and **if appropriate** update but make sure you keep some of the initial notes. Description field is limited. try to include a reference number.
> * write memory if you are saving it
<!-- markdownlint-enable MD032-->

port open/startup :

```cisco
en
show running-config interface 1/0/X
configure
interface 1/0/X
no shutdown
description 'DD/MM/YY-REFNO-port description'
exit
exit
write memory
```
<!-- markdownlint-disable MD032 -->
> [!NOTE] NOTE
> * always do `show running-config interface 1/0/X` of the interface you are going to shut to make sure it's not a trunk or something special
> * write memory if you are saving it
> * You can also use an interface clearing script which will reconfigure port correctly, but you will still need to use `no shutdown`
<!-- markdownlint-enable MD032 -->

### Counters and Stats

Interface Counters:

```cisco
# This will show all counters for all ports, first batch will be in 2nd out
show interface counters

# this will show you counters for one interface without headings. The first line will be the in counters and the second line will be the out counters.
show interface counters | include 1/0/15

# Additional interface stats
show interface 1/0/15
show interface ethernet 1/0/14
```

* [ ] SNMP Counters
* [ ] Clearing Counters

### Cable Status

```cisco
en
cablestatus 1/0/X
```

From the Netgear M4200 and M4300 Series ProSAFE - Managed SwitchesCLI - Command Reference Manual - Software Version 12.0.2 0 - February 2018 (Page 312):

> _Cable Status: One of the following statuses is returned:\
>
> * Normal. The cable is working correctly.\
> * Open. The cable is disconnected or there is a faulty connector.\
> * Short. There is an electrical short in the cable.\
> * Cable Test Failed. The cable status could not be determined. The cable may in fact be working._
>
> _Cable Length: If this feature is supported by the PHY for the current link speed, the cable length is displayed as a range between the shortest estimated length and the longest estimated length. Note that if the link is down and a cable is attached to a 10/100 Ethernet adapter, then the cable status may display as Open or Short because some Ethernet adapters leave unused wire pairs unterminated or grounded. Unknown is displayed if the cable length could not be determined_

### Port Security

setting up mac address security in full:

```cisco
en
show running-config interface 1/0/X
configure
interface 1/0/X
port-security
port-security max-dynamic 0
port-security violation shutdown
port-security mac-address 00:02:D1:8D:F8:AC 99
description 'DD/MM/YY-IT-XXXXX-port description-MACLOCKED'
exit
exit
write memory
 ```

move dynamically learned mac address to static on a port in 1 hit (if port security already enabled on port):

```cisco
en
configure
interface 1/0/X
port-security mac-address move
 ```

An order of events to do it gradually:

1. Enabled Global Port Security: `port-security` (Note all other commands are done at interface level)
2. Enabled Interface Port Security: `port-security` (NOTE THIS WILL CAUSE THE PORT TO BOUNCE)
3. Once mac addresses are know (hours, days, weeks), move dynamically learned macs to static mac list: `port-security mac-address move`
4. Enable port to be shutdown if mac list quantities are reached: `port-security violation shutdown`
5. Set number of Max-dynamic MAC address for the port to be 0: `port-security max-dynamic 0`

> [!NOTE] NOTE
>
> * always do `show running-config interface 1/0/X` of the interface you are going to secure its not a trunk or something special
> * write memory if you are saving it

show ports shutdown due to port-security:

```cisco
show interfaces status err-disabled
```

show ports with port-security:

```cisco
show port-security all

show port-security 1/0/4

show port-security static 1/0/4

show port-security dynamic 1/0/4

show port-security violation 1/0/4
```

Want to move a port???

> [!IMPORTANT] Remove static macs if moving devices
> If you need to move a device to a different port to the same switch you will need to remove the port-security on the old port before the device will work on the new port

### Link Debouncing

```cisco
link debounce time <millisecond>

link debounce time 500

no link debounce time

show interface debounce
```

### Interface browsing / searching

Interface browsing:

```cisco
en
show interfaces status all
```

Interface searching:

```cisco
en
show interfaces status all | include KEYWORDINDESCRITION
```

> [!NOTE] Include Command
> `include` command on Netgear's is **case sensitive**.

### MAC Address browsing / searching

mac address on interface:

```cisco
show mac-addr-table interface 1/0/X
```

> [!NOTE] show mac-address-table command
> `show mac-address-table` is different to `show mac-addr-table`

mac address searching:

```cisco
show mac-addr-table | include AA:BB:CC:00:11:22
```

> [!NOTE] Include Command
> `include` command on Netgear's is **case sensitive**.

### Bulk Changes

multiple interface selection:

```cisco
interface 1/0/2,1/0/10-1/0/20,1/0/22
```

## Switching and Routing Commands

### Trunk Changes

show trunks:

```cisco
show interfaces switchport trunk
```

Modifying allowed vlans on an existing trunk:

```cisco
config
interface 1/0/X
! to add allowed vlans
switchport trunk allowed vlan add 2,3,4

! to remove allowed vlans
switchport trunk allowed vlan remove 3,4

! to set all vlans - NB: THIS CAN BE DISRUPTIVE AND SHOULD NOT BE DONE
switchport trunk allowed vlan 1,2,3,4
```

you can also use `except` & `all`.

### VLAN

* [ ] VLAN Notes

### Static Routing Changes

```cisco
en
ip route 0.0.0.0 0.0.0.0 192.168.1.3 description BackupRouter
no ip route 0.0.0.0 0.0.0.0 192.168.1.2
exit
show ip route
```

## Stacking

### Exec Level

`show switch`: show all switches in the stack and which is management and which is standby\
`show switch 1`: show details about switch 1 in stack\
`show switch detail`: show details about all of them

`show stack-status`: show the stack status from the management switch\
`show stack-status all`: show all the stack status\
`show stack-status 1 clear`: clear the stack status stats from switch 1

`show stack-port`: show stack-port summary\
`show stack-port stack-path all 1`: show all switches stack paths to 1\
`show stack-port stack-path 1 2`: show the stack cabling path from switch 1 to 2 in stack\
`show stack-port diag all`: show stack diag stats

### Stack Level

```cisco
configure
stack
```
<!-- cSpell:ignore movemanagement -->
`initiate failover`: Initiate warm 'restart' to backup unit.\
`movemanagement`: change the active management unit.\
`standby`: assign an active standby.\
`stack-port 1/0/50 stack`: configure 1/0/50 as a stack port.

## Services

### DHCP Info

DHCP Commands:

```cisco
# show DHCP leases & conflicts
show ip dhcp binding
show ip dhcp conflict


# clear dhcp binding
clear ip dhcp binding <<IP ADDRESS TO CLEAR>>

# Show DHCP Pool Config
show ip dhcp pool configuration all
show ip dhcp pool configuration <<NAME>>

# dhcp misc commands
show ip dhcp global configuration
show ip dhcp server statistics
```

> [!NOTE] NOTE
> show dhcp XXXX commands are for making the switch a DHCP Client (mostly)

## Management, Monitoring and Misc

### Syslog

Want to remove a syslog entry one at a time or just change one entries configuration?

```cisco
show logging hosts
! note down the host index number for the one you want to remove. Lets assume its 1 in this case
configure
logging host remove 1
exit
save
```

Don't want to change the configuration but want to change the hostname or ip address only?

```cisco
show logging hosts
configure
logging host reconfigure 1 newhostnamehere
exit
save
```

### Port Mirroring

> [!TIP] Mirror vs capture
> Mirror is for WireShark to another machine. Capture is the switch trying to do it and I think its more for debugging.

`show monitor session`: show list of sessions setup\
`show monitor session 1`: show the details of monitor session 1. There can only be 4 sessions (1-4)\
`no monitor`: remove all monitor configs setup\
Source Interface Command: `monitor session session-id source {interface {unit/slot/port | cpu | lag} | vlan vlan-id | remote vlan vlan-id} [rx | tx]` - eg:

* `monitor session 1 source interface 1/0/10`
* `monitor session 1 source vlan 10 rx`

Destination Interface Command: `monitor session session-id destination {interface {unit/slot/port} | remote vlan vlan-id reflector-port unit/slot/port)` - eg:

* `monitor session 1 destination interface 1/0/1`

#### RSPAN VLAN

TBC

### Crypto

If you want to use SSH and/or HTTPS you may need to run the crypto setup. This happens on the switch but isn't in the config file.

for ssh you just need keys, but for HTTPS (ip http secure-server) you need a certificate. If you are not able to use a proper one use a self signed one per instructions below.

```cisco
configure
! for SSH we need keys
crypto key generate dsa
! system will not look like its responding for a couple of seconds to a minute
crypto key generate rsa
! system will not look like its responding for a couple of seconds to a minute
!
! if we want HTTPS we need to generate a self signed certificate
crypto certificate generate
!
exit
exit
```

### Settings in Exec mode

There are some settings that don't get changed in configure mode, but instead get changed in exec mode. Here are some i'm aware of (but there are more):

* hostname
* vlan database
* ip http port 49151
* ip http secure-server
* ip http secure-port 49152
* ip ssh server enable
* sshcon timeout 30
* no ip telnet server enable

> [!TIP] New default ports
> AV UI Default HTTP Port is: 80\
> AV UI Default HTTPS Port is: 443\
> Main/Full UI default HTTP Port is: 49151\
> Main/Full UI default HTTPS Port is: 49152


## References

[M4300-52G-PoE\+](https://www.netgear.com/support/product/M4300-52G-PoE-Plus%20550W%20PSU.aspx)
[M4300-28G-PoE\+](https://www.netgear.com/support/product/M4300-28G-PoE-Plus%20550W%20PSU.aspx)
[M4100-50G-Poe\+](https://www.netgear.com/support/product/M4100-50G-POEplus%20(GSM7248Pv1h1).aspx)

### Useful manuals

<!-- cSpell:ignore Stackable -->

[M4300 Intelligent Edge Series Fully Managed Stackable Switches, M4300 Series Switches, M4300-96X Modular Switch, Command Line (CLI) Reference Manual, Software Version or Release 12.0.11 (netgear.com)](https://www.downloads.netgear.com/files/GDC/M4300/M4300-M4300-96X_CLI_EN.pdf)

[M4300 Intelligent Edge Series Fully Managed Stackable Switches Software Version 12.0.8 (netgear.com)](https://www.downloads.netgear.com/files/GDC/M4300/M4300_SWA_EN.pdf)

[M4300 Intelligent Edge Series Fully Managed Stackable Switches, M4300 Series Switches, M4300-96X Modular Switch, User Manual, Software Version or Release 12.0.11 (netgear.com)](https://www.downloads.netgear.com/files/GDC/M4300/M4300_M4300-96X_UM_EN.pdf)
