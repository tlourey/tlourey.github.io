---
title: Misc References
description: Another Doom Pile
published: true
categories:
    - Tech
type: pages
layout: pages
isdraft: true
tags:
    - References
date: 2025-01-18T16:52:00
lastmod: 2025-03-21T06:05:39.857Z
fmContentType: pages
---


<!--- cSpell:disable --->
* [Standards](#standards)
  * [Networks](#networks)
  * [CIDR](#cidr)
    * [VLSM](#vlsm)
  * [CEF](#cef)
  * [SMTP](#smtp)
  * [SNMP](#snmp)
    * [RFC1628 - Generic UPS Management Information Base](#rfc1628---generic-ups-management-information-base)
  * [Markdown](#markdown)
  * [Misc](#misc)
* [Linux](#linux)
  * [Debian Manuals](#debian-manuals)
  * [Ubuntu Manuals](#ubuntu-manuals)
* [Microsoft Platforms](#microsoft-platforms)
* [Azure](#azure)
  * [Conventions](#conventions)
* [Networking](#networking)
* [Windows](#windows)
* [Active Directory](#active-directory)
* [People](#people)
* [Misc Misc Misc](#misc-misc-misc)
<!--- cSpell:enable --->

<!---
* [x] add in ubuntu documentation links
* [x] add in debian manuals
--->

> [!NOTE] NOTE
> Things in **bold** I use **a lot**

## Standards

### Networks

<https://www.iana.org/>\
<https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.txt> - Port Listing in Txt\
**<https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml> - Port Listing in HTML** \
<https://www.iana.org/protocols>

### CIDR

**[CIDR](CIDR.md)**\
<https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing>

#### VLSM

[VLSM Workbook](/assets/pdfs/vlsm-workbook-v2.pdf)

### CEF

[What is CEF?](https://www.microfocus.com/documentation/arcsight/arcsight-smartconnectors-8.3/cef-implementation-standard/Content/CEF/Chapter%201%20What%20is%20CEF.htm)

[Implementing ArcSight Common Event Format(CEF) - Version 26](https://www.microfocus.com/documentation/arcsight/arcsight-smartconnectors-8.4/pdfdoc/cef-implementation-standard/cef-implementation-standard.pdf) - Standards Document

### SMTP

[RFC5321: SMTP](https://datatracker.ietf.org/doc/html/rfc5321/)\
[RFC2142: MAILBOX NAMES FOR COMMON SERVICES, ROLES AND FUNCTIONS](https://datatracker.ietf.org/doc/html/rfc2142)\
[RFC7208: SPF](https://datatracker.ietf.org/doc/html/rfc7208)\
[RFC8601: Message Header Field for Indicating Message Authentication Status](https://datatracker.ietf.org/doc/html/rfc8601)

### SNMP

#### RFC1628 - Generic UPS Management Information Base

<https://datatracker.ietf.org/doc/html/rfc1628>

APC Support: <https://www.apc.com/us/en/faqs/FA156148/?r=65&other.LCC_KnowledgeEditAsisdraft.knowledgeEditAsisdraft=1/>

### Markdown

<https://daringfireball.net/projects/markdown/> - where it started\
<https://spec.commonmark.org/> - the main standard (via <https://commonmark.org>)
<https://markdown.github.io/> - documents various implementations\
<https://github.github.com/gfm/> - the GitHub Flavored Markdown Spec\
<https://en.wikipedia.org/wiki/Markdown>

<https://www.markdownguide.org/getting-started/>\
<https://dillinger.io/>

Refer to [Markdown Tips](./markdown-tips.html)

### Misc

<https://en.wikipedia.org/wiki/Well-known_URI>\
<https://en.wikipedia.org/wiki/Security.txt> / <https://securitytxt.org/>

## Linux

Crontab: Best website for refining crontab timings: [Crontab.guru - The cron schedule expression generator](https://crontab.guru/) - more in [Linux Commands](linux-commands.md)\
[Arch Linux Wiki](https://wiki.archlinux.org/title/Main_page) - Contains a lot more up to date resources for linux, even for non-arch users. I **don't** use arch by the way :grin:

### Debian Manuals

[The Debian Administrators Handbook](https://www.debian.org/doc/manuals/debian-handbook/index.en.html)\
[Debian Reference](https://www.debian.org/doc/manuals/debian-reference/index.en.html)\
[Securing Debian Manual](https://www.debian.org/doc/manuals/securing-debian-manual/index.en.html)\
<https://www.debian.org/doc/>

### Ubuntu Manuals

**[Ubuntu Server Documentation](https://documentation.ubuntu.com/server/)**\
[official Ubuntu Documentation](https://help.ubuntu.com/) - older documentation landing portal\
[Ubuntu Wiki](https://wiki.ubuntu.com/) - community edited, not well maintained.

## Microsoft Platforms

**<https://msportals.io/>** - **The best and most up to date website of all of Microsoft's Portals.** Source: <https://github.com/adamfowlerit/msportals.io>\
<https://cmd.ms/> - I don't use this much but can be useful\
<https://pnp.github.io/> - Microsoft 365 & Power Platform Community - used to be called Patterns and Practices. Make some good tools like PnP Tools for SharePoint/O365 plus a tonne of samples.\
<https://adoption.microsoft.com/en-us/> - we should all use this website more often

## Azure

### Conventions

<https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/resource-naming>\
<https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/resource-abbreviations>\
<https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/resource-name-rules>

## Networking

<https://en.wikipedia.org/wiki/Captive_portal>\
[Use Apple products on enterprise networks](https://support.apple.com/en-au/101555) - covers steps to complete and IP Ranges

[StarLink Help Centre](https://www.starlink.com/au/support)\
[StarLink Enterprise Guide](https://starlink-enterprise-guide.readme.io/)\
[StarLink API Documentation](https://starlink.readme.io/)


## Windows

<https://support.microsoft.com/en-au/windows/keyboard-shortcuts-in-windows-dcc61a57-8ff0-cffe-9796-cb9706c75eec> - Windows shortcuts. The ones you are normally forgetting are:

* <kbd>Windows key</kbd> + <kbd>A</kbd>: Action Centre
* <kbd>Windows key</kbd> + <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>B</kbd>: Reset graphics driver
* <kbd>CTRL</kbd> + <kbd>Esc</kbd>: Start menu
* <kbd>Left Alt</kbd> + <kbd>Left Shift</kbd> + <kbd>Num Lock</kbd>: Turn on mouse keys

Also check [Windows Tips](windows-tips.md)

## Active Directory

<https://admx.help/> - good group policy reference - except for all the ads

## People

<https://merill.net/> / <https://github.com/merill> - Big Azure AD / Entra Guy. Makes a LOT of tools, sites and references that are very useful. Plus a great entra ID newsletter and I think is blog is good too!\
<https://entra.news/> - the newsletter from the guy above.

## Misc Misc Misc

[Formatting Sandbox](https://meta.stackexchange.com/questions/3122/formatting-sandbox/327695#327695)
