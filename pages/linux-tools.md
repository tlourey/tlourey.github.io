---
title: Linux Tools
description: Linux tools to remember
categories:
    - Tech
type: pages
layout: pages
draft: true
published: true
date: 2025-01-11T16:40:00
lastmod: 2025-03-04T22:57:42.428Z
tags:
    - Linux
    - References
    - Tools
---


<!--- cSpell:disable --->
* [etckeeper](#etckeeper)
  * [etckeeper Commands](#etckeeper-commands)
  * [etckeeper Notes](#etckeeper-notes)
  * [etckeeper References](#etckeeper-references)
* [changetrack](#changetrack)
  * [changetrack Commands and Setup](#changetrack-commands-and-setup)
  * [changetrack References](#changetrack-references)
* [logcheck](#logcheck)
  * [logcheck commands and setup](#logcheck-commands-and-setup)
  * [logcheck notes](#logcheck-notes)
  * [useful logcheck rules](#useful-logcheck-rules)
  * [logcheck references](#logcheck-references)
* [apt-unattended](#apt-unattended)
  * [apt-unattended Commands](#apt-unattended-commands)
  * [apt-unattended Notes](#apt-unattended-notes)
  * [apt-unattended References](#apt-unattended-references)
* [logrotate](#logrotate)
  * [logrotate Commands](#logrotate-commands)
  * [logrotate Notes](#logrotate-notes)
  * [logrotate Tips](#logrotate-tips)
  * [logrotate References](#logrotate-references)
<!--- cSpell:enable --->

## etckeeper

### etckeeper Commands

`sudo apt install etckeeper` or `sudo apt install etckeeper git` to install both etckeeper and git\
`sudo etckeeper init` performs init of etckeeper but this should be done during install\
`sudo etckeeper commit <<INSERT MESSAGE>>` make a commit with messages\
`sudo etckeeper vcs log` show the git log\
`sudo etckeeper vcs log /etc/passwd` show the log for /etc/passwd

### etckeeper Notes

* Repo is in /etc/.git but this is only viewable as root
* It has a nightly autocommit via cron
* It is also run when apt installs packages
* Don't message with the etckeeper git like you would normally. use the etckeeper commands not git commands.

### etckeeper References

<https://ubuntu.com/server/docs/etckeeper>\
<https://documentation.ubuntu.com/server/how-to/backups/install-etckeeper/>\
<https://www.digitalocean.com/community/tutorials/how-to-manage-etc-with-version-control-using-etckeeper-on-centos-7>\
<https://etckeeper.branchable.com/>

## changetrack

### changetrack Commands and Setup

`sudo apt install changetrack`: installs changetrack\
`sudo vi /etc/default/changetrack`: modify changetrack defaults:

* uncomment `CONFFILES_LIST=/var/lib/changetrack/all_conffiles.txt` so it takes affect
* change `AUTO_TRACK_ALL_CONFFILES` to yes

`sudo vi /etc/changetrack.conf`: my suggetestions of changes:\

```bash
/boot/grub/*
/etc/cron*
/etc/aliases
/etc/apt/preferences
/etc/logrotate*
/etc/default/*
/etc/fetchmailrc
/etc/hosts
/etc/lprfilter
/etc/modprobe.d/blacklist
/etc/network/*
/etc/news/leafnode/config
/etc/pam.d/*
/etc/printcap
/etc/ssh/sshd_config
/etc/sudoers
/etc/postfix/*
/etc/ufw/*
/root/.bash*
/root/.profile
/etc/apt/apt.conf.d/
```

### changetrack References

<http://changetrack.sourceforge.net/>\
<https://launchpad.net/ubuntu/+source/changetrack>

## logcheck

### logcheck commands and setup

`sudo apt install logcheck`
`sudo vi /etc/logcheck/logcheck.conf`:

* Adjust `SENDMAILTO=` address to external address or alias
* Change from address for logcheck account in `/etc/passwd` from `logcheck system account` to be something like `logcheck@servername`

`logcheck-test`: used for testing new logcheckrules

### logcheck notes

### useful logcheck rules

* best not to modify the supplied rule files, but rather add your own.

/etc/logcheck/ignore.d.server/local-server:

```bash
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ kernel: \[[0-9]+\.[0-9]+\] IPv4: host .* ignores redirects for .*$
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ kernel: \[[0-9]+\.[0-9]+\] IPv4: martian source .*$
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ kernel: \[[0-9]+\.[0-9]+\] ll header: .*$
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ kernel: \[[0-9]+\.[0-9]+\] .*promiscuo.*$
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ kernel: \[[0-9]+\.[0-9]+\] net_ratelimit.*$
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ kernel: \[[0-9]+\.[0-9]+\] audit:.*.usr.sbin.cron.*$
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ kernel: \[[0-9]+\.[0-9]+\] audit:.*.ntp-systemd-netif.*$
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ kernel: \[[0-9]+\.[0-9]+\] audit: type=110(1|3|5|4|6).*$
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ kernel: \[[0-9]+\.[0-9]+\] audit: type=111(0|2).*$
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ kernel: \[[0-9]+\.[0-9]+\] audit: type=1123.*$
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ kernel: \[[0-9]+\.[0-9]+\] audit: type=113(0|1).*$
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ kernel: \[[0-9]+\.[0-9]+\] audit: type=1006.*$
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ kernel: \[[0-9]+\.[0-9]+\] wan-fw DROP.*$
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ kernel: \[[0-9]+\.[0-9]+\] kauditd_printk_skb.*$
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ kernel: \[[0-9]+\.[0-9]+\] i2c i2c-2:.*$
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ kernel: \[[0-9]+\.[0-9]+\] \[UFW.*$
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ systemd.* Started Cleanup of Temporary Directories..*$
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ systemd.* Starting Cleanup of Temporary Directories....*$
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ systemd.* slice User.*$
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ systemd.* ntopng.service.*$
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ systemd.* Startup finished in.*$
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ systemd.* SIGRTMIN.*$
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ systemd.* Closed GnuPG.*$
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ systemd.* Removed session.*$
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ systemd.* session opened for user tim.*$
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ systemd\[.*$
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ systemd-logind.*$
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ sudo: omsagent.*$
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ auditd.*$
^\w{3} [ :0-9]{11} [._[:alnum:]-]+ sudo.*omsagent.*$
^\w{3} [ :[:digit:]]{11} [._[:alnum:]-]+ ntopng.*$
^\w{3} [ :0-9]{11} [._[:alnum:]-]+ su.*pam_systemd.*Cannot create session.*$
^\w{3} [ :0-9]{11} [._[:alnum:]-]+ systemd\[[0-9]+\]: Reached.*$
^\w{3} [ :0-9]{11} [._[:alnum:]-]+ systemd\[[0-9]+\]: Stop.*$
^\w{3} [ :0-9]{11} [._[:alnum:]-]+ systemd\[[0-9]+\]: Start.*$
^\w{3} [ :0-9]{11} [._[:alnum:]-]+ systemd\[[0-9]+\]: grub-common.*$
^\w{3} [ :0-9]{11} [._[:alnum:]-]+ systemd\[[0-9]+\]: Listening on GnuPG.*$
^\w{3} [ :0-9]{11} [._[:alnum:]-]+ postfix.postfix-script\[[0-9]+\]:.*$
^\w{3} [ :0-9]{11} [._[:alnum:]-]+ postfix.master\[[0-9]+\]:.*$
^\w{3} [ :0-9]{11} [._[:alnum:]-]+ sshd\[[0-9]+\]: Disconnected from user spidey.*$
^\w{3} [ :0-9]{11} [._[:alnum:]-]+ sshd\[[0-9]+\]: Timeout, client not responding.*$
^\w{3} [ :0-9]{11} [._[:alnum:]-]+ sshd\[[0-9]+\]: Did not receive identification string from.*$
^\w{3} [ :0-9]{11} [._[:alnum:]-]+ auditd\[[0-9]+\]: rotating log files with.*$
^\w{3} [ :0-9]{11} [._[:alnum:]-]+ nullmailer.*$
^\w{3} [ :0-9]{11} [._[:alnum:]-]+ CRON.*cron.*$
^\w{3} [ :0-9]{11} [._[:alnum:]-]+ CRON.*logcheck.*$
^\w{3} [ :0-9]{11} [._[:alnum:]-]+ .*motd.*$
^\w{3} [ :0-9]{11} [._[:alnum:]-]+ .*ntp-systemd-netif.*$
^\w{3} [ :0-9]{11} [._[:alnum:]-]+ dbus-daemon.*$
^\w{3} [ :0-9]{11} [._[:alnum:]-]+ PackageKit.*$
^\w{3} [ :0-9]{11} [._[:alnum:]-]+ postfix.*$
^\w{3} [ :0-9]{11} [._[:alnum:]-]+ snapd.*no updates available.*$
^\w{3} [ :0-9]{11} [._[:alnum:]-]+ snapd.*all snaps are up-to-date.*$
^\w{3} [ :0-9]{11} [._[:alnum:]-]+ fwupdmgr\[[0-9]+\]: (Downloading..|Idle..) [ :0-9]{1,3}%
```

Azure autopatching can be noisy, so if used consider this:

/etc/logcheck/ignore.d.server/local-azureautopatch

```bash
\w{3} [ :0-9]{11} [._[:alnum:]-]+ bash\[[0-9]+\]: (Connecting to IMDS endpoint...|Return code from IMDS connection http request: 200\.|Connection to IMDS end point successfully established\. VMCloudType is Azure\.|Completed building bootstrap container configuration\.)
\w{3} [ :0-9]{11} [._[:alnum:]-]+ bash\[[0-9]+\]: ([,`|' -]+)\S+
```

### logcheck references

<https://www.debian.org/doc/manuals/securing-debian-manual/log-alerts.en.html>
<https://www.debian.org/doc/manuals/debian-handbook/sect.supervision.en.html#sect.logcheck>
<https://launchpad.net/ubuntu/+source/logcheck>
<https://packages.debian.org/stable/admin/logcheck>
<https://linux.die.net/man/8/logcheck>
<https://linux.die.net/man/1/logcheck-test>
<https://packages.debian.org/stable/admin/logcheck-database>
<https://www.debian.org/releases/bookworm/amd64/release-notes/ch-information.en.html#rsyslog-timestamp-change-affects-logcheck>

## apt-unattended

### apt-unattended Commands

`sudo apt-get install unattended-upgrades`\
`sudo vi /etc/apt/apt.conf.d/50unattended-upgrades`: Make the following changes:

```python
Unattended-Upgrade::Mail "it-notifications-extra@careflight.org";

Unattended-Upgrade::MailReport "always";

Unattended-Upgrade::Automatic-Reboot "false"; #should be false by default, at least for servers

```

If you want exclude a package for unattended-upgrades.

```python
Unattended-Upgrade::Package-Blacklist {
  "packagename"; // will match anything after packagename
  "packagename$"; // will match packagename ONLY
};
```

Look for Blacklist in `/etc/apt/apt.conf.d/50unattended-upgrades`

Optional: `sudo dpkg-reconfigure --priority=low unattended-upgrades` but I don't normally do this.

### apt-unattended Notes

### apt-unattended References

<https://ubuntu.com/server/docs/package-management>
<https://help.ubuntu.com/community/AutomaticSecurityUpdates#Using_the_.22unattended-upgrades.22_package>
<https://www.cyberciti.biz/faq/set-up-automatic-unattended-updates-for-ubuntu-20-04/>

## logrotate

### logrotate Commands

`/usr/sbin/logrotate /etc/logrotate.conf`: run manually\
`sudo systemctl start logrotate.timer`: run systemd timer manually.

### logrotate Notes

* Used to be run by cron job in /etc/cron.daily but now seems to use systemd timers
* weekly: 0 means Sunday, 1 means Monday, ..., 6 means Saturday; the special value 7 means each 7 days, irrespectively of weekday. Defaults to 0 if the weekday argument is omitted.

### logrotate Tips

For files that are stuck open, you can consider the following directives.

* copytruncate
* If required, use a post-rotate to restart the service

From: <https://serverfault.com/questions/55610/logrotate-and-open-files>

### logrotate References

**<https://man.archlinux.org/man/logrotate.conf.5#CONFIGURATION_FILE_DIRECTIVES>**\
<https://man.archlinux.org/man/logrotate.8>\
<https://github.com/logrotate/logrotate>

<!--
## toolname

### toolname Commands

### toolname Notes

### toolname References

<>
-->
