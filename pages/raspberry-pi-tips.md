---
title: Raspberry Pi Tips
description: Tips and tricks for the PI.
published: true
categories:
    - Tech
type: pages
layout: pages
date: 2025-03-02T12:22:10.320Z
lastmod: 2025-04-06T01:13:44.538Z
tags:
    - RaspberryPi
    - Tips
isdraft: true
fmContentType: pages
mermaid: "false"
preview: ""
---

<!--- cSpell:disable --->
* [Documentation](#documentation)
* [Differenes between RaspberryPi OS Editions](#differenes-between-raspberrypi-os-editions)
* [Setting a static IP on a Pi using Bookworm](#setting-a-static-ip-on-a-pi-using-bookworm)
  * [Use a DHCP Reservation](#use-a-dhcp-reservation)
  * [Network Manager](#network-manager)
  * [/etc/network/interfaces](#etcnetworkinterfaces)
* [full-update](#full-update)
* [Firmware Upgrade](#firmware-upgrade)
* [raspi-config non-interactive](#raspi-config-non-interactive)
* [Read only SD Card](#read-only-sd-card)
* [config.txt](#configtxt)
* [Controlling a Raspberry Pi Fan](#controlling-a-raspberry-pi-fan)
  * [Checking settings](#checking-settings)
  * [Modifying RPM Config](#modifying-rpm-config)
* [vcgencmd](#vcgencmd)
* [vclog](#vclog)
* [rfkill](#rfkill)
* [Pairing a Bluetooth Keyboard](#pairing-a-bluetooth-keyboard)
* [Tools](#tools)
<!--- cSpell:enable --->

## Documentation

<https://www.raspberrypi.com/documentation/>

## Differenes between RaspberryPi OS Editions

<https://forums.raspberrypi.com/viewtopic.php?t=339721>

## Setting a static IP on a Pi using Bookworm

### Use a DHCP Reservation

Crappy but seems offical: <https://www.raspberrypi.com/documentation/computers/configuration.html#assign-a-static-ip-address>

### Network Manager

<https://networkmanager.dev/docs/api/latest/nmcli.html>\
<https://networkmanager.dev/docs/api/latest/nmcli.html#:~:text=Examples,-This%20section%20presents>\
<https://networkmanager.dev/docs/api/latest/nmcli-examples.html>

```bash
sudo nmcli c show
nmcli con show
# sudo nmcli con mod "Your Connection Name" ipv4.addresses "192.168.1.100/24" ipv4.gateway "192.168.1.1" ipv4.dns "8.8.8.8" ipv4.method manual
sudo nmcli con mod "Wired connection 1" ipv4.addresses 192.168.1.22/24 ipv4.gateway 192.168.1.1 ipv4.dns 192.168.1.1 ipv4.method manual
sudo nmcli con mod "Wired connection 1" -ipv4.address "192.168.1.100/24"
nmcli device wifi list
nmcli device wifi connect "$SSID" password "$PASSWORD"
nmcli --ask device wifi connect "$SSID"
sudo systemctl restart NetworkManager
```

### /etc/network/interfaces

```ini
iface eth0 inet static
address 192.168.1.100        # Your desired static IP address
netmask 255.255.255.0        # Your subnet mask
gateway 192.168.1.1          # Your gateway (router) IP address
dns-nameservers 8.8.8.8      # DNS server(s) - You can add multiple servers
```

Also consider setting up configs in source `/etc/network/interfaces.d/*`

## full-update

From: <https://www.raspberrypi.com/documentation/computers/os.html#manage-software-packages-with-apt>

> [!TIP]
> Unlike Debian, Raspberry Pi OS is under continual development. As a result, package dependencies sometimes change, so you should always use `full-upgrade` instead of the standard `upgrade`.

```bash
sudo apt update
sudo apt full-upgrade
```

## Firmware Upgrade

> [!WARNING]
> Pre-release versions of software are not guaranteed to work. Do not use rpi-update on any system unless recommended to do so by a Raspberry Pi engineer. It could leave your system unreliable or broken. **Do not use rpi-update as part of any regular update process**.

Uses apt package: `raspi3-firmware`

<https://www.raspberrypi.com/documentation/computers/os.html#rpi-update>

rpi-update downloads the latest pre-release version of the Linux kernel, its matching modules, device tree files, and the latest versions of the VideoCore firmware. It then installs these files into an existing Raspberry Pi OS install.

```bash
sudo rpi-update
sudo reboot
```

White paper on firmware updates: <https://pip.raspberrypi.com/categories/685-whitepapers-app-notes/documents/RP-003476-WP/Updating-Pi-firmware.pdf>

[Downgrade firmware to the last stable release](https://www.raspberrypi.com/documentation/computers/os.html#downgrade-firmware-to-the-last-stable-release)

## raspi-config non-interactive

<https://www.raspberrypi.com/documentation/computers/configuration.html#raspi-config-cli>

## Read only SD Card

<https://core-electronics.com.au/guides/read-only-raspberry-pi/>

To Enable:

1. `sudo raspi-config`
2. Select Performance Options
3. Select Overlay File System
4. When prompted "Would you like the overlay file system to be enabled?" select 'Yes'
5. wait while /boot/initrd is generated
6. Press Ok for overlay
7. When prompted "Would you like the boot partition to be write protected" select Yes
8. Select ok when advised "the boot partition is read only"

To Revert back:

1. `sudo raspi-config`
2. Select Performance Options
3. Select Overlay File System
4. When prompted "Would you like the overlay file system to be enabled?" select 'No'
5. Press Ok when advised the overlay file system is disabled
6. You will then be advised that the current partition is read only and you need to reboot
7. Then go to disable it again.
8. This time you will be asked "would you like the boot partition to be write protected?" Select 'No'
9. Press ok. You may have to reboot again

Script I found to do this while googing: <https://github.com/ghollingworth/overlayfs/blob/master/overctl> and also <https://yagrebu.net/unix/rpi-overlay.md#:~:text=Finishing%20Touches-,Read%2DOnly%20/boot,-The%20/boot%20filesystem>

## config.txt

RaspberryPi BIOS Settings

For bookworm onwards its located in: `/boot/firmware/config.txt`\
Before bookworm it was in `/boot/config.txt`

<https://www.raspberrypi.com/documentation/computers/config_txt.html#what-is-config-txt>

## Controlling a Raspberry Pi Fan

### Checking settings

`cat /sys/class/hwmon/hwmon0/pwm1`\
`cat /sys/class/thermal/thermal_zone0/trip_point_0_temp`\
`cat /sys/class/thermal/thermal_zone0/trip_point_1_temp`\

### Modifying RPM Config

from: <https://github.com/raspberrypi/linux/issues/2715#issuecomment-769405042>

1. SSH into your pi
2. Navigate to the boot directory by using the command: `cd /boot`
3. Open the config.txt file in nano by using the command: `sudo nano config.txt`
4. Use the down arrow to go to the bottom of this file.
5. Add these 5 lines changing the temp to whatever you prefer. Noting 65 Degrees Celsius = 65000. In addition, the fan has 4 speeds this just sets at what temperatures the fan speed changes. I wanted it to be super silent so my temperature targets are very aggressive. Running a Unifi controller for 5 months with occasional 40 degree Celsius days with no issues so far.

```config
# PoE Hat Fan Speeds
dtparam=poe_fan_temp0=65000
dtparam=poe_fan_temp1=70000
dtparam=poe_fan_temp2=75000
dtparam=poe_fan_temp3=80000
```

7. Press 'Control+X' on your keyboard to exit
8. Press 'Y' on your keyboard to agree to overwriting the file
9. Press 'Enter' to confirm
10. This will close the nano text editor
11. reboot your pi using the command
12. sudo reboot
13. The fan should work with your new settings now

## vcgencmd

`vcgencmd measure_temp`: Get temp of Pi\
`vcgencmd get_config`: show config.txt settings. see <https://www.raspberrypi.com/documentation/computers/config_txt.html#what-is-config-txt>\
`vcgencmd commands`: show other vcgencmd commands

More info:

* <https://www.raspberrypi.com/documentation/computers/os.html#vcgencmd>
* <https://github.com/raspberrypi/documentation/blob/bd97e2f9aaf9f41ae36e6c8b54083ae6573d9d28/raspbian/applications/vcgencmd.md>
* <https://github.com/raspberrypi/documentation/blob/bd97e2f9aaf9f41ae36e6c8b54083ae6573d9d28/raspbian/applications/vcdbg.md>

## vclog

From <https://www.raspberrypi.com/documentation/computers/os.html#vclog>

`vclog` displays log messages from the VideoCore GPU from Linux running on the Arm. It needs to be run as root.\
`sudo vclog --msg`: prints out the message log\
`sudo vclog --assert`: prints out the assertion log.

## rfkill

```bash
rfkill --output ID,TYPE
rfkill block all
rfkill unblock wlan
rfkill block bluetooth uwb wimax wwan gps fm nfc
```

## Pairing a Bluetooth Keyboard

When the taskbar pairing icon isn't working:

`sudo bluetoothctla`

```bash
agent on
default agent
scan on
# Find the device you are looking for
scan off
trust <<INSERT MAC ADDRESS OF DEVICE>>
connect <<INSERT MAC ADDRESS OF DEVICE>>
# If its a keyboard it should come back with 6 digits to type into the keyboard. Type them and press enter
```

from: <http://wiki.sunfounder.cc/index.php?title=Connecting_Raspberry_Pi_with_the_Bluetooth_keyboard#:~:text=Switch%20on%20the%20keyboard%20and,%5Bbluetooth%5D%23%20scan%20off>

Some extra Commands inside bluetoothctl to help:\
`remove <<INSERT MAC ADDRESS OF DEVICE>>`: removes device from list. This should be tried before all others. Ideally either before or after `trust`\
`pair <<INSERT MAC ADDRESS OF DEVICE>>`: shouldn't be needed for keyboard and mouse but may be.\
`info <<INSERT MAC ADDRESS OF DEVICE>>`: show info about the device.\
`power off`: turn the bluetooth controlled off (this isn't rfkill)

More commends: <https://manpages.debian.org/unstable/bluez/bluetoothctl.1.en.html>

## Tools

[Raspberry Pi SD Card Image Manager](https://github.com/gitbls/sdm)\
[Pi-Gen](https://github.com/RPi-Distro/pi-gen): Tool used to create the official Raspberry Pi OS images (can also create custom images)
