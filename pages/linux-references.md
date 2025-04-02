---
title: Linux References
description: This may not be the right place for this.
published: true
categories:
    - Tech
type: pages
layout: pages
date: 2025-03-26T11:43:45.306Z
lastmod: 2025-04-02T22:45:38.932Z
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
  * [Using the urgency value](#using-the-urgency-value)
    * [apt-listchanges](#apt-listchanges)
    * [apt-show-versions](#apt-show-versions)
    * [apt-check](#apt-check)
<!--- cSpell:enable --->

* [ ] Consider placement: This may not be the right place for this. Maybe this page should be Linux Tips or it shoud be put into Linux Tools.

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

**Question: Does the urgency value relate to the ubuntu security notice value?**

* [ ] consider text about urgency / cve matching

### Using the urgency value

* [ ] link in with nagios check_apt critical options and critical regex
* [ ] cover which of the above are included with ubuntu vs being 3rd party

#### apt-listchanges

From <https://askubuntu.com/questions/272215/seeing-apt-get-changelogs-for-to-be-upgraded-packages>

Install: `sudo apt install apt-listchanges`

Run this oneliner:

```bash
(cd $(mktemp -d) && apt download $(apt list -qq --upgradable | cut -f1 -d"/") && apt-listchanges -h --latest=1 *.deb) | grep urgency
```

May need to do some stderr/stdout finagling
Doesn't need sudo

Example result:

```text
WARNING: apt does not have a stable CLI interface. Use with caution in scripts.

WARNING: apt does not have a stable CLI interface. Use with caution in scripts.

linux (5.15.0-135.146) jammy; urgency=medium
tzdata (2025a-0ubuntu0.22.04) jammy; urgency=medium
```

> [!NOTE] Ubuntu LTS 20
> apt-listchanges for Ubuntu LTS 20 does not support `--latest` option. But it does seem to work after a couple of runs since it uses `apt list --upgradable`. YMMV
> You can try this:
>
> ```bash
> (cd $(mktemp -d) && apt download $(apt list -qq --upgradable | cut -f1 -d"/") && apt-listchanges -h *.deb) | grep urgency
> ```

#### apt-show-versions

Install: `sudo apt install apt-show-versions`

```bash
apt-show-versions | grep upgradeable | grep security
# OR
apt-show-versions -u
# OR 
apt-show-versions -u -b | grep security
```

> [!NOTE] security or not?
> I noticed that `apt-show-versions` listed a package as being `-security` when it wasn't using `security` in other tools like `apt list --upgradable` or `apt-check`

From: <https://askubuntu.com/a/556399/443835>

#### apt-check

`/usr/lib/update-notifier/apt-check`

* [ ] cover apt-check - <https://askubuntu.com/questions/441921/why-does-usr-lib-update-notifier-apt-check-not-agree-with-apt-get-upgrade>
