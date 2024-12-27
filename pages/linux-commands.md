---
title: Linux Commands
description: Linux commands to remember
---

[back](/)

# Linux Commands

* [Terminal Stuff](#terminal-stuff)
* [Files](#files)
  * [finding large directories and large files](#finding-large-directories-and-large-files)
* [Hardware Info](#hardware-info)
* [Storage](#storage)
  * [MDADM](#mdadm)
* [Log files](#log-files)
* [Main SystemD Commands](#main-systemd-commands)
  * [Important Commands](#important-commands)
    * [systemctl](#systemctl)
    * [journalctl](#journalctl)
    * [timedatectl](#timedatectl)
    * [resolvectl](#resolvectl)
  * [Misc Commands](#misc-commands)
  * [Links](#links)

## Terminal Stuff

```bash
watch
less
wc
```

## Files

### finding large directories and large files

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

## Main SystemD Commands

### Important Commands

#### systemctl

`systemctl list-unit-files` list unit files\
`systemctl list-unit-files |grep enabled`\
`sudo systemctl list-timers` list timers registered\
`sudo systemctl list-timers --all` list all timers\
`sudo systemctl cat mdcheck_start.timer`  show the unit file for the timer\
`sudo systemctl cat mdcheck_start.service` show the unit file for the service\
`sudo systemctl status mdcheck_start.service` check the status of a service\
`sudo systemctl restart mdcheck_start.service`\
`sudo systemctl stop mdcheck_start.service`\
`sudo systemctl | grep something` grep most systemctl services\
by 'most' remember a service can be:

* started/stopped
* enabled/disabled
* masked/unmasked - which changes pointers to /dev/null I think

#### journalctl

`sudo journalctl -xe` most common use. jumps to end of journal logs and shows extra info about log entries

`sudo journalctl -u service_name` show logs about a particular service\
`sudo journalctl --no-pager` don't page logs\
`sudo journalctl -r` show logs in reverse order\
`sudo journalctl -n 25` show most recent 25 lines\
`sudo journalctl -f` follow logs live\
`sudo journalctl --utc` if you want them in utc\
`sudo journalctl -k` # Kernal messages only\
`sudo journalctl -u service_name`\
`sudo journalctl --since=yesterday --until=now`\
`sudo journalctl --since "2020-07-10 15:10:00" --until "2020-07-12"`\
`sudo journalctl -p 3 -xb` show only priority 3 (which is error) -b since last boot\

#### timedatectl

Time and date stuff if chrony or NTPD isn't installed

#### resolvectl

DNS Config

Force systemd-resolved to use the name servers you want to: `sudo resolvectl dns eth0 8.8.4.4 8.8.8.8`
> [!CAUTION]
>
> I would only use this overide to change the order of servers
> It most likely will ignore this commend if rebooted
> i'm not sure if things like netplan apply would override it

### Misc Commands

* hostnamectl
* localectl
* loginctl
* machinectl???

### Links

* <https://www.digitalocean.com/community/tutorials/systemd-essentials-working-with-services-units-and-the-journal>
* <https://www.digitalocean.com/community/tutorials/how-to-use-journalctl-to-view-and-manipulate-systemd-logs>
* <https://www.digitalocean.com/community/tutorials/understanding-systemd-units-and-unit-files>
* <https://www.freedesktop.org/software/systemd/man/latest/>
* <https://linuxhandbook.com/journalctl-command/>
* <https://linuxconfig.org/how-to-schedule-tasks-with-systemd-timers-in-linux>
* <https://www.redhat.com/sysadmin/systemd-commands>
