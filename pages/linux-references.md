---
title: Linux References
description: This may not be the right place for this.
published: true
categories:
    - Tech
type: pages
layout: pages
date: 2025-03-26T11:43:45.306Z
lastmod: 2025-04-11T02:11:55.807Z
tags:
    - Linux
    - Security
isdraft: true
fmContentType: pages
mermaid: false
preview: ""
---

<!--- cSpell:disable --->
* [Man Page sections](#man-page-sections)
* [Ubuntu and Debian Package Urgency](#ubuntu-and-debian-package-urgency)
  * [Using the urgency value](#using-the-urgency-value)
    * [apt-listchanges](#apt-listchanges)
    * [apt-show-versions](#apt-show-versions)
    * [apt-check](#apt-check)
* [Unattended Upgrade Options](#unattended-upgrade-options)
  * [Block a package](#block-a-package)
  * [SystemD Timers](#systemd-timers)
<!--- cSpell:enable --->

* [ ] Consider placement or naming: This may not be the right place for this. Maybe this page should be Linux Tips or it shoud be put into Linux Tools.

## Man Page sections

1 - Executable programs or shell commands\
2 - System calls (functions provided by the kernel)\
3 - Library calls (functions within program libraries)\
4 - Special files (usually found in /dev)\
5 - File formats and conventions, e.g. /etc/passwd\
6 - Games\
7 - Miscellaneous (including macro packages and conventions), e.g., man(7), groff(7)\
8 - System administration commands (usually only for root)\
9 - Kernel routines [Non-standard]

Web based man pages:

* **<https://linux.die.net/man/>**
* <https://www.man7.org/linux/man-pages/>
* <https://wiki.archlinux.org/title/Man_page>

* <https://manpages.ubuntu.com/>
* <https://manpages.debian.org/>

See also [man pages in Linux Commands](linux-commands.md#man-pages)

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

## Unattended Upgrade Options

<https://documentation.ubuntu.com/server/how-to/software/automatic-updates/>\
<https://documentation.ubuntu.com/server/how-to/software/package-management/#automatic-updates>\
<https://pimylifeup.com/unattended-upgrades-debian-ubuntu/>

`/etc/apt/apt.conf.d/50unattended-upgrades`:

Enable/Disable Updating and Upgrading:

> [!NOTE] Defaults
> Default is for both to be enabled

```python
APT::Periodic::Update-Package-Lists "1";
APT::Periodic::Unattended-Upgrade "1";
```

Reboots:

See <https://documentation.ubuntu.com/server/how-to/software/automatic-updates/#reboots>

Default is false. Change to true if it should autoreboot the server.
If changing to true consider if `Automatic-Reboot-WithUsers` and/or `Unattended-Upgrade::Automatic-Reboot-Time` should be changed.

```python
Unattended-Upgrade::Automatic-Reboot "false";
Unattended-Upgrade::Automatic-Reboot-WithUsers "true";
Unattended-Upgrade::Automatic-Reboot-Time "now";
```

Email Updates:

See <https://documentation.ubuntu.com/server/how-to/software/automatic-updates/#notifications>

```python
Unattended-Upgrade::Mail "it-notifications-extra@careflight.org";
Unattended-Upgrade::MailReport "always";
```

> [!IMPORTANT]
> Just adding another package repository to an Ubuntu system WILL NOT make unattended-upgrades consider it for updates!

To adjust repos: <https://documentation.ubuntu.com/server/how-to/software/automatic-updates/#where-to-pick-updates-from>

### Block a package

<https://documentation.ubuntu.com/server/how-to/software/automatic-updates/#how-to-block-certain-packages>

Uses Python Regex: <https://docs.python.org/3/howto/regex.html>

Exclude Kernel Updates:

```python
Unattended-Upgrade::Package-Blacklist {
      "linux-headers";
      "linux-image";
      "linux-generic";
      "linux-modules";
};
```

OR

```python
Unattended-Upgrade::Package-Blacklist {
      "linux-*";
};
```

Block a package:

```python
Unattended-Upgrade::Package-Blacklist {
      "unifi*";
};
```

### SystemD Timers

> Systemd timer units, `apt-daily.timer` and `apt-daily-upgrade.timer`, trigger these actions at a scheduled time with a random delay. These timers activate services that execute the `/usr/lib/apt/apt.systemd.daily` script.
> However, it may happen that if the server is off at the time the timer unit elapses, the timer may be triggered immediately at the next startup (still subject to the `RandomizedDelaySec` value). As a result, they may often run on system startup and thereby cause immediate activity and prevent other package operations from taking place at that time. For example, if another package has to be installed, it would have to wait until the upgrades are completed.
>
> In many cases this is beneficial, but in some cases it might be counter-productive; examples are administrators with many shut-down machines or VM images that are only started for some quick action, which is delayed or even blocked by the unattended upgrades. To change this behaviour, we can change/override the configuration of both APT's timer units `apt-daily-upgrade.timer` and `apt-daily.timer`. To do so, use systemctl edit `<timer_unit>` and override the *Persistent* attribute setting it to *false*:
>
> ```text
> [Timer]
> Persistent=false
> ```
>
> With this change, the timer will trigger the service only on the next scheduled time. In other words, it won't catch up to the run it missed while the system was off. See the explanation for the *Persistent* option in [systemd.timer](https://manpages.ubuntu.com/manpages/noble/en/man5/systemd.timer.5.html) manpage for more details.
