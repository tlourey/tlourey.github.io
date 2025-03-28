---
title: Linux Commands
description: Linux commands to remember
categories:
    - Tech
type: pages
layout: pages
published: true
fmContentType: pages
date: 2024-12-13T15:22:00
lastmod: 2025-03-28T04:26:11.571Z
tags:
    - Commands
    - Linux
    - References
isdraft: false
---

<!--- cSpell:disable --->
* [Operating System Commands](#operating-system-commands)
  * [man pages](#man-pages)
* [Terminal Stuff](#terminal-stuff)
  * [Terminal Filtering and Monitoring](#terminal-filtering-and-monitoring)
  * [Aliases](#aliases)
  * [TMUX](#tmux)
  * [Serial Stuff](#serial-stuff)
* [Files](#files)
  * [What process is using a file](#what-process-is-using-a-file)
  * [ls options often forgotten](#ls-options-often-forgotten)
  * [Finding large directories and large files](#finding-large-directories-and-large-files)
  * [Compressing and Decompressing files](#compressing-and-decompressing-files)
  * [Compressed Log Files](#compressed-log-files)
* [Hardware](#hardware)
  * [Hardware Info](#hardware-info)
  * [rfkill](#rfkill)
  * [bluetoothctl](#bluetoothctl)
* [Storage](#storage)
  * [MDADM](#mdadm)
* [Logging and Log files](#logging-and-log-files)
* [Cron](#cron)
* [Accounts and Groups](#accounts-and-groups)
* [Apt](#apt)
  * [changelog](#changelog)
* [dnf](#dnf)
* [Main SystemD Commands](#main-systemd-commands)
  * [Important Commands](#important-commands)
    * [systemctl](#systemctl)
    * [journalctl](#journalctl)
    * [timedatectl](#timedatectl)
    * [resolvectl](#resolvectl)
  * [Misc SystemD Commands](#misc-systemd-commands)
  * [SystemD Links](#systemd-links)
* [Network Commands](#network-commands)
  * [netstat](#netstat)
  * [tcpdump](#tcpdump)
  * [Network Reference](#network-reference)
* [OpenSSL Commands](#openssl-commands)
  * [OpenSSL Links](#openssl-links)
* [SSH](#ssh)
* [SSH Client](#ssh-client)
  * [Port Forwarding](#port-forwarding)
  * [Reverse Port Forwarding](#reverse-port-forwarding)
* [SSH Keys](#ssh-keys)
  * [SSHD](#sshd)
* [Misc System Commands](#misc-system-commands)
<!--- cSpell:enable --->

<!---
* [ ] needsreboot package - also consider if it should be documented in linux-tools.md

-->

## Operating System Commands

Distro Version:

`cat /etc/os-release`:TBA\
`cat /etc/*-release`: TBA\
`cat /etc/issue`:TBA\
`hostnamectl`:TBA - see more in [Main SystemD Commands](#main-systemd-commands)\
`lsb_release -a`:tba - may not exist on some Redhat machines by default

`cat /etc/debian_version`:TBA\
`cat /etc/redhat-release`:TBA

Kernel Version:
`uname`:TBA\
`uname -a`:TBA\
`uname -r`:TBA\
`uname -mrs`:TBA\
`cat /proc/version`:TBA

More:

* <https://www.cyberciti.biz/faq/find-linux-distribution-name-version-number/>
* <https://www.cyberciti.biz/faq/how-do-i-determine-rhel-version/>
* <https://www.cyberciti.biz/faq/how-to-check-ubuntu-version-in-linux-command-line/>

### man pages

`man topic`\
`man man` to know more about the man command itself.

Some tips on the man command: <https://www.redhat.com/en/blog/top-five-man-options>

Web based man pages:

* **<https://linux.die.net/man/>**
* <https://www.man7.org/linux/man-pages/>
* <https://wiki.archlinux.org/title/Man_page>

* <https://manpages.ubuntu.com/>
* <https://manpages.debian.org/>

> [!NOTE] Man page sections
> 1 - Executable programs or shell commands
> 2 - System calls (functions provided by the kernel)
> 3 - Library calls (functions within program libraries)
> 4 - Special files (usually found in /dev)
> 5 - File formats and conventions, e.g. /etc/passwd
> 6 - Games
> 7 - Miscellaneous (including macro packages and conventions), e.g., man(7), groff(7)
> 8 - System administration commands (usually only for root)
> 9 - Kernel routines [Non-standard]

## Terminal Stuff

### Terminal Filtering and Monitoring

```bash
watch
less
wc
column
tail
tail -f
```

### Aliases

```bash
alias list='ls -la'
alias ls='ls -h' # other options will still work such as ls -la but the -h will be added.
alias [alias]='[path-to-script]/[filename].sh'
```

To make permanent, add alias to:

* Bash shell: ~/.bashrc
* Zsh shell: ~/.zshrc
* Tcsh shell: ~/.tcshrc
* Fish shell: ~/.config/fish/config.fish

> [!NOTE] Double edged sword
> If you add an option to a command as an alias, when you remote to a new system, it may not have that alias. Consider the usefulness of a permanent alias vs the gain in muscle memory

### TMUX
<!-- cspell:ignore Byobu -->
* [ ] TMUX
* [ ] Byobu
* [ ] screen

### Serial Stuff

Query comms / serial port settings: `stty < /dev/ttyS0`\
`screen /dev/ttyS0 <speed>`

Consider:

* `minicom`
* `picocom`
* `setserial`
* `cu -l /dev/ttyS0 -s 9600`

More info: <https://unix.stackexchange.com/questions/22545/how-to-connect-to-a-serial-port-as-simple-as-using-ssh>

## Files

### What process is using a file

```bash
fuser /var/log/syslog
# Will come back with a process id
ps aux | grep <Process ID from above>
```

### ls options often forgotten

-t: sort by time, newest first
-h: human readable sizes
-S: sort by file size, largest first
-r: reverse
-R: recursive
--time: options are:

* access time (-u): atime, access, use;
* change time (-c): ctime, status;
* birth time: birth, creation;

-u: sort by access time
-c:

* with -lt: sort by, and show, ctime (time of last modification of file status information);
* with -l: show ctime and sort by name;
* otherwise: sort by ctime, newest first

-X: sort by extensions
-x: lines instead of columns

### Finding large directories and large files

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

### Compressing and Decompressing files

`tar -zcvf <<archive name>>.tgz files-to-compress`\
`tar -zxvf <<archive name>>.tgz location-to-extract`

Options:

* -c: create an archive
* -x: extract from an archive
* -f: filename of archive
* -v: verbose
* -z: use Gzip compression
* -t: list files in archive
* -r: updates or adds files to existing archive (without recreating it)
* -u: add files to existing archive
* -A: move multiple archives into one
* -j: use bzip2 (.tar.bz2)
* -W: verify extension

`gunzip [Options] [archive-name/filename]`

`gzip file.txt`: zips file.txt into file.gz\
`gunzip file.gz`: unzip file.gz and then delete file.gz leaving only file.txt

Options:
-h: show all options
-c: view text in file
-f: force (not sure why)
-k: keep original file after (un)zipping
-l: give details on filename
-r: recursive
-v: verbose
-t: test if file is valid
-a: only works on windows. uses ASCII to convert end-of-line characters using local conversion.

More options are available. Look at: <https://www.geeksforgeeks.org/gunzip-command-in-linux-with-examples/>

Other Zip Commands:

```bash
zipdetails
zipinfo
```

### Compressed Log Files

When using things like logrotate that compress log files you don't want to have to uncompress them every time to run the usual commands against them. You can try these commands when working with compressed log files:

```bash
zgrep
zcat
zless
zmore
zdiff
zcmp
zegrep
```

Note that some of the z commands don't support some of the options the regular utility does. eg: `zgrep` doesn't support `--recursive (-r)`. Check the man pages for more info.

Some examples:

`zless SwitchName.log.* | grep ab:cd:ef:12:34:56`: search a compressed switch log for a mac address\
`zcat 192.168.1.2_abcdef123456.log.* | grep 2025-03-19 | grep 12:34:56:ab:cd:ef`: search a compressed UniFi AP log file for a mac address on a specific date\
`zgrep searchstring /var/log/apache2/access.log.*`: search for `searchstring` in `/var/log/apache2/access.log.*` (which includes files in like `access.log.4.gz`)

## Hardware

### Hardware Info

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

### rfkill

```bash
rfkill --output ID,TYPE
rfkill block all
rfkill unblock wlan
rfkill block bluetooth uwb wimax wwan gps fm nfc
```

rfkill is part of [systemd](#systemd-links)

### bluetoothctl

`agent on`: Turns bluetooth agent on\
`default agent`: sets bluetoothctl as default agent to manage bluetooth\
`scan on`: start scanning\
`scan off`: stop scanning\
`trust <<INSERT MAC ADDRESS OF DEVICE>>`: trust a specific device.\
`connect <<INSERT MAC ADDRESS OF DEVICE>>`: connect to a specific device\
`remove <<INSERT MAC ADDRESS OF DEVICE>>`: removes device from list. This should be tried before all others. Ideally either before or after `trust`\
`pair <<INSERT MAC ADDRESS OF DEVICE>>`: shouldn't be needed for keyboard and mouse but may be.\
`info <<INSERT MAC ADDRESS OF DEVICE>>`: show info about the device.\
`power off`: turn the bluetooth controlled off (this isn't rfkill)

> [!NOTE] NOTE
> If its a keyboard it should come back with 6 digits to type into the keyboard. Type them and press enter

More bluetoothctl commands: <https://manpages.debian.org/unstable/bluez/bluetoothctl.1.en.html>

## Storage

```bash
lsblk
blkid
fdisk
cat /etc/fstab
```

### MDADM

REF: <https://www.ducea.com/2009/03/08/mdadm-cheat-sheet/>

## Logging and Log files

* `/var/log/auth.log`: keep track of all authentication attempts (successful or failed) on your system
* `faillog -a`: show fail log
* `sudo faillog -l 60 olivia`: lock out Olivia for 60 mins
* `sudo less /var/log/boot.log`: boot log
* `cat /var/log/apt/history.log`: Apt history

Some Tips to test/evaluate syslog message via the network are in [Microsoft Sentinel Tips](/pages/microsoft-sentinel-tips.md#syslog-connector-testing)

## Cron

`crontab -l`: current users crontab
`sudo crontab -l`: root's crontab?
`cat /etc/crontab`: system crontab file
`crontab -e`: edit crontab file (can't remember if this needs sudo or not)
`ls /etc/cron.d/`: individual crontab files
`ls /etc/cron.hourly`: individual scripts to run as root hourly
`ls /etc/cron.daily/`: individual scripts to run as root daily
`ls /etc/cron.weekly/`: individual scripts to run as root weekly
`ls /etc/cron.monthly/`: individual scripts to run as root monthly

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

> [!CAUTION] Use `passwd -l` with caution**
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

## Apt

TBC
<!---
* [ ] apt vs apt-get vs aptitude vs dpkg
* [ ] link out to reference and guidance
--->

### changelog

TBC
<!---
* [ ] cover apt changelog /apt-get changelog
* [ ] cover apt-listchanges - see https://askubuntu.com/questions/272215/seeing-apt-get-changelogs-for-to-be-upgraded-packages
  * may need to be installed
  * can use a oneliner to get changelogs that doesn't need sudo: (cd $(mktemp -d) && apt download $(apt list -qq --upgradable | cut -f1 -d"/") && apt-listchanges *.deb)
  * ubuntu lts 20 doesn't support apt-listchanges --latest. For versions that do the following has pretty good output:
    ```
    (cd $(mktemp -d) && apt download $(apt list -qq --upgradable | cut -f1 -d"/") && apt-listchanges -h --latest=1 *.deb) | grep urgency
    WARNING: apt does not have a stable CLI interface. Use with caution in scripts.

    WARNING: apt does not have a stable CLI interface. Use with caution in scripts.

    linux (5.15.0-135.146) jammy; urgency=medium
    tzdata (2025a-0ubuntu0.22.04) jammy; urgency=medium
    ```
* [ ] cover apt-show-versions - see https://askubuntu.com/a/556399/443835
  * Needs to be installed
  * Can be used with regex like: apt-show-versions | grep upgradeable | grep security
  * or apt-show-versions -u, or apt-show-versions -u -b | grep security
  * apt-show-versions listed a package as being -seurity when it wasn't using other tools like apt list --upgradable or apt-check
* [ ] cover apt-check - https://askubuntu.com/questions/441921/why-does-usr-lib-update-notifier-apt-check-not-agree-with-apt-get-upgrade
* [ ] consider text about urgency / cve matching
* [ ] link in with nagios check_apt critical options and critical regex
* [ ] cover which of the above are included with ubuntu vs being 3rd party
-->

## dnf

`sudo dnf upgrade`: update packages\
`sudo dnf system-upgrade`: update os to latest releaase

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
`sudo systemctl start mdcheck_start.service` starts a service now. Can also be used to run a timer manually unless timer is configured with `RefuseManualStart=yes` or `RefuseManualStop=yes`\
`sudo systemctl disable mdcheck_start.service` prevents a service from running at startup\
`sudo systemctl enable mdcheck_start.service` allows a service to run at startup\
`sudo systemctl enable --now mdcheck_start.service` allows a service to run at startup and also starts it now\
`sudo systemctl daemon-reload`: scan for new or changed units\
`sudo systemctl reload mdcheck_start.service`: reloads a unit and its configuration\
`sudo systemctl reenable mdcheck_start.service`: disables and re-enableds a unit (useful if units \[install\] section has changed)\
`sudo systemctl mask mdcheck_start.service`: Mask a unit to make it impossible to start both manually and as a dependency, which makes masking dangerous. It makes a sim link of the unit file to /dev/null meaning it will never start.\
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

**`sudo journalctl -xe`** most common use. jumps to end of journal logs and shows extra info about log entries

`sudo journalctl -e` jumps to the end\
`sudo journalctl -u service_name` show logs about a particular service\
`sudo journalctl --no-pager` don't page logs\
`sudo journalctl -r` show logs in reverse order\
`sudo journalctl -n 25` show most recent 25 lines\
`sudo journalctl -f` follow logs live\
`sudo journalctl --utc` if you want them in utc\
`sudo journalctl -k` # Kernal messages only\
`sudo journalctl --since=yesterday --until=now`\
`sudo journalctl --since "2020-07-10 15:10:00" --until "2020-07-12"`\
`sudo journalctl -p 3 -xb` show only priority 3 (which is error) -b since last boot

#### timedatectl

Time and date stuff if chrony or NTPD isn't installed. Taken from <https://documentation.ubuntu.com/server/how-to/networking/timedatectl-and-timesyncd/>.

`timedatectl status`: check the timedatectl status\
`timedatectl list-timezones`: show the timezones\
`sudo timedatectl set-timezone Australia/Sydney`: Sets the timezone to Australia/Sydney

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

> [!CAUTION] CAUTION
> I would only use this override to change the order of servers
> It most likely will ignore this commend if rebooted
> i'm not sure if things like netplan apply would override it

### Misc SystemD Commands

* hostnamectl
* localectl
* loginctl
* machinectl???
* [bluetoothctl (refer above)](#bluetoothctl)

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

Also see [rfkill](#rfkill)

## Network Commands

Netplan:
`sudo netplan try`: applies the netplan configs but will revert after X seconds if you don't press enter to confirm.\
`sudo netplan apply`: applies the netplan configs (have fun!)\
<https://documentation.ubuntu.com/server/explanation/networking/about-netplan/>\
<https://netplan.readthedocs.io/en/stable/howto/>

`ethtool`: Is a program that displays and changes Ethernet card settings such as auto-negotiation, port speed, duplex mode, and Wake-on-LAN. <https://documentation.ubuntu.com/server/explanation/networking/configuring-networks/#ethernet-interface-settings>\

### netstat

`netstat`:

> [!NOTE] netstat
> netstat is a cross platform command existing in Unix, Linux, Mac and Windows but nearly all of them have different options/switches/parameters

`sudo netstat -tulpn` or `sudo netstat -lnptv`: show listening.\
`sudo netstat -lanp`: show active and listening\
`sudo netstat -lanp | grep 22`: grep active and listening for port 22

`nslookup`\
`dig`\
`hostname`\
`dnsdomainname`

`nc`: netcat: <https://manpages.org/nc>

<https://nc110.sourceforge.io/>

* [ ] add in common netcat commands

### tcpdump

`sudo tcpdump -i eth0 -nn -s0 -v port 80`

* -i : Select interface that the capture is to take place on, this will often be an ethernet card or wireless adapter but could also be a vlan or something more unusual. Not always required if there is only one network adapter.
* -nn : A single (n) will not resolve hostnames. A double (nn) will not resolve hostnames or ports. This is handy for not only viewing the IP / port numbers but also when capturing a large amount of data, as the name resolution will slow down the capture.
* -s0 : Snap length, is the size of the packet to capture. -s0 will set the size to unlimited - use this if you want to capture all the traffic. Needed if you want to pull binaries / files from network traffic.
* -v : Verbose, using (-v) or (-vv) increases the amount of detail shown in the output, often showing more protocol specific information.

`tcpdump`: packet capture\
`sudo tcpdump -n udp port 514 -vv`: Capture UDP Port 512 but don't show me all the details in verbose.\
`sudo tcpdump -n udp port 514 -A -vv`: Capture UDP Port 512 AND show me all the details in verbose.\
`sudo tcpdump -i eth0 proto 17`: capture protocol 17 (udp) on eth0\
`sudo tcpdump -i any port 514 -A -vv`: capture on any interface port 514 and show me all the details in verbose\
`sudo tcpdump -i eth0 ip 192.168.1.10`: captures traffic to or from 192.168.1.10 on eth0\
`sudo tcpdump -i eth0 dst 10.10.1.20`: capture traffic on eth0 going to 10.10.1.20\
`sudo tcpdump -i eth0 -s0 -w test.pcap`: capture all traffic on eth0 (snap length) and write it to a packet capture file\
`tcpdump -i eth0 -U -w - 'host 192.168.2.29 and (port 22222 or port 22221 or port 80)'`: uses and & or statements. Using in brackets is better to prevent shell getting in the way. (()) in zsh (mac)

<https://www.tcpdump.org/manpages/tcpdump.1.html>

tcpdump exmaples:

* <https://github.com/tcpdump-examples/how-to-use-tcpdump>
* <https://danielmiessler.com/blog/tcpdump>
* <https://hackertarget.com/tcpdump-examples/>

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

## SSH

## SSH Client

`ssh username@host`\
`ssh username@host -p customportno`\
`ssh username@host -i /path/to/identitykey`\
`ssh username@host -J jumpusername@jumphost:jumpport`\
`ssh username@host -B eth0`: bind to an interface\
`ssh username@host -b 192.168.1.25`: bind to an ip address\
`ssh username@host -v`: verbose - useful for diagnosing automation and auth issues.

* [x] port forwading commands
* [x] reverse port forward commands
* [ ] add in commands and info for control socket connection sharing (ControlPath and ControlMaster)
* [ ] tunnel commands

### Port Forwarding

To forward a local port (say 5110) to a remote destination (say popserver.example.com port 110), you can write something like one of these:

```bash
ssh username@host -L 5110:popserver.example.com:110
ssh username@host -L 8080:webserver.example.com:80
ssh username@host -L 8443:192.168.1.1:443
```

To specify an IP address for the listening end of the tunnel, prepend it to the argument:

`ssh username@host -L 127.0.0.5:23:localhost:23 myhost`

From the SSH man page:

> ```bash
> ssh username@host -L [bind_address:]port:host:hostport
> ssh username@host -L [bind_address:]port:remote_socket
> ssh username@host -L local_socket:host:hostport
> ssh username@host -L local_socket:remote_socket
> ```
>
> Specifies that connections to the given TCP port or Unix socket on the local (client) host are to be forwarded to the given host and port, or Unix socket, on the remote side.  This works by allocating a socket to listen to either a TCP port on the local side, optionally bound to the specified bind_address, or to a Unix socket.  Whenever a connection is made to the local port or socket, the connection is forwarded over the secure channel, and a connection is made to either host port hostport, or the Unix socket remote_socket, from the remote machine.
>
> Port forwardings can also be specified in the configuration file.  Only the superuser can forward privileged ports.  IPv6 addresses can be specified by enclosing the address in square brackets.
>
> By default, the local port is bound in accordance with the GatewayPorts setting.  However, an explicit bind_address may be used to bind the connection to a specific address.  The bind_address of "localhost" indicates that the listening port be bound for local use only, while an empty address or '*' indicates that the port should be available from all interfaces.

### Reverse Port Forwarding

To forward a remote port to a local destination, just use the -R option instead of -L:

```bash
ssh username@host -R 5023:mytelnetserver.myhouse.org:23
```

From the SSH man page:

> ```bash
> ssh username@host -R [bind_address:]port:host:hostport
> ssh username@host -R [bind_address:]port:local_socket
> ssh username@host -R remote_socket:host:hostport
> ssh username@host -R remote_socket:local_socket
> ssh username@host -R [bind_address:]port
> ```
>
> Specifies that connections to the given TCP port or Unix socket on the remote (server) host are to be forwarded to the local side.
>
> This works by allocating a socket to listen to either a TCP port or to a Unix socket on the remote side.  Whenever a connection is made to this port or Unix socket, the connection is forwarded over the secure channel, and a connection is made from the local machine to either an explicit destination specified by host port hostport, or local_socket, or, if no explicit destination was specified, ssh will act as a SOCKS 4/5 proxy and forward connections to the destinations requested by the remote SOCKS client.
>
> Port forwardings can also be specified in the configuration file. Privileged ports can be forwarded only when logging in as root on the remote machine.  IPv6 addresses can be specified by enclosing the address in square brackets.
>
> By default, TCP listening sockets on the server will be bound to the loopback interface only.  This may be overridden by specifying a bind_address.  An empty bind_address, or the address '*', indicates that the remote socket should listen on all interfaces.  Specifying a remote bind_address will only succeed if the server's GatewayPorts option is enabled (see sshd_config(5)).
>
> If the port argument is '0', the listen port will be dynamically allocated on the server and reported to the client at run time.  When used together with -O forward, the allocated port will be printed to the standard output.

## SSH Keys

* [ ] Add in SSH Keygen stuff
* [ ] Add in ssh key copy stuff
* [ ] Add in authorised keys file management tips

### SSHD

`sudo sshd -T`:Show sshd current **running** config

## Misc System Commands

`sudo dpkg-reconfigure tzdata`: Set timezone\
`cat /proc/sys/net/ipv4/ip_forward` check the proc setting\
`echo 1 > /proc/sys/net/ipv4/ip_forward` set it temporarily\
`sysctl -w net.ipv4.ip_forward=0` also set it temporarily\
`sudo vi /etc/sysctl.conf` and add:

```bash
net.ipv4.ip_forward = 1
```

`sudo sysctl -p` to make it permanent.
