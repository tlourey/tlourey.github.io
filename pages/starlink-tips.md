---
title: Starlink Tips
description: Tips and Tricks for Starlink and its networking
published: true
categories:
    - Tech
type: pages
layout: pages
date: 2025-03-24T11:47:32.173Z
lastmod: 2025-06-16T07:24:46.915Z
tags:
    - Internet
    - References
    - Tips
    - Networks
isdraft: true
fmContentType: pages
mermaid: false
preview: ""
keywords:
    - Internet
    - Starlink
    - Tips
    - Network
---

<!--- cSpell:disable --->
* [Dishy access via web or app when using a 3rd party router](#dishy-access-via-web-or-app-when-using-a-3rd-party-router)
  * [Static Route](#static-route)
  * [Dishy Access over Network](#dishy-access-over-network)
* [Dishy Status](#dishy-status)
* [Stowing Dishy](#stowing-dishy)
  * [Issues with stowing](#issues-with-stowing)
* [Hardware](#hardware)
* [Firmware Updates](#firmware-updates)
* [Misc Articles](#misc-articles)
* [Starlink References](#starlink-references)
<!--- cSpell:enable --->

## Dishy access via web or app when using a 3rd party router

**[How do I use the Starlink app with my third-party router?](https://www.starlink.com/au/support/article/27802782-944e-10aa-bc29-23ccbc1fce73)**\
<https://starlink-enterprise-guide.readme.io/docs/using-a-3rd-party-router>

### Static Route

Based off **[How do I use the Starlink app with my third-party router?](https://www.starlink.com/au/support/article/27802782-944e-10aa-bc29-23ccbc1fce73)**

1. Ensure your router can support a static route on the wan side
2. Create a static route on the wan interface:

   * Network destination: 192.168.100.0
   * Subnet Mask: 255.255.255.0
   * Gateway: 192.168.100.1
   * Interface: WAN

[Can I add a third-party router or mesh system?](https://www.starlink.com/au/support/article/a206a55c-0597-2d06-1408-dea7dcf24221)\
[What is bypass mode?](https://www.starlink.com/au/support/article/a0fe8d51-32f7-d2b9-d74a-801e31ad9f6a)

### Dishy Access over Network

1. Go to <http://dishy.starlink.com> in edge - if that fails go to <http://192.168.100.1>. Note HTTP not HTTPS

## Dishy Status

[Booting](https://support.starlink.com/?topic=718b444d-e8c2-eeee-c214-beecc96e44ae) - Starting up. keep waiting\
[Searching](https://support.starlink.com/?topic=8dd04f1b-f7b3-882c-3827-a660c5fe48c7) - Looking for satellites\
[Disconnected](https://support.starlink.com/?topic=8c2013d8-844d-75bc-ed2b-2d696a5834ed) - Not connected\
[Poor Cable Connection](https://support.starlink.com/?topic=f24683ea-add0-916b-ee11-841ae00e2701)\
Online - Connected

## Stowing Dishy

1. Go to <http://dishy.starlink.com/settings>
2. Select Stow (you may have to scroll down)
3. Press OK

### Issues with stowing

When packing up, if you run into issues 'stowing' dishy (putting it back into position for packing away). You can try the following:

1. Close the web browser and try the steps above 'Pack up' again
2. Manually trigger automatic stowing
   1. Leaving Dishy plugged in to at least power, remove dishy from its base
   2. Place dishy upside down on a flat clean surface that won't scratch or damage dishy
   3. After a period of time (either 1 minute or 10 minutes) dishy should automatically stow itself
   4. Turn the power off
3. Don't stow dishy
   1. Turn the power off
   2. Pack Dishy separately, safely in the unstowed position

More Info: [How do I stow my Starlink?](https://www.starlink.com/au/support/article/76c3666b-97ae-6ae3-e629-143910488d90)

## Hardware

[What Starlink Kit do I have?](https://www.starlink.com/au/support/article/61d2f65f-85b8-a5b2-9bad-b3c2f27379d6)\
[What is the difference in visibility between High Performance and Standard?](https://www.starlink.com/au/support/article/8d01f43e-1074-1373-2a06-d00454668b42)\
[Specifications](https://www.starlink.com/specifications)\
[Power Usage](https://www.starlink.com/au/support/article/18836c7e-2d97-6153-fe67-c18427bd0558)\
[Which Starlink router do I have?](https://www.starlink.com/au/support/article/5a09acb1-ac3c-69ed-6cbb-67510cfbf8ce)

## Firmware Updates

[How do I update my Starlink if it doesn't automatically update?](https://www.starlink.com/au/support/article/44b964f6-a538-d7c1-b893-b02822f444b5)

* Firmware Updates are usually installed between 1 AM and 4 AM in the timezone where the device is located by GPS.
* It is commonly 3:00 AM +/- 30 minutes <https://starlink-enterprise-guide.readme.io/docs/software-updates>

## Misc Articles

[What ports does Starlink block?](https://www.starlink.com/au/support/article/c3caacdf-1c1f-98db-b821-bbb36ca9d89b) - ports blocked over the Internet\
[Does Starlink provide time synchronization or NTP servers?](https://www.starlink.com/au/support/article/0873e885-831a-9f4e-4808-2838a28f2e69)\
[What is a Starlink identifier?](https://www.starlink.com/au/support/article/2802431a-135f-0671-4c1b-4cedb65b291a)

[More detailed technical specs](https://starlink-enterprise-guide.readme.io/docs/technical-specs)

## Starlink References

[StarLink Help Centre](https://www.starlink.com/au/support)\
[StarLink Enterprise Guide](https://starlink-enterprise-guide.readme.io/)\
[StarLink API Documentation](https://starlink.readme.io/)\
[StarLink POPs](https://www.peeringdb.com/net/18747)\
[StarLink Public IP Ranges](public-ip-ranges.md#starlink)
