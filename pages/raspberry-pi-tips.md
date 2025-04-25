---
title: Raspberry Pi Tips
description: Tips, tricks and things to remember for the PI.
published: true
categories:
    - Tech
type: pages
layout: pages
date: 2025-03-02T12:22:10.320Z
lastmod: 2025-04-25T05:42:34.681Z
tags:
    - RaspberryPi
    - Tips
    - Linux
isdraft: true
fmContentType: pages
mermaid: false
preview: ""
keywords:
    - Raspberry Pi
---

<!--- cSpell:disable --->
* [Documentation](#documentation)
* [Determine which Pi model you have from the command line](#determine-which-pi-model-you-have-from-the-command-line)
* [Differences between RaspberryPi OS Editions](#differences-between-raspberrypi-os-editions)
  * [Automount](#automount)
  * [Packages for common file system support](#packages-for-common-file-system-support)
* [Raspberry Pi Imager](#raspberry-pi-imager)
  * [Raspberry Pi Imager Custom Settings](#raspberry-pi-imager-custom-settings)
  * [Raspberry Pi bootloader changes](#raspberry-pi-bootloader-changes)
* [On First Boot after new image](#on-first-boot-after-new-image)
* [Setting a static IP on a Pi using Bookworm](#setting-a-static-ip-on-a-pi-using-bookworm)
  * [Use a DHCP Reservation](#use-a-dhcp-reservation)
  * [Network Manager](#network-manager)
  * [/etc/network/interfaces](#etcnetworkinterfaces)
* [full-upgrade](#full-upgrade)
* [Firmware Upgrade](#firmware-upgrade)
* [raspi-config non-interactive](#raspi-config-non-interactive)
* [Read only SD Card](#read-only-sd-card)
* [config.txt](#configtxt)
* [cmdline.txt](#cmdlinetxt)
* [Controlling a Raspberry Pi Fan](#controlling-a-raspberry-pi-fan)
  * [Checking settings](#checking-settings)
  * [Modifying RPM Config](#modifying-rpm-config)
* [vcgencmd](#vcgencmd)
* [vclog](#vclog)
* [rfkill](#rfkill)
* [Pairing a Bluetooth Keyboard](#pairing-a-bluetooth-keyboard)
* [Sound](#sound)
* [XScreensaver](#xscreensaver)
* [Tools](#tools)
* [Misc References](#misc-references)
<!--- cSpell:enable --->

## Documentation

<https://www.raspberrypi.com/documentation/>

<!--
Reference or tip?
-->

## Determine which Pi model you have from the command line

`cat /sys/firmware/devicetree/base/model`: Example: `Raspberry Pi 4 Model B Rev 1.1`\
`cat /proc/device-tree/model`: Example: `Raspberry Pi 3 Model B Plus Rev 1.3`\
`pinout`: Gives a visual representation of the Raspberry Pi Pins but also, gives the model number and revision.
`cat /proc/cpuinfo`: Gives CPU Info. You can then check some of the information again <https://elinux.org/RPi_Hardware>

> [!NOTE] No lshw
> seems Raspberry Pi OS doesn't have lshw installed

## Differences between RaspberryPi OS Editions

<https://forums.raspberrypi.com/viewtopic.php?t=339721>

### Automount

Raspberry Pi OS Lite does **not** automount removable media unlike the full edition.

From [https://pimylifeup.com/raspberry-pi-mount-usb-drive/](https://pimylifeup.com/raspberry-pi-mount-usb-drive/#:~:text=It%E2%80%99s%20important%20to%20know%20that%20Raspberry%20Pi%20OS%20lite%20currently%20does%20not%20automatically%20mount%20your%20drives.%20So%20you%20will%20need%20to%20either%20set%20it%20up%20manually%20or%20install%20the%20software%20package%20to%20have%20it%20automatically%20mount.)

> *"It's important to know that Raspberry Pi OS lite currently does not automatically mount your drives. So you will need to either set it up manually or install the software package to have it automatically mount."*

Solutions:

* udiskie, manually started as a deamon: <https://github.com/coldfix/udiskie>
  > [!IMPORTANT] udiskie may need a polkit config
  > For udiskie to run as pi, you may need to follow [these](https://github.com/coldfix/udiskie/wiki/Permissions) polkit instructions

* udev rules: <https://blog.jasonantman.com/2009/11/running-a-script-on-usb-drive-insertion/>
* autofs (maybe - can't quickly find solid answer on if it automounts?)
* fstab (note if storage is not attached at raspberrypi bootup, it add an extra 90 seconds to timeout): [Automatically mount a storage device - Raspberry Pi Documentation](https://www.raspberrypi.com/documentation/computers/configuration.html#automatically-mount-a-storage-device)

See also [External Storage - Official Raspberry Pi Documentation](https://www.raspberrypi.com/documentation/computers/configuration.html#external-storage)

### Packages for common file system support

NTFS: `sudo apt install ntfs-3g`\
See [NTFS on the Raspberry Pi](https://pimylifeup.com/raspberry-pi-ntfs/) for more details. (note site has too many ads)

exFAT:\
`sudo apt install exfat-fuse`\
`sudo apt install exfat-utils`\
See [exFAT on the Raspberry Pi](https://pimylifeup.com/raspberry-pi-exfat/) for more details. (note site has too many ads)

## Raspberry Pi Imager

### Raspberry Pi Imager Custom Settings

Pre-defined os settings:

On RPiOS it is at: `~/.config/Raspberry Pi/Imager.conf`
On windows it might be in the registry at: `HKCU\Software\Raspberry Pi\Imager`

From <https://forums.raspberrypi.com/viewtopic.php?t=339566>

### Raspberry Pi bootloader changes

If you want to change your boot order or the bootloader you need to use Raspberry Pi Imager. See [Update the bootloader](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#bootloader_update_stable)

For bootloader confiuguration changes see [Update the bootloader configuraiton](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#update-the-bootloader-configuration)

`sudo rpi-eeprom-update` will show you the current and available versions, and the current policy. You may need to reconfigure it to see latest using instructions [Update the bootloader configuraiton](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#update-the-bootloader-configuration)

`ls -la /usr/lib/firmware/raspberrypi/bootloader-2711/default`: Show default firmware versions already available on current Pi.\
`ls -la /usr/lib/firmware/raspberrypi/bootloader-2711/latest/`: Show latest version of firwmare downloaded.\
`less /usr/lib/firmware/raspberrypi/bootloader-2711/release-notes.md`: Release notes of versions.

## On First Boot after new image

After Raspberry Pi Imager is complete but before first boot, the [`cmdline.txt`](#cmdlinetxt) file has something like this in 2022:

```text
console=serial0,115200 console=tty1 root=PARTUUID=067e19d7-02 rootfstype=ext4 elevator=deadline fsck.repair=yes rootwait quiet init=/usr/lib/raspi-config/init_resize.sh
```

The `/usr/lib/raspi-config/init_resize.sh` runs on first run and at the end modifies `cmdline.txt` so it doesn't run again. From: <https://gijs-de-jong.nl/posts/raspberry-pi-file-system-resize-on-first-boot/>, specifically: <https://gijs-de-jong.nl/posts/raspberry-pi-file-system-resize-on-first-boot/#:~:text=How%20the%20automatic%20file%20system%20expansion%20is%20implemented>

Here is one from 2025 with Bookworm:

```text
console=serial0,115200 console=tty1 root=PARTUUID=067e19d7-02 rootfstype=ext4 fsck.repair=yes rootwait quiet init=/usr/lib/raspberrypi-sys-mods/firstboot cfg80211.ieee80211_regdom=US systemd.run=/boot/firstrun.sh systemd.run_success_action=reboot systemd.unit=kernel-command-line.target
```

> [!WARNING] WIP
> The below first run order list is still very much a **Work In Progress**

So the order for bookworm seems to be:

1. <https://github.com/RPi-Distro/raspberrypi-sys-mods/blob/bookworm/usr/lib/raspberrypi-sys-mods/firstboot>
   1. [`Modify /boot/firmware/cmdline.txt` so firstboot doesn't run again.](https://github.com/RPi-Distro/raspberrypi-sys-mods/blob/93ab67567a088b6adbb0a8ec9d09655af52c14e4/usr/lib/raspberrypi-sys-mods/firstboot#L112)
   2. [call](https://github.com/RPi-Distro/raspberrypi-sys-mods/blob/93ab67567a088b6adbb0a8ec9d09655af52c14e4/usr/lib/raspberrypi-sys-mods/firstboot#L121) the [main function](https://github.com/RPi-Distro/raspberrypi-sys-mods/blob/93ab67567a088b6adbb0a8ec9d09655af52c14e4/usr/lib/raspberrypi-sys-mods/firstboot#L80)
   3. Generate SSH Keys by mounting the root partition and then running [/usr/lib/raspberrypi-sys-mods/regenerate_ssh_host_keys](https://github.com/RPi-Distro/raspberrypi-sys-mods/blob/bookworm/usr/lib/raspberrypi-sys-mods/regenerate_ssh_host_keys)
   4. If `/boot/firmware/custom.toml` is found, call apply_custom function, telling it to use `/boot/firmware/custom.toml`
      1. Run `python3 -c "import toml"`
      2. If it doesn't fail run [`/usr/lib/raspberrypi-sys-mods/init_config` supplying the toml firle as an argument](https://github.com/RPi-Distro/raspberrypi-sys-mods/blob/93ab67567a088b6adbb0a8ec9d09655af52c14e4/usr/lib/raspberrypi-sys-mods/firstboot#L65).
         1. **TBA**
   5. Fix PartUUID
   6. Reboot if there is no failure reason determined.
2. `systemd.run=/boot/firstrun.sh` - this is dynamically created by the Raspberry Pi Imager depending on the configration you set (see [Raspberry Pi Imager Custom Settings](#raspberry-pi-imager-custom-settings)). See below for First Run Github links

firstrun.sh generation links from github:

* <https://github.com/raspberrypi/rpi-imager/blob/qml/src/downloadthread.cpp>
* <https://github.com/raspberrypi/rpi-imager/blob/qml/src/OptionsPopup.qml>

## Setting a static IP on a Pi using Bookworm

### Use a DHCP Reservation

Crappy but seems official: <https://www.raspberrypi.com/documentation/computers/configuration.html#assign-a-static-ip-address>

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

Using NMCLI as a hotspot:\
From <https://www.raspberrypi.com/documentation/computers/configuration.html#host-a-wireless-network-from-your-raspberry-pi>

```bash
# enable hotspot
sudo nmcli device wifi hotspot ssid <example-network-name> password <example-password>

# disable hotspot
## To disable the hotspot network and resume use of your Pi as a wireless client, run the following command:
sudo nmcli device disconnect wlan0

## After disabling the network, run the following command to reconnect to another Wi-Fi network:
sudo nmcli device up wlan0
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

## full-upgrade

From: <https://www.raspberrypi.com/documentation/computers/os.html#manage-software-packages-with-apt>

> [!TIP]
> Unlike Debian, Raspberry Pi OS is under continual development. As a result, package dependencies sometimes change, so you should always use `full-upgrade` instead of the standard `upgrade`.

full-update commands:

```bash
sudo apt update # -y
sudo apt full-upgrade # -y
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

<!--
More a reference than tip
-->

RaspberryPi BIOS Settings

For bookworm onwards its located in: `/boot/firmware/config.txt`\
Before bookworm it was in `/boot/config.txt`

<https://www.raspberrypi.com/documentation/computers/config_txt.html#what-is-config-txt>

<https://elinux.org/RPiconfig>

Note that if you want to change your boot order or the bootloader you need to use Raspberry Pi Imager. See [Raspberry Pi Imager](#raspberry-pi-imager).

## cmdline.txt

<!--
More a reference than tip
-->

The Linux kernel accepts a collection of command line parameters during boot. On the Raspberry Pi, this command line is defined in a file in the boot partition, called cmdline.txt. You can edit this text file with any text editor.

For bookworm onwards its located in: `/boot/firmware/cmdline.txt`\
Before bookworm it was in `/boot/cmdline.txt`

<https://www.raspberrypi.com/documentation/computers/configuration.html#kernel-command-line-cmdline-txt>\
<https://elinux.org/RPi_cmdline.txt>\
<https://www.kernel.org/doc/html/latest/admin-guide/kernel-parameters.html> - lots of them

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

<!-- markdownlint-disable MD029 -->
7. Press 'Control+X' on your keyboard to exit
8. Press 'Y' on your keyboard to agree to overwriting the file
9. Press 'Enter' to confirm
10. This will close the nano text editor
11. reboot your pi using the command
12. sudo reboot
13. The fan should work with your new settings now
<!-- markdownlint-enable MD029 -->

## vcgencmd

`vcgencmd measure_temp`: Get temp of Pi\
`vcgencmd get_config <command>`: show config.txt settings. see <https://www.raspberrypi.com/documentation/computers/config_txt.html#what-is-config-txt>

* `vcgencmd get_config <config>` - lists a specific config value. E.g. vcgencmd get_config arm_freq\
* `vcgencmd get_config int` - lists all the integer config options that are set (non-zero)\
* `vcgencmd get_config str` - lists all the string config options that are set (non-null)\

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

## Sound

`alsactl`: advanced controls for ALSA soundcard driver. <https://linux.die.net/man/1/alsactl>:\

* `sudo alsactl store`: stores current settings in `/var/lib/alsa/asound.state`
* `alsactl --file ~/.config/asound.state store`
* `alsactl --file ~/.config/asound.state restore`
* More commands from: <https://askubuntu.com/questions/50067/how-to-save-alsamixer-settings>
  > 1. `sudo alsamixer`
  > 2. do not exit alsamixer
  > 3. in a new terminal `sudo alsactl store`
* `sudo alsactl dump-state`
* `sudo alsactl dump-cfg`

`aplay -l`: List all soundcards and digital audio devices via ALSA. <https://linux.die.net/man/1/aplay>\
`aplay -L`: List all PCMs defined\
`aplay -D plughw:CARD=UACDemoV10 /usr/share/sounds/alsa/Front_Center.wav`: play this sound on this PCM device
`alsamixer`: Interactive TUI mixer for setting volume levels. <https://linux.die.net/man/1/alsamixer>\
`amixer`: cmdline mixer for ALSA. <https://linux.die.net/man/1/amixer>:\

* `amixer -c <CARDNAME> info`: show the info about a mixer device for CARDNAME. CARDNAME can be a friendly name like HDMI or a USB Speaker device name, or a card number.
* `amixer -c <CARDNAME> scontrols`: Show me the simple controls for CARDNAME.
* `amixer -c <CARDNAME> scontents`: show me the simple controls and some more details about them for CARDNAME
* `amixer -c <CARDNAME> get <SCONTROL>`: get the current simple control value (`get` is an alias `sget`)
* `amixer -c <CARDNAME> set <SCONTROL> <PARAMETER>`: set the current simple control parameter. (`set` is an alias of `sset`):
  > Sets the simple mixer control contents. The parameter can be the volume either as a percentage from 0% to 100% with % suffix, a dB gain with *dB* suffix (like -12.5dB), or an exact hardware value. The dB gain can be used only for the mixer elements with available dB information. When plus(+) or minus(-) letter is appended after volume value, the volume is incremented or decremented from the current value, respectively.
  >
  > The parameters *cap, nocap, mute, unmute, toggle* are used to change capture (recording) and muting for the group specified.
  >
  > The optional modifiers can be put as extra parameters to specify the stream direction or channels to apply. The modifiers *playback* and *capture* specify the stream, and the modifiers *front, rear, center, woofer* are used to specify channels to be changed.
  >
  > A simple mixer control must be specified. Only one device can be controlled at a time.
* `amixer -c <CARDNAME> controls`: show me the controls for CARDNAME. This will show you the numid's you can use for this card.
* `amixer -c <CARDNAME> contents`: show me the controls and some more details about them for CARDNAME. This will show you the numids for this card and their values and how they work.
* `amixer -c <CARDNAME> cget <CONTROL>`: get the current control value
* `amixer -c <CARDNAME> cset <CONTROL> <PARAMETER>`: set the current control parameter\

  Examples from man page:
  > `amixer -c 1 sset Line,0 80%,40% unmute cap`: will set the second soundcard's left line input volume to 80% and right line input to 40%, unmute it, and select it as a source for capture (recording).\
  > `amixer -c 1 -- sset Master playback -20dB`: will set the master volume of the second card to -20dB. If the master has multiple channels, all channels are set to the same value.\
  > `amixer -c 1 set PCM 2dB+`: will increase the PCM volume of the second card with 2dB. When both playback and capture volumes exist, this is applied to both volumes.\
  > `amixer -c 2 cset iface=MIXER,name='Line Playback Volume",index=1 40%`: will set the third soundcard's second line playback volume(s) to 40%\
  > `amixer -c 2 cset numid=34 40%`: will set the 34th soundcard element to 40%

  My examples:

  ```bash
  sudo amixer -c Ego set ummute
  sudo amixer -c Ego set PCM 75%
  sudo amixer -c Ego set PCM unmute playback 50%

  sudo amixer -c Ego cset numid=5 50%,50%
  sudo amixer -c Ego cset numid=5 12,12
   ```

`sudo speaker-test -c2 -D <devicename>`: test the speakers. May need sudo. <https://linux.die.net/man/1/speaker-test>

`~/.asoundrc` file syntax: <https://www.alsa-project.org/wiki/Asoundrc>

`ls /proc/asound/cards`\
`ls /proc/asound/card2`

## XScreensaver

Activate now: `xscreensaver-command -activate`

## Tools

[Raspberry Pi SD Card Image Manager](https://github.com/gitbls/sdm)\
[Pi-Gen](https://github.com/RPi-Distro/pi-gen): Tool used to create the official Raspberry Pi OS images (can also create custom images)

## Misc References

[Embedded Linux Wiki](https://elinux.org/Main_Page)\
[STICKY: Using fstab A Beginner's Guide](https://forums.raspberrypi.com/viewtopic.php?t=302752)\
[Raspberry Pi Pinout Guide](https://pinout.xyz/) - interactive reference to the Raspberry Pi GPIO pins, and a guide to the Raspberry Pi's GPIO interfaces - also see the `pinout` command.\
[RPi GPIO Python Module Info](https://sourceforge.net/p/raspberry-gpio-python/wiki/Home/)\
[Official Documentation](#documentation)
