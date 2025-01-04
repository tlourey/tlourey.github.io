---
title: Netgear Fully Managed Switch M4300 CLI Reference
description: Commands to remember for Netgear Switches
categories: References Commands
---

[home](/) [up](./)

> [!WARNING] Draft
> This page is **VERY** draft. Use the commands below with caution. Make sure you backup beforehand. Some commands can cause Netgear's to lockup if done incorrectly.

> [!CAUTION] M4300 Only
> These commands are based on M4300's only. Do not use on older models.

Contents:

* [Config/Device Management](#configdevice-management)
* [Firmware Upgrades and Image Management](#firmware-upgrades-and-image-management)
* [Port Commands](#port-commands)
  * [Up, Down, PoE Commands](#up-down-poe-commands)
  * [Counters and Stats](#counters-and-stats)
  * [Cable Status](#cable-status)
  * [Port Security](#port-security)
  * [Interface browsing / searching](#interface-browsing--searching)
  * [MAC Address browsing / searching](#mac-address-browsing--searching)
  * [Bulk Changes](#bulk-changes)
* [Trunk Changes](#trunk-changes)
* [VLAN](#vlan)
* [Routing Changes](#routing-changes)
* [DHCP Info](#dhcp-info)
* [Misc Links](#misc-links)

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
```

Log searching:

```cisco
en 
show logging buffered | include SEARCHTEXT\
```

> [!NOTE] Include Command
> `include` command on Netgear's is <ins>**case sensitive**</ins>.

## Firmware Upgrades and Image Management

> [!NOTE] Upgrade Prep:
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

> [!NOTE]
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

> [!NOTE]
>
> * always do `show running-config interface 1/0/X` of the interface you are going to shut to make sure its not an uplink, downlink, trunk or something special. Also be cautious if its an access point.
> * review the existing description from the show running config step above and **if appropriate** update but make sure you keep some of the initial notes. Description field is limited. try to include a reference number.
> * write memory if you are saving it

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

> [!NOTE]
>
> * always do `show running-config interface 1/0/X` of the interface you are going to shut to make sure it's not a trunk or something special
> * write memory if you are saving it
> * You can also use an interface clearing script which will reconfigure port correctly, but you will still need to use {{no shutdown}}

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
> • Normal. The cable is working correctly.\
> • Open. The cable is disconnected or there is a faulty connector.\
> • Short. There is an electrical short in the cable.\
> • Cable Test Failed. The cable status could not be determined. The cable may in fact be working._
>
> _Cable Length: If this feature is supported by the PHY for the current link speed, the cable length is displayed as a range between the shortest estimated length and the longest estimated length. Note that if the link is down and a cable is attached to a 10/100 Ethernet adapter, then the cable status may display as Open or Short because some Ethernet adapters leave unused wire pairs unterminated or grounded. Unknown is displayed if the cable length could not be determined_

### Port Security

setting up mac address security:

```cisco
en
show running-config interface 1/0/X
configure
interface 1/0/X
port-security
port-security violation shutdown
port-security mac-address 00:02:D1:8D:F8:AC 99
description 'DD/MM/YY-IT-XXXXX-port description-MACLOCKED'
exit
exit
write memory
 ```

> [!NOTE]
>
> * always do `show running-config interface 1/0/X` of the interface you are going to secure its not a trunk or something special
> * write memory if you are saving it

show ports with port-security:

```cisco
show port-security all

show port-security 1/0/4

show port-security static 1/0/4

show port-security dynamic 1/0/4

show port-security violation 1/0/4 
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
> `include` command on Netgear's is <ins>**case sensitive**</ins>.

### MAC Address browsing / searching

mac address on interface:

```cisco
show mac-addr-table interface 1/0/X
```

> [!NOTE]
> `show mac-address-table` is different to `show mac-addr-table`

mac address searching:

```cisco
show mac-addr-table | include AA:BB:CC:00:11:22
```

> [!NOTE] Include Command
> `include` command on Netgear's is <ins>**case sensitive**</ins>.

### Bulk Changes

multiple interface selection:

```cisco
interface 1/0/2,1/0/10-1/0/20,1/0/22
```

## Trunk Changes

show trunks:

```cisco
show interfaces switchport trunk
```

* [ ] Adding and changing vlans on trunks

## VLAN

* [ ] VLAN Notes

## Routing Changes

* [ ] routing change aka failover

## DHCP Info

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

> [!NOTE]
> show dhcp XXXX commands are for making the switch a DHCP Client (mostly)

## Misc Links

[M4300-52G-PoE\+|https://www.netgear.com/support/product/M4300-52G-PoE-Plus%20550W%20PSU.aspx]
[M4300-28G-PoE\+|https://www.netgear.com/support/product/M4300-28G-PoE-Plus%20550W%20PSU.aspx]
[M4100-50G-Poe\+|https://www.netgear.com/support/product/M4100-50G-POEplus%20(GSM7248Pv1h1).aspx]

h2. Useful manuals

[M4300 Intelligent Edge Series Fully Managed Stackable Switches, M4300 Series Switches, M4300-96X Modular Switch, Command Line (CLI) Reference Manual, Software Version or Release 12.0.11 (netgear.com)|https://www.downloads.netgear.com/files/GDC/M4300/M4300-M4300-96X_CLI_EN.pdf]

[M4300 Intelligent Edge Series Fully Managed Stackable Switches Software Version 12.0.8 (netgear.com)|https://www.downloads.netgear.com/files/GDC/M4300/M4300_SWA_EN.pdf]

[M4300 Intelligent Edge Series Fully Managed Stackable Switches, M4300 Series Switches, M4300-96X Modular Switch, User Manual, Software Version or Release 12.0.11 (netgear.com)|https://www.downloads.netgear.com/files/GDC/M4300/M4300_M4300-96X_UM_EN.pdf]
