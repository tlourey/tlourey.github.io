---
title: Misc References
description: Another Doom Pile
published: true
categories:
    - Tech
type: pages
layout: pages
isdraft: false
tags:
    - References
date: 2025-01-18T16:52:00
lastmod: 2026-02-21T21:38:02.263Z
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
  * [Linux Standards](#linux-standards)
  * [Misc Standards](#misc-standards)
* [Linux](#linux)
  * [Debian Manuals](#debian-manuals)
  * [Ubuntu Manuals](#ubuntu-manuals)
* [Microsoft Platforms](#microsoft-platforms)
* [Azure](#azure)
  * [Conventions](#conventions)
* [Networking](#networking)
* [Windows](#windows)
* [Active Directory](#active-directory)
* [Regex and Similar](#regex-and-similar)
* [Search Tools](#search-tools)
  * [Google](#google)
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

### Linux Standards

* [ ] Put POSIX Stuff here\
**<https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard>** - see also

* <https://man7.org/linux/man-pages/man7/file-hierarchy.7.html>
* <https://linux.die.net/man/7/hier>
* <https://www.freedesktop.org/software/systemd/man/latest/file-hierarchy.html>

**<https://ss64.com/>** - amazing command line reference resource for Windows, PowerShell, Mac, Linux and more

### Misc Standards

<https://en.wikipedia.org/wiki/Well-known_URI>\
<https://en.wikipedia.org/wiki/Security.txt> / <https://securitytxt.org/>

## Linux

Crontab: Best website for refining crontab timings: [Crontab.guru - The cron schedule expression generator](https://crontab.guru/) - more in [Linux Commands](linux-commands.md)\
[Arch Linux Wiki](https://wiki.archlinux.org/title/Main_page) - Contains a lot more up to date resources for linux, even for non-arch users. I **don't** use arch by the way :grin:\
[The Linux Documentation Project](https://tldp.org/): Older resource but still has a fair bit of stuff. Doesn't come up as much in Google these days but worth remembering.\
**[nixCraft - Linux Tips, Hacks, Tutorials, And Ideas In Blog](https://www.cyberciti.biz/)**: Vivek Gite and one of the best Linux websites around.\
**[Linux Audit](https://linux-audit.com/)**: I only found this very recently but it looks good.\
**<https://ss64.com/>** - amazing command line reference resource for Windows, PowerShell, Mac, Linux and more

### Debian Manuals

[The Debian Administrators Handbook](https://www.debian.org/doc/manuals/debian-handbook/index.en.html)\
[Debian Reference](https://www.debian.org/doc/manuals/debian-reference/index.en.html)\
[Securing Debian Manual](https://www.debian.org/doc/manuals/securing-debian-manual/index.en.html)\
<https://www.debian.org/doc/>\
[Apt Guide](https://www.debian.org/doc/manuals/apt-guide/index.en.html)

### Ubuntu Manuals

**[Ubuntu Server Documentation](https://documentation.ubuntu.com/server/)**\
[Ubuntu Documentation](https://docs.ubuntu.com/) - slowing replacing the next link over time. Gives a good overview of their products & platforms\
[official Ubuntu Documentation](https://help.ubuntu.com/) - older documentation landing portal\
[Ubuntu Wiki](https://wiki.ubuntu.com/) - community edited, not well maintained.

[The Ubuntu Security Guide](https://ubuntu.com/security/certifications/docs/usg) - free to read but requires ubuntu pro subscription for tooling

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

Also see [StarLink Tips](starlink-tips.md)

[4G Signal Statistics Explained](https://www.netvault.net.au/netmon-4g-signal-statistics-explained/)\
[Guide to Mobile Networks 4G LTE Signal Strength Reference Guide](https://www.telcoantennas.com.au/blog/guide-to-mobile-networks/4g-lte-signal-strength-reference-guide/)

## Windows

<https://support.microsoft.com/en-au/windows/keyboard-shortcuts-in-windows-dcc61a57-8ff0-cffe-9796-cb9706c75eec> - Windows shortcuts. The ones you are normally forgetting are:

* <kbd>Windows key</kbd> + <kbd>A</kbd>: Action Centre
* <kbd>Windows key</kbd> + <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>B</kbd>: Reset graphics driver
* <kbd>CTRL</kbd> + <kbd>Esc</kbd>: Start menu
* <kbd>Left Alt</kbd> + <kbd>Left Shift</kbd> + <kbd>Num Lock</kbd>: Turn on mouse keys

**<https://ss64.com/>** - amazing command line reference resource for Windows, PowerShell, Mac, Linux and more

Also check [Windows Tips](windows-tips.md)

## Active Directory

<https://admx.help/> - good group policy reference - except for all the ads\
<https://adamtheautomator.com/audit-group-membership-changes-active-directory/>\
<https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/plan/appendix-l--events-to-monitor>

## Regex and Similar

* Regex for GUID/UUID that Notepad++ likes: `[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}`. From <https://stackoverflow.com/a/6640851>
* Regexes for specific GUID/UUID Versions: <https://stackoverflow.com/a/38191078>
* Regex for finding codeblocks right after markdown alerts (put into codeblock for formatting):

```regex
> \[!\w+\][^\n]*\n>[^\n]*\n\n\```
```

For Useful Excel Formulas see [Excel Tips](excel-tips.md)\
For very useful Regex Tools see [Software in Misc Tools](misc-tools.md#software-tools)

## Search Tools

### Google

<https://www.google.com.au/advanced_search>

<https://ahrefs.com/blog/google-advanced-search-operators/>\
Refine Google Searches (search terms: )<https://support.google.com/websearch/answer/2466433>\
Google Advanced Search: <https://support.google.com/websearch/answer/35890>

<https://blog.google/products/search/how-were-improving-search-results-when-you-use-quotes/>

From: <https://ahrefs.com/blog/google-advanced-search-operators/>

> Working
>
> |Search operator|What it does|Example|
> |-------|-------|-------|
> |" "|Search for results that mention a word or phrase.|"steve jobs"|
> |OR|Search for results related to X or Y. |jobs OR gates|
> |\||Same as OR:|jobs \| gates|
> |AND|Search for results related to X and Y. |jobs AND gates|
> |-|Search for results that don't mention a word or phrase.|jobs -apple|
> |*|Wildcard matching any word or phrase.|steve * apple|
> |( )|Group multiple searches.|(ipad OR iphone) apple|
> |define:|Search for the definition of a word or phrase. |define:entrepreneur|
> |cache:|Find the most recent cache of a webpage.|cache:apple.com|
> |filetype:|Search for particular types of files (e.g., PDF).|apple filetype:pdf|
> |ext: |Same as filetype:|apple ext:pdf|
> |site:|Search for results from a particular website.|site:apple.com|
> |related:|Search for sites related to a given domain.|related:apple.com|
> |intitle:|Search for pages with a particular word in the title tag.|intitle:apple|
> |allintitle:|Search for pages with multiple words in the title tag. |allintitle:apple iphone|
> |inurl:|Search for pages with a particular word in the URL. |inurl:apple|
> |allinurl:|Search for pages with multiple words in the URL. |allinurl:apple iphone|
> |intext:|Search for pages with a particular word in their content.|intext:apple iphone|
> |allintext:|Search for pages with multiple words in their content.|allintext:apple iphone|
> |weather:|Search for the weather in a location. |weather:san francisco|
> |stocks:|Search for stock information for a ticker.|stocks:aapl|
> |map:|Force Google to show map results.|map:silicon valley|
> |movie:|Search for information about a movie.|movie:steve jobs|
> |in|Convert one unit to another.|$329 in GBP|
> |source:|Search for results from a particular source in Google News.|apple source:the_verge|
> |before:|Search for results from before a particular date.|apple before:2007-06-29|
> |after:|Search for results from after a particular date.|apple after:2007-06-29|
>
> Sidenote. You can also use the _ operator, which acts as a wildcard in Google Autocomplete.
>
>Unreliable:
>
> |Search operator|What it does|Example|
> |---|---|---|
> |\# ..\#|Search within a range of numbers. |iphone case $50..$60|
> |inanchor:|Search for pages with backlinks containing specific anchor text. |inanchor:apple|
> |allinanchor:|Search for pages with backlinks containing multiple words in their anchor text. |allinanchor:apple iphone|
> |AROUND(X)|Search for pages with two words or phrases within X words of one another. |apple AROUND(4) iphone|
> |loc:|Find results from a given area.|loc:"san francisco" apple|
> |location:|Find news from a certain location in Google News.|location:"san francisco" apple|
> |daterange:|Search for results from a particular date range. |daterange:11278-13278|

## People

**<https://merill.net/> / <https://github.com/merill> - Big Azure AD / Entra Guy. Makes a LOT of tools, sites and references that are very useful. Plus a great entra ID newsletter and I think is blog is good too!**\
<https://entra.news/> - the newsletter from the guy above.

<https://www.hanselman.com/> - Scott Hanselman - Vice President at Microsoft, Developer Community\
**<http://www.hanselman.com/tools>** - Scotts Tool List
<https://www.hanselman.com/blog/>

<https://www.jsnover.com/> - Father of PowerShell

<https://devblogs.microsoft.com/oldnewthing/author/oldnewthing> - Raymond Chen - old MS Developer with some good stories\
<https://devblogs.microsoft.com/oldnewthing/>

<https://www.superhouse.tv/>

## Misc Misc Misc

[Formatting Sandbox](https://meta.stackexchange.com/questions/3122/formatting-sandbox/327695#327695)\
[Zytrax info](https://www.zytrax.com/tech/) - very deep stuff on common topics. Had the stuff on SPF macros i've never heard of. Plus has SS7 and 100 other tech topics big ones are DNS and LDAP.\
<https://renenyffenegger.ch/notes/index.html>
