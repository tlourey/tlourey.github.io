---
title: Linux Commands
description: Linux commands to remember
categories:
- References
- Commands
- Linux
type: pages
---

[home](/) [up](./)

* [Terminal Stuff](#terminal-stuff)
* [Files](#files)
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
  * [Misc SystemD Commands](#misc-systemd-commands)
  * [SystemD Links](#systemd-links)
* [OpenSSL Commands](#openssl-commands)
  * [OpenSSL Links](#openssl-links)
* [Misc System Commands](#misc-system-commands)

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

## Main SystemD Commands

<https://systemd.io/>
<https://commons.wikimedia.org/wiki/File:Systemd_components.svg>
<https://www.freedesktop.org/software/systemd/man/latest/>

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

Time and date stuff if chrony or NTPD isn't installed

#### resolvectl

DNS Config

Force systemd-resolved to use the name servers you want to: `sudo resolvectl dns eth0 8.8.4.4 8.8.8.8`
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

<https://systemd.io/>
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

## OpenSSL Commands

`openssl s_client -connect example.org:443`
`openssl s_client -showcerts -connect example.org:443`
`openssl s_client -connect google.com:443 -servername ibm.com`: using openssl with SNI
`echo -n | openssl s_client -connect google.com:443 -servername ibm.com </dev/null | openssl x509 -noout -text | grep ibm.com`
`openssl x509 -in /etc/ssl/certs/ldap.pem -text -noout | grep "Not After"`: show not after date on cert
`openssl x509 -in /etc/ssl/certs/ldap.pem -text -noout | grep -A 1 "Serial Number"`: show serial number of cert
`openssl pkcs12 -in filename.pfx -out cert.pem -nodes`: convert pfx to pem
`openssl x509 -noout -text -in certificiate.crt -modulus`: check details on certification
`openssl rsa -noout -text -in keyfile.ekey/key -modulus`: check details on key
`openssl req -noout -text -in request.csr -modulus`: check details on request
`openssl rsa -in encrypted-key-file.ekey -out unecrypted-key-file.key`: change encrypted key to unencrypted

### OpenSSL Links

<https://www.xolphin.com/support/Certificate_conversions/Convert_pfx_file_to_pem_file>
<http://help.globalscape.com/help/secureserver3/Converting_an_incompatible_traditional_PEM_encoded_encrypted_private_key.htm>
<http://sycure.wordpress.com/2008/05/15/tips-using-openssl-to-extract-private-key-pem-file-from-pfx-personal-information-exchange/>
<http://stackoverflow.com/questions/991758/how-to-get-an-openssl-pem-file-from-key-and-crt-files>
<https://support.citrix.com/article/CTX136444#OpenSSL>
<https://docs.citrix.com/en-us/citrix-gateway/12-1/install/certificate-management/how-to-convert-pfx-certificate-to-pem.html>
<https://www.xolphin.com/support/Certificate_conversions/Convert_pfx_file_to_pem_file>
<http://jefferytay.wordpress.com/2010/12/09/converting-a-pfx-file-to-pem-and-key-via-openssl/>

To use a lower version of TLS (Results may vary in newer versions): <https://askubuntu.com/questions/1233186/ubuntu-20-04-how-to-set-lower-ssl-security-level>

## Misc System Commands

`sudo dpkg-reconfigure tzdata`: Set timezone
`cat /proc/sys/net/ipv4/ip_forward` check the proc setting
`echo 1 > /proc/sys/net/ipv4/ip_forward` set it temporaryly
`sysctl -w net.ipv4.ip_forward=0` also set it temporaryly
`sudo vi /etc/sysctl.conf` and add:

```bash
net.ipv4.ip_forward = 1
```

`sudo sysctl -p`

to make it permanent.
