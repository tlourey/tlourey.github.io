---
title: Nagios Tips
description: Tips and References for Nagios with a little sprinkle of SNMP and OIDs
published: true
categories:
    - Tech
type: pages
layout: pages
date: 2025-01-28T00:56:46.164Z
lastmod: 2025-02-26T13:02:33.000Z
tags:
    - Monitoring
    - Nagios
    - SNMP
    - Tips
    - References
draft: true
fmContentType: pages
---

<!--- cSpell:disable --->
* [Nagios Verify](#nagios-verify)
* [Searching](#searching)
* [HostGroup Excludes](#hostgroup-excludes)
* [Emails with missing hostname](#emails-with-missing-hostname)
* [Nagios References](#nagios-references)
  * [Thresholds](#thresholds)
* [SNMP](#snmp)
  * [Ticks](#ticks)
  * [Uptime oids](#uptime-oids)
  * [Macros](#macros)
* [Vendor Refs](#vendor-refs)
  * [Synology](#synology)
  * [Netgear](#netgear)
  * [APC](#apc)
<!--- cSpell:enable --->

## Nagios Verify

*nagios4 -v config_file: Reads all data in the configuration files and performs a basic verification/sanity check.  Always make sure you verify your config data before (re)starting Nagios.*

In my case I use `sudo /usr/sbin/nagios4 -v ~/my-nagios-repo/nagios-test.cfg`:

* It needs to be sudo so it can access everything Nagios can (one day I may try `sudo -u nagios CMD`)
* nagios-test.cfg is the same as my normal nagios.conf except i've changed: `cfg_dir=./conf.d` so it verifies all the changes in my local repo before I push and then pull in `/etc/nagios4`

More info: [Verifying your Nagios Core configuration](https://assets.nagios.com/downloads/nagioscore/docs/nagioscore/4/en/verifyconfig.html)

## Searching

When searching in vscode, try these:

`name\s*generic`

* This will search for name then ignore any whitespace characters (tabs or spaces) then the next bit of text.
* eg: use\s*generic-switch

## HostGroup Excludes

When applying checks to hostgroups, you can exclude a host.

```nagios
define service {
  use                   generic-service
  hostgroup_name        windows-machines
  #dauphine is excluded from this check as it is not on the domain.
  host_name             !not-this-host
  service_description   SSH
  check_command
}
```

## Emails with missing hostname

If you have an email alert come through, normally for a service but the hostname seems to be missing, check if the alias definition for the host is blank.

Example:

```email
From: nagios@domain
Sent: Sunday, 12 January 2025 7:23 PM
To: nagiosalerts
Subject: ** PROBLEM Service Alert: /Battery Runtime Remaming is WARNING **

***** Nagios *****

Notification Type: PROBLEM

Service: Battery Runtime Remaming
Host:
Address: 192.168.0.10
State: WARNING

Date/Time: Sun Jan 12 19:22:52 AEDT 2025
```

```nagios
define host {
    use                         generic-host
    host_name                   CF-HQUPS3
    alias
    Address                     192.168.0.10
}
```

## Nagios References

[Nagios Plugin Development Guidelines](https://nagios-plugins.org/doc/guidelines.html)

[Nagios Object Definitions](https://assets.nagios.com/downloads/nagioscore/docs/nagioscore/4/en/objectdefinitions.html)\
[Nagios Host Definitions](https://assets.nagios.com/downloads/nagioscore/docs/nagioscore/4/en/objectdefinitions.html#host)\
[Nagios Service Definitions](https://assets.nagios.com/downloads/nagioscore/docs/nagioscore/4/en/objectdefinitions.html#service)\

[Nagios Macro List](https://assets.nagios.com/downloads/nagioscore/docs/nagioscore/4/en/macrolist.html)

<https://nagios-plugins.org/doc/man/check_snmp.html>\
<https://nagios-plugins.org/doc/extra-opts.html>\
<https://nagios-plugins.org/development/>\

<https://www.monitoring-plugins.org/doc/man/index.html>\
<https://www.monitoring-plugins.org/doc/guidelines.html>\
<https://www.monitoring-plugins.org/doc/man/check_http.html>

### Thresholds

<https://www.monitoring-plugins.org/doc/guidelines.html#THRESHOLDFORMAT>

```nagios
# Warning anything between ~ and 35, Critical anything between ~ and 50
!~:35!~:50

# Warning anything between 30~16, critical 15~0
-w 30:16 -c 15:0
!30:16!15:0
```

## SNMP

### Ticks

Sometimes timeticks are used in SNMP. To convert to seconds:
`ticks/100 = seconds`

### Uptime oids

New: HOST-RESOURCES-MIB::hrSystemUptime (1.3.6.1.2.1.25.1.1.0) - returns timeticks - could be snmp agent / nmc time
Old: DISMAN-EVENT-MIB::sysUpTimeInstance (1.3.6.1.2.1.1.3.0) - returns timeticks - could be device time
Newer?: 1.3.6.1.6.3.10.2.1.3.0 [returns seconds](https://mibs.observium.org/mib/SNMP-FRAMEWORK-MIB/#snmpEngineTime)

<https://kb.paessler.com/en/topic/61249-why-does-the-snmp-system-uptime-sensor-report-wrong-values>

### Macros

For the host:

```nagios
_SNMPCOMMUNITY    public
```

For the service or check:

```nagios
$_HOSTSNMPCOMMUNITY$
```

## Vendor Refs

### Synology

MIB Guide: <https://kb.synology.com/en-us/DG/Synology_DiskStation_MIB_Guide/3>\
MIB Guide as PDF: <https://global.download.synology.com/download/Document/Software/DeveloperGuide/Firmware/DSM/All/enu/Synology_DiskStation_MIB_Guide.pdf>\
MIB Download: <https://global.download.synology.com/download/Document/Software/DeveloperGuide/Firmware/DSM/All/enu/Synology_MIB_File.zip>

### Netgear

MIB Download: <https://www.downloads.netgear.com/files/GDC/M4300/M4300v12.0.19.4-mibs.zip>

### APC

<https://www.opsview.com/resources/monitoring/blog/apc-ups-monitoring-useful-oids>\
<https://docs.vistanet.jp/about/supported-resources/templates-in-detail/apc-ups-status-check-g2/>

MIB Guide: <https://download.schneider-electric.com/files?p_Doc_Ref=SPD_ASTE-6Z5QEY_EN&p_enDocType=User+guide&p_File_Name=ASTE-6Z5QEY_R0_EN.pdf>\
MIB Download: <https://www.se.com/au/en/download/document/APC_POWERNETMIB_452_EN/>

APC Support for Generic UPS OID Standard Thing <https://www.apc.com/us/en/faqs/FA156148/?r=65&other.LCC_KnowledgeEditAsDraft.knowledgeEditAsDraft=1/>\
