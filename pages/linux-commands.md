---
title: Linux Commands
description: Linux commands to remember
categories:
    - References
    - Commands
    - Linux
type: pages
layout: pages
published: true
fmContenttype: pages
date: 2024-12-13T15:22:00
lastmod: 2025-01-19T13:36:43.151Z
---

[home](/) [up](./)
<!--- cSpell:disable --->
* [Terminal Stuff](#terminal-stuff)
* [Files](#files)
* [Hardware Info](#hardware-info)
* [Storage](#storage)
  * [MDADM](#mdadm)
* [Log files](#log-files)
* [Cron](#cron)
* [Accounts and Groups](#accounts-and-groups)
* [Main SystemD Commands](#main-systemd-commands)
  * [Important Commands](#important-commands)
    * [systemctl](#systemctl)
    * [journalctl](#journalctl)
    * [timedatectl](#timedatectl)
    * [resolvectl](#resolvectl)
  * [Misc SystemD Commands](#misc-systemd-commands)
  * [SystemD Links](#systemd-links)
* [Network Commands](#network-commands)
  * [Network Reference](#network-reference)
* [OpenSSL Commands](#openssl-commands)
  * [OpenSSL Links](#openssl-links)
* [Misc System Commands](#misc-system-commands)
<!--- cSpell:enable --->

## Terminal Stuff

```bash
watch
less
wc
```

## Files

What process is using a file:

```bash
fuser /var/log/syslog
# Will come back with a process id
ps aux | grep <Process ID from above>
```

Finding large directories and large files:

```bash
cd /
sudo du --max-depth=1 -h | sort -h

ls -lahS

# if too many files, pipe to more or less
ls -lahS | more
ls -lahS | less

ls -lah 192.168.1.10*
ls -lahS 192.168.1.10*

#If you have one large log file and want to see what day had more log entries try:
#Linux - Search (grep) for number of lines in log file per day
```

## Hardware Info

```bash
lshw
lshw | less
lshw --short
lscpu
lsusb
lspci
lsblk
hwinfo # may not always be installed
hwinfo --short
```

ref: <https://opensource.com/article/19/9/linux-commands-hardware-information>

## Storage

```bash
lsblk
blkid
fdisk
cat /etc/fstab
```

### MDADM

REF: <https://www.ducea.com/2009/03/08/mdadm-cheat-sheet/>

## Log files

* `/var/log/auth.log`: keep track of all authentication attempts (successful or failed) on your system
* `faillog -a`: show fail log
* `sudo faillog -l 60 olivia`: lock out Olivia for 60 mins
* `sudo less /var/log/boot.log`: boot log
* `cat /var/log/apt/history.log`: Apt history

## Cron

`crontab -l`: current users crontab
`sudo crontab -l`: root's crontab?
`cat /etc/crontab`: system crontab file
`crontab -e`: edit crontab file (can't remember if this needs sudo or not)
`ls /etc/cron.d/`: indivudal crontab files
`ls /etc/cron.hourly`: indivudal scripts to run as root hourly
`ls /etc/cron.daily/`: indivudal scripts to run as root daily
`ls /etc/cron.weekly/`: indivudal scripts to run as root weekly
`ls /etc/cron.monthly/`: indivudal scripts to run as root monthly

`cat /etc/default/cron`: cron's default settings

Best website for refining crontab timings: [Crontab.guru - The cron schedule expression generator](https://crontab.guru/)

* <https://crontab.guru/examples.html>
* <https://crontab.guru/tips.html>

Very well know cron bug that has been left in there by design: <https://crontab.guru/cron-bug.html>

Also refer to [systemctl](#systemctl) commands for times and the links in [SystemD Links](#systemd-links) about timers. SystemD timers do the same thing as cron but they are newer.

## Accounts and Groups

`passwd -S USERNAME` shows the date and status of a users password.
> Display account status information. The status information consists of 7 fields. The first field is the user's login name. The second field indicates if the user account has a locked password (L), has no password (NP), or has a usable password (P). The third field gives the date of the last password change. The next four fields are the minimum age, maximum age, warning period, and inactivity period for the password. These ages are expressed in days.

`sudo passwd -l USERNAME`: Lock out a users password. Doesn't disable account, just doesn't allow password.
> [!CAUTION] Use `passwd -l` with caution
> This is not the best way to not get prompted for sudo. Because you can't run sudo with a locked password unless you have a no password entry. Use with caution if you don't have a way to roll back!

`sudo passwd -u USERNAME`: unlock password.\
`sudo usermod --expiredate 1 USERNAME`: Disables an account.\
`sudo faillog -l 60 olivia`: lock out Olivia for 60 mins

`sudo addgroup sshlogin`\
`sudo adduser XXX`\
`sudo adduser XXX sshlogin`: add other users group\
`sudo adduser XXX sudo`: if user also needs sudo\
`sudo useradd -m -G sshlogin,sudo XXX -s /bin/bash`: sets a users shell, shouldn't be needed much these days\
`sudo passwd XXX`: if you need to change user's password

## Main SystemD Commands

<https://systemd.io/>\
<https://commons.wikimedia.org/wiki/File:Systemd_components.svg>\
<https://www.freedesktop.org/software/systemd/man/latest/>\

### Important Commands

#### systemctl

`systemctl list-units`: lists enabled unit files\
`systemctl list-units --all`: lists enabled unit files\
`systemctl list-unit-files` list unit files (even those not enabled)\
`systemctl list-unit-files | grep enabled`\
`systemctl list-unit-files --all | grep packagename`\
`systemctl list-unit-files --state=masked`: list masked units
`sudo systemctl list-timers` list timers registered\
`sudo systemctl list-timers --all` list all timers\
`sudo systemctl cat mdcheck_start.timer`  show the unit file for the timer\
`sudo systemctl cat mdcheck_start.service` show the unit file for the service\
`sudo systemctl status mdcheck_start.service` check the status of a service\
`sudo systemctl restart mdcheck_start.service` restarts a service now\
`sudo systemctl stop mdcheck_start.service` stops a service now\
`sudo systemctl start mdcheck_start.service` starts a service now\
`sudo systemctl disable mdcheck_start.service` prevents a service from running at startup\
`sudo systemctl enable mdcheck_start.service` allows a service to run at startup\
`sudo systemctl enable --now mdcheck_start.service` allows a service to run at startup and also starts it now\
`sudo systemctl daemon-reload`: scan for new or changed units\
`sudo systemctl reload mdcheck_start.service`: reloads a unit and its configuration\
`sudo systemctl reenable mdcheck_start.service`: disables and re-enableds a unit (useful if units \[install\] section has changed)\
`sudo systemctl mask mdcheck_start.service`: Mask a unit to make it impossible to start both manually and as a dependancy, which makes masking dangerious. It makes a sim link of the unit file to /dev/null meaning it will never start.\
`sudo systemctl unmask mdcheck_start.service`: unmask a unit (there are more steps)\
`systemctl show --property=UnitPath`: show paths to unit files\
The main Unit paths are (listed from lowest to highest precedence):

* `/usr/lib/systemd/system/`: units provided by installed packages
* `/etc/systemd/system/`: units installed by the system administrator

`sudo systemctl | grep something` grep most systemctl services\
by 'most' remember a service can be:

* started/stopped
* enabled/disabled
* masked/unmasked - which changes pointers to /dev/null I think

You can have systemd override files (which apparently are like files in /etc/default/). these are supposed to be stored in: `/etc/systemd/system/snmptrapd.service.d/` for the snmptrapd.service

[https://wiki.archlinux.org/title/Systemd](https://wiki.archlinux.org/title/Systemd)

#### journalctl

`sudo journalctl -xe` most common use. jumps to end of journal logs and shows extra info about log entries

`sudo journalctl -e` jumps to the end
`sudo journalctl -u service_name` show logs about a particular service\
`sudo journalctl --no-pager` don't page logs\
`sudo journalctl -r` show logs in reverse order\
`sudo journalctl -n 25` show most recent 25 lines\
`sudo journalctl -f` follow logs live\
`sudo journalctl --utc` if you want them in utc\
`sudo journalctl -k` # Kernal messages only\
`sudo journalctl --since=yesterday --until=now`\
`sudo journalctl --since "2020-07-10 15:10:00" --until "2020-07-12"`\
`sudo journalctl -p 3 -xb` show only priority 3 (which is error) -b since last boot\

#### timedatectl

Time and date stuff if chrony or NTPD isn't installed. Taken from <https://documentation.ubuntu.com/server/how-to/networking/timedatectl-and-timesyncd/>.

`timedatectl status`: check the timedatectl status\
`timedatectl list-timezones`: show the timezones\
`sudo timedatectl set-timezone Australia/Sydney`: Sets the timezone to Australia/Sydney\
> [!TIP] Consider Distribution Rec Method
> Eg: Ubuntu usually recommends `sudo dpkg-reconfigure tzdata`

`sudo timedatectl set-local-rtc 0`: Maintains the RTC in UTC. set to 1 to maintain in local timezone.

`systemctl status systemd-timesyncd`: If masked or missing, you may have chrony installed.\
Timesyncd can configured in `/etc/systemd/timesyncd.conf` & `/etc/systemd/timesyncd.conf.d/`.

#### resolvectl

DNS Status: `resolvectl status`

Refresh DNS Settings in an Azure VM: `sudo netplan try`

> [!TIP] /etc/resolv.conf
> Starting is Ubuntu 20, resolv.conf file is a symbolic link of /run/systemd/resolve/stub-resolv.conf file. This makes sure that the updated DNS servers are reflected in /run/systemd/resolve/resolv.conf file. For more information, see [systemd-resolved](https://manpages.ubuntu.com/manpages/bionic/man8/systemd-resolved.service.8.html#:%7E:text=systemd%2Dresolved%20is%20a%20system,an%20LLMNR%20resolver%20and%20responder)

DNS Config: To force systemd-resolved to use the name servers you want to: `sudo resolvectl dns eth0 8.8.4.4 8.8.8.8`
> [!CAUTION]
>
> I would only use this overide to change the order of servers
> It most likely will ignore this commend if rebooted
> i'm not sure if things like netplan apply would override it

### Misc SystemD Commands

* hostnamectl
* localectl
* loginctl
* machinectl???

### SystemD Links

<https://systemd.io/>\
<https://commons.wikimedia.org/wiki/File:Systemd_components.svg>

* <https://www.freedesktop.org/software/systemd/man/latest/>
* <https://www.man7.org/linux/man-pages/man1/systemd.1.html>
* <https://www.digitalocean.com/community/tutorials/systemd-essentials-working-with-services-units-and-the-journal>
* <https://www.digitalocean.com/community/tutorials/how-to-use-journalctl-to-view-and-manipulate-systemd-logs>
* <https://www.digitalocean.com/community/tutorials/understanding-systemd-units-and-unit-files>
* <https://www.freedesktop.org/software/systemd/man/latest/>
* <https://linuxhandbook.com/journalctl-command/>
* <https://linuxconfig.org/how-to-schedule-tasks-with-systemd-timers-in-linux>
* <https://www.redhat.com/sysadmin/systemd-commands>
* <https://wiki.archlinux.org/title/Systemd>

## Network Commands

Netplan:
`sudo netplan try`: applies the netplan configs but will revert after X seconds if you don't press enter to confirm.\
`sudo netplan apply`: applies the netplan configs (have fun!)\
<https://documentation.ubuntu.com/server/explanation/networking/about-netplan/>\
<https://netplan.readthedocs.io/en/stable/howto/>

`ethtool`: Is a program that displays and changes Ethernet card settings such as auto-negotiation, port speed, duplex mode, and Wake-on-LAN. <https://documentation.ubuntu.com/server/explanation/networking/configuring-networks/#ethernet-interface-settings>\
`netstat`:
> [!NOTE] netstat
> netstat is a cross platform command existing in Unix, Linux, Mac and Windows but nearly all of them have different options/switches/parameters

`sudo netstat -tulpn`: show listening.

`nslookup`
`dig`
`hostname`
`dnsdomainname`

### Network Reference

<https://documentation.ubuntu.com/server/explanation/networking/configuring-networks/>\
<https://documentation.ubuntu.com/server/explanation/networking/about-netplan/>\
<https://netplan.readthedocs.io/en/stable/howto/>

## OpenSSL Commands

`openssl s_client -connect example.org:443`\
`openssl s_client -showcerts -connect example.org:443`\
`openssl s_client -connect google.com:443 -servername ibm.com`: using openssl with SNI\
`echo -n | openssl s_client -connect google.com:443 -servername ibm.com </dev/null | openssl x509 -noout -text | grep ibm.com`\
`openssl x509 -in /etc/ssl/certs/ldap.pem -text -noout | grep "Not After"`: show not after date on cert\
`openssl x509 -in /etc/ssl/certs/ldap.pem -text -noout | grep -A 1 "Serial Number"`: show serial number of cert\
`openssl pkcs12 -in filename.pfx -out cert.pem -nodes`: convert pfx to pem\
`openssl x509 -noout -text -in certificiate.crt -modulus`: check details on certification\
`openssl rsa -noout -text -in keyfile.ekey/key -modulus`: check details on key\
`openssl req -noout -text -in request.csr -modulus`: check details on request\
`openssl rsa -in encrypted-key-file.ekey -out unecrypted-key-file.key`: change encrypted key to unencrypted\

### OpenSSL Links

<https://www.xolphin.com/support/Certificate_conversions/Convert_pfx_file_to_pem_file>\
<http://help.globalscape.com/help/secureserver3/Converting_an_incompatible_traditional_PEM_encoded_encrypted_private_key.htm>\
<http://sycure.wordpress.com/2008/05/15/tips-using-openssl-to-extract-private-key-pem-file-from-pfx-personal-information-exchange/>\
<http://stackoverflow.com/questions/991758/how-to-get-an-openssl-pem-file-from-key-and-crt-files>\
<https://support.citrix.com/article/CTX136444#OpenSSL>\
<https://docs.citrix.com/en-us/citrix-gateway/12-1/install/certificate-management/how-to-convert-pfx-certificate-to-pem.html>\
<https://www.xolphin.com/support/Certificate_conversions/Convert_pfx_file_to_pem_file>\
<http://jefferytay.wordpress.com/2010/12/09/converting-a-pfx-file-to-pem-and-key-via-openssl/>\

To use a lower version of TLS (Results may vary in newer versions): <https://askubuntu.com/questions/1233186/ubuntu-20-04-how-to-set-lower-ssl-security-level>

## Misc System Commands

`sudo dpkg-reconfigure tzdata`: Set timezone\
`cat /proc/sys/net/ipv4/ip_forward` check the proc setting\
`echo 1 > /proc/sys/net/ipv4/ip_forward` set it temporaryly\
`sysctl -w net.ipv4.ip_forward=0` also set it temporaryly\
`sudo vi /etc/sysctl.conf` and add:

```bash
net.ipv4.ip_forward = 1
```

`sudo sysctl -p` to make it permanent.
