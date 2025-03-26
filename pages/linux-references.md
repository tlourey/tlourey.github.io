---
title: Linux References
description: ""
published: false
categories:
    - Tech
type: pages
layout: pages
date: 2025-03-26T11:43:45.306Z
lastmod: 2025-03-26T11:59:52.184Z
tags:
    - Linux
    - Security
isdraft: true
fmContentType: pages
mermaid: false
preview: ""
---

<!--- cSpell:disable --->
* [Ubuntu and Debian Package Urgency](#ubuntu-and-debian-package-urgency)
<!--- cSpell:enable --->

## Ubuntu and Debian Package Urgency

From <https://www.debian.org/doc/debian-policy/ch-controlfields.html#urgency>:
<!--- <!-- markdownlint-disable-next-line MD033 -->
> This is a description of how important it is to upgrade to this version from previous ones. It consists of a single keyword taking one of the values `low`, `medium`, `high`, `emergency`, or `critical`<sup>12</sup> (not case-sensitive) followed by an optional commentary (separated by a space) which is usually in parentheses. For example:
>
> `Urgency: low (HIGH for users of diversions)`
>
> The value of this field is usually extracted from the `debian/changelog` file - see [Debian changelog: debian/changelog](https://www.debian.org/doc/debian-policy/ch-source.html#s-dpkgchangelog).

From <https://www.debian.org/doc/debian-policy/ch-controlfields.html#id27>:

> [12]
> Other urgency values are supported with configuration changes in the archive software but are not used in Debian. The urgency affects how quickly a package will be considered for inclusion into the `testing` distribution and gives an indication of the importance of any fixes included in the upload. `Emergency` and `critical` are treated as synonymous.

Ubuntu ref: <https://canonical-ubuntu-packaging-guide.readthedocs-hosted.com/en/latest/reference/debian-dir-overview/>
