---
title: Misc Tools
description: And not enough toolboxes
categories:
    - Tech
type: pages
layout: pages
isdraft: false
published: true
tags:
    - Email
    - Linux
    - Microsoft365
    - Networks
    - Python
    - Security
    - Tools
    - Windows
    - Provisioning
fmContentType: pages
date: 2025-01-20T20:00:00
lastmod: 2026-02-08T03:21:35.464Z
keywords:
    - Tools
---

<!--- cSpell:words Hostmaster Hostmasters APNIC WHOIS Vesa microcontrollers circuitpython DNSSEC RDAP ICANN byobu -->
<!--- cSpell:ignore Nirsoft cyrilbois Deview pyrexp Keji mfcmapi MAPI winget NBLGGH -->

<!--- cSpell:disable --->
* [Network Tools](#network-tools)
  * [Speedtest](#speedtest)
* [Linux Tools](#linux-tools)
* [Software Language Tools](#software-language-tools)
  * [Python](#python)
    * [Maker Variants](#maker-variants)
  * [KQL Tools](#kql-tools)
  * [PowerShell Tools](#powershell-tools)
* [Development Tools](#development-tools)
  * [Vagrant](#vagrant)
  * [VSCode](#vscode)
* [Microsoft 365 Tools](#microsoft-365-tools)
* [Outlook and Exchange Tools](#outlook-and-exchange-tools)
* [Windows Tools](#windows-tools)
  * [Windows package manager aka winget](#windows-package-manager-aka-winget)
  * [Hardware](#hardware)
  * [Provisioning and Deployment Tools](#provisioning-and-deployment-tools)
* [Video Cables](#video-cables)
* [Chrome or Edge Extensions](#chrome-or-edge-extensions)
* [Misc Web Tools](#misc-web-tools)
* [Security Tools](#security-tools)
* [Master Tools](#master-tools)
  * [History and Background](#history-and-background)
  * [Webmaster](#webmaster)
    * [Search](#search)
  * [Hostmaster](#hostmaster)
  * [Postmaster](#postmaster)
  * [NOC](#noc)
<!--- cSpell:enable --->

## Network Tools

[Network Calculators](https://subnetmask.info) - now seems to redirect to <https://web.archive.org/web/20240429134052if_/https://subnetmask.info/>\
<https://wq.apnic.net/static/search.html>\
<https://netox.apnic.net/>\
<http://lg.he.net/>\
<https://bgp.he.net/>\
<https://www.ripe.net/>\
<https://www.ausnog.net/tools/lg>\
<https://lg.aussiebroadband.com.au/>\
<https://lists.ausnog.net/pipermail/ausnog/>\
<https://www.internetexchangemap.com/>\
<https://www.peeringdb.com/>\
<http://gfblip.appspot.com/>\
<https://ixpdb.euro-ix.net/en/>\
<https://crt.sh/>\
<https://search.censys.io/>\
<https://dns.google/>\
<https://lookup.icann.org/en>
<http://dns.squish.net/>\
<http://www.webdnstools.com/dnstools/domain_check>\
<https://www.cotse.net/users/initiate/Security.htm>\
<http://www.subnetmask.info/>\
<https://developers.cloudflare.com/dns/reference/recommended-third-party-tools/>\
<https://lists.ausnog.net/pipermail/ausnog/>\
<https://docs.wpvip.com/domains/check-dns-record-time-to-live/#:~:text=Run%20dig%20%40%20%2B,current%20TTL%20for%20the%20domain>\
<https://regauth.standards.ieee.org/standards-ra-web/pub/view.html#registries>\
<https://www.talosintelligence.com/reputation_center/lookup>\
<https://www.appmaildev.com/>

### Speedtest

<https://speedtest.net>\
<https://fast.com>\
<https://speed.cloudflare.com>\
<https://wifiman.com>\
<https://www.ozspeedtest.com>\
<https://www.aussiebroadband.com.au/speed-test/>

## Linux Tools

<https://explainshell.com/> - paste in a shell command and understand what it does\
[Byobu](https://www.byobu.org/) - Open source text-based window manager and terminal multiplexer. Can use tmux or screen underneath. Nicer than native tmux. May not be installed everywhere so consider learning tmux as well.

* [Byobu Help when using TMUX](https://github.com/dustinkirkland/byobu/blob/master/usr/share/doc/byobu/help.tmux.txt)
* [Byobu Help when using screen](https://github.com/dustinkirkland/byobu/blob/master/usr/share/doc/byobu/help.screen.txt)
* [Older Byobu cheat sheet](https://gist.github.com/inhumantsar/bf86ff1961cccdf8be06)

> [!TIP] Keyboard shortcuts to remember
> Exit Scrollback mode:

> * <kbd>ESC</kbd>
> * <kbd>q</kbd>
> * <kbd>Ctrl</kbd> + <kbd>c</kbd>
> * <kbd>ENTER</kbd>

## Software Language Tools

[regex101](https://regex101.com/)\
[pyrexp](https://pythonium.net/regex) - Thanks to [@cyrilbois](https://github.com/cyrilbois) for the PR and making the tool!

### Python

#### Maker Variants

<https://micropython.org/> - lean version of python for microcontrollers, like arduino\
<https://circuitpython.org/> - beginner / easier to user version of the above for microcontrollers\
<https://circuitpython.org/blinka> - use circuitpython on SBCs like the Raspberry Pi

### KQL Tools

<https://www.kqlsearch.com/>

Check out [Misc KQL References and Resources](kql-queries.md#misc-kql-references-and-resources)

### PowerShell Tools

[PowerShell Module Browser](https://learn.microsoft.com/en-us/powershell/module/)

## Development Tools

### Vagrant

**<https://portal.cloud.hashicorp.com/vagrant/discover>** - vagrant boxes search\
<https://www.vagrantup.com/>\
<https://developer.hashicorp.com/vagrant/docs>\
**<https://developer.hashicorp.com/vagrant/docs/cli>**

Common Vagrant Commands:

```bash
mkdir nameforproject
vagrant init ubuntu/jammy64
vagrant up
vagrant snapshot save
vagrant snapshot restore
vagrant halt
vagrant destory
vagrant box list
vagrant box remove box/name
```

### VSCode

[VSCode Settings and Extensions](vscode-settings-and-extensions.md)

## Microsoft 365 Tools

<https://microsoft365dsc.com/>\
<https://aka.ms/m365dscwhitepaper>\
<https://microsoft365dsc.com/resources/overview/>

## Outlook and Exchange Tools

[NK2Edit - Edit AutoComplete files of Microsoft Outlook](https://www.nirsoft.net/utils/outlook_nk2_edit.html)\
[OutlookAttachView - View / Extract / Save Outlook Attachments from command-line or GUI](https://www.nirsoft.net/utils/outlook_attachment.html)\
[MS-Outlook/Office Related software](https://www.nirsoft.net/outlook_office_software.html) - more from the maker of the above (Nirsoft)\
[mfcmapi](https://github.com/microsoft/mfcmapi) - MFCMAPI provides access to MAPI stores to facilitate investigation of Exchange and Outlook issues and to provide developers with a sample for MAPI development. See also [mfcmapi website](https://microsoft.github.io/mfcmapi/)

Also see [Exchange And Outlook Tips](exchange-and-outlook-tips.md#outlook-and-exchange-tools)

## Windows Tools

**<https://learn.microsoft.com/en-us/windows/powertoys/>**\
**<https://cmder.app/>** really good terminal emulator app for windows for all kinds of Windows & Linux shells as well as hooking into other tools like SecureCRT and PuTTY!

* Note to self, remember the [Keyboard Shortcuts](https://cmder.app/#:~:text=(Cmder.exe)-,Keyboard%20shortcuts,-Tab%20manipulation)
* [Cmder wiki](https://github.com/cmderdev/cmder/wiki)
* [Main readme.md](https://github.com/cmderdev/cmder/blob/master/README.md)

<https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html> - see also: [PuTTY Commands](putty-commands.md)\
**<https://learn.microsoft.com/en-us/sysinternals/>** - the whole sysinternals suite is amazing but some of the forgotten ones are\

* [PSPing](https://learn.microsoft.com/en-us/sysinternals/downloads/psping): PsPing implements Ping functionality, TCP ping, latency and bandwidth measurement.
* [ADExplorer](https://learn.microsoft.com/en-us/sysinternals/downloads/adexplorer)
* [ZoomIT](https://learn.microsoft.com/en-us/sysinternals/downloads/zoomit)

**<https://www.vandyke.com/products/securecrt/windows.html> - Its not free but its good.**\
<https://mobaxterm.mobatek.net/> - i'm not a massive fan but it comes in useful with the portable edition, including cygwin, quick port forwarding, and some other niceties.\
[Cygwin](https://www.cygwin.com/) - Linux env for Windows, somewhat natively.\
<https://www.farmanager.com/> - Clone of Norton Commander/Midnight Commander but for windows, still getting updates and has plenty of features
**[Total Commander](https://www.ghisler.com/)** - THE PIMP! One of the best tools you can have if you work in IT or with lots of files, a lot.

* <https://www.ghisler.ch/wiki/index.php?title=Main_Page>: Total Commander Wiki (not sure if official)
* [Useful External Tools for Total Commander](https://www.ghisler.com/tools.htm)
* **[Total Commander plugins](https://www.ghisler.com/plugins.htm)**

  > [!TIP] SFTP
  > Note to self: When you forget, *again*, how to access an SSH Connection via the plugin: Its not in FTP Connections, its in Network Neighbourhood

<https://aka.ms/terminal> / <https://github.com/microsoft/terminal> - i'm not totally on the Windows Terminal Bandwagon yet but its not shit.

### Windows package manager aka winget

[Windows Package Manager](https://learn.microsoft.com/en-us/windows/package-manager/)\
**[Use the WinGet tool to install and manage applications](https://learn.microsoft.com/en-us/windows/package-manager/winget/)** - winget contains commands\
**[Rego with packages](https://github.com/microsoft/winget-pkgs)**

Install using PowerShell: `Add-AppxPackage -RegisterByFamilyName -MainPackage Microsoft.DesktopAppInstaller_8wekyb3d8bbwe`\
Install using MS Store Web Site: <https://apps.microsoft.com/detail/9NBLGGH4NNS1>\
<!--- <!-- markdownlint-disable-next-line MD033-->
<a href="ms-windows-store://pdp/?ProductId=9NBLGGH4NNS1">Open MS Store to app directly</a>

### Hardware

**[USBDeview](https://www.nirsoft.net/utils/usb_devices_view.html)** - really good tool. Shows info about USB device drivers and USB Devices (also nearly everything from Nirsoft is awesome)\
[DevManView](https://www.nirsoft.net/utils/device_manager_view.html) - Alternative to device manager of Windows (have not used it but everything from Nirsoft is awesome)

### Provisioning and Deployment Tools

<https://github.com/CodingWonders/DISMTools>

## Video Cables

Somewhat specific cables I often buy and want to remember.

[Keji 4K HDMI Cable 5m](https://www.officeworks.com.au/shop/officeworks/p/keji-4k-hdmi-cable-5m-kejihdmi5m) - cheapish for 5M\
[StarTech.com 3m 10 ft White Mini DisplayPort to DisplayPort 1.2 Adapter Cable M/M - DisplayPort 4k with HBR2 Support - Mini DP to DP Cable](https://www.amazon.com.au/dp/B0081ZBNCA)\
[Club3D CAC-2067 DisplayPort to DisplayPort 1.4/Hbr3/ HDR Support Cable DP 1.4 8K 60Hz 1 Meter/3.28 Feet Black Vesa Certified](https://www.amazon.com.au/dp/B076D6GGG8)\
Active DisplayPort to HDMI for Lenovo Docks that you prefer: [CableCreation Active DisplayPort to HDMI 4K 60Hz Cable 2.4M(8FT) Support Multi-Screen Display, DP to HDMI HDR Monitor Cable Unidirectional, DP Cable 1.4 to HDMI Support 4K 30Hz, 2K/1080P 144Hz, 120Hz](https://www.amazon.com.au/CableCreation-Unidirectional-DisplayPort-Eyefinity-Multi-Display/dp/B082CXMBCQ?ref_=ast_sto_dp&th=1)

## Chrome or Edge Extensions

* Session Buddy:
  * <https://microsoftedge.microsoft.com/addons/detail/session-buddy/hgpnndpninkidjggjjhfadpmipappndb?hl=en-GB>\
  * <https://chromewebstore.google.com/detail/session-buddy/edacconmaakjimmfgnblocblbcdcpbko>
[Refined Microsoft Learn](https://github.com/merill/refined-microsoft-learn/)
  * <https://microsoftedge.microsoft.com/addons/detail/refined-microsoft-learn/ohjiccikicdhcdlophelgjppakkdlfmg>\
  * <https://chromewebstore.google.com/detail/microsoft-learn-boost/mkacacgjjgafnjekdcoodibajidagopd>
* Context Menu Search:
  * <https://chromewebstore.google.com/detail/context-menu-search/ocpcmghnefmdhljkoiapafejjohldoga>

## Misc Web Tools

<https://caiorss.github.io/bookmarklet-maker/>\
[Network Calculators](https://subnetmask.info) - now seems to redirect to <https://web.archive.org/web/20240429134052if_/https://subnetmask.info/>\
[The Most Accurate Online Ruler](https://www.ginifab.com/feeds/cm_to_inch/actual_size_ruler.html)\
[Actual size of Online Ruler (cm/mm)](https://www.piliapp.com/actual-size/cm-ruler/)\
<https://www.drawio.com/> / <http://draw.io/>\
<https://www.mermaidchart.com/play> - web based mermaid play pen\
<https://www.google.com.au/advanced_search> - also check out [Search Tools in Misc References](misc-references.md#search-tools)

## Security Tools

**<https://crt.sh/>**\
<https://search.censys.io>\
<https://www.talosintelligence.com/reputation_center/>\
<https://www.talosintelligence.com/reputation_center/lookup?search=example.com> - lookup string\
<https://www.ssllabs.com/ssltest/> - does a bit more than just an SSL test but thats it main function

<https://dicepass.org>\
<https://github.com/onetimesecret/onetimesecret> / <https://onetimesecret.com/>\
<https://www.random.org> / <https://www.random.org/passwords/?num=5&len=16&format=html&rnd=new>

## Master Tools

### History and Background

<https://datatracker.ietf.org/doc/html/rfc2142> MAILBOX NAMES FOR COMMON SERVICES, ROLES AND FUNCTIONS

### Webmaster

<https://analytics.google.com>\
[Google Admin Toolbox](https://toolbox.googleapps.com/apps/main/)

#### Search

<https://www.bing.com/webmasters>

<https://search.google.com/search-console>\
<https://www.google.com/webmasters/tools/siteoverview> - older site that may not be relevant any more

### Hostmaster

**<https://www.whatsmydns.net>** - DNS Replication Check\
**<http://dns.squish.net>** - DNS Traversal Check\
**<https://dns.google>**\
<https://developers.cloudflare.com/dns/reference/recommended-third-party-tools/>:

* [DNSViz](https://dnsviz.net/): A web-based tool for visualizing the status of a DNS zone to understand and troubleshoot the deployment of DNS Security Extensions (DNSSEC)
* [Dig Web Interface](https://digwebinterface.com/): An online DNS lookup tool based on the command line interface dig. Users can skip the process of entering commands with complicated parameters in the terminal by entering the same information in this web tool and getting the same results.
* [Mess with DNS](https://messwithdns.net/): An educational resource that encourages users to experiment with DNS records by providing users with a domain where they are free to play around and break things during the learning process.

<http://www.webdnstools.com/dnstools/domain_check>\
<https://lookup.icann.org/en> - RDAP (whois replacement)\
RDAP Client from ICANN: <https://github.com/icann/icann-rdap/wiki/RDAP-command>\
[Google Admin Toolbox](https://toolbox.googleapps.com/apps/main/)\
[Flush Cache | Public DNS | Google for Developers](https://developers.google.com/speed/public-dns/cache) - Request form to flush cache on Google DNS for a particular domain

<https://docs.wpvip.com/domains/check-dns-record-time-to-live/#:~:text=Run%20dig%20%40%20%2B,current%20TTL%20for%20the%20domain.>

### Postmaster

Also often includes abuse functions

**<https://gmail.com/postmaster/>** - if you have a domain you can sign up and should\
<https://senders.yahooinc.com> - if you have a domain you can sign up - not as useful as google postmaster but still good\
<https://blog.postmaster.yahooinc.com>\
<https://sendersupport.olc.protection.outlook.com/pm/Postmaster>\
<https://sendersupport.olc.protection.outlook.com/snds/>\
<https://sendersupport.olc.protection.outlook.com/snds/JMRP.aspx> - Junk email reporting program - works if you host your own email/own the IP Addresses.

**<https://mha.azurewebsites.net>** - Microsoft Message Header Analyzer - really good header analyzer\
<https://toolbox.googleapps.com/apps/messageheader/> - Google Message Header Analyzer\
<https://toolbox.googleapps.com/apps/dig/> - Google Dig (DNS Lookup)\
**<https://mxtoolbox.com>** - really great site with lots of email tools\

* **<https://mxtoolbox.com/SuperTool.aspx>**\
* **<https://mxtoolbox.com/EmailHeaders.aspx>**\
* **<https://mxtoolbox.com/emailhealth>** - good email health overview for a specific domain\
* **<https://mxtoolbox.com/dmarc.aspx>**\
* **<https://mxtoolbox.com/spf.aspx>** - allows you to specify a domain AND an IP Address to see if the SPF record is in it (without manually figuring that out)\

**<https://dmarcian.com/dmarc-tools/>** - there are a bunch of tools here that I recommend\
<https://dmarcly.com/tools/>\
**<https://www.appmaildev.com>** - haven't used much but it seems to be getting better and better\
<https://www.learndmarc.com/> - a very visual DMARC, DKIM and SFP tester, header parser and learning tool.

> [!TIP] TIP
> Links to Exchange and Exchange Online Header Messages are in [Microsoft 365 Tips](microsoft-365-tips.md#exchange-email-header-references)

### NOC

[APNIC WHOIS Search | APNIC](https://wq.apnic.net/static/search.html)\
[APNIC NetOX](https://netox.apnic.net/)

[Looking Glass - Hurricane Electric (AS9639)](http://lg.he.net/)\
[Hurricane Electric BGP Toolkit](https://bgp.he.net/)

<http://whois.ripe.net/>
<https://apps.db.ripe.net/db-web-ui/query>\
[RIPE Network Coordination Centre](https://www.ripe.net)\
[Looking Glasses](https://www.ausnog.net/tools/lg)

**<https://www.peeringdb.com>**\
<https://www.internetexchangemap.com>\
<https://ixpdb.euro-ix.net/en/>

<http://gfblip.appspot.com>

<https://radar.cloudflare.com>
