---
title: Raspberry Pi Tips
description: Tips and tricks for the PI.
published: true
categories:
    - Tech
type: pages
layout: pages
date: 2025-03-02T12:22:10.320Z
lastmod: 2025-03-04T04:35:15.822Z
tags:
    - Tips
    - Raspberry Pi
draft: true
fmContentType: pages
mermaid: "false"
preview: ""
---

<!--- cSpell:disable --->
* [vcgencmd](#vcgencmd)
* [Controlling a Raspberry Pi Fan](#controlling-a-raspberry-pi-fan)
  * [Checking settings](#checking-settings)
  * [Modifying RPM Config](#modifying-rpm-config)
* [rfkill](#rfkill)
* [Pairing a Bluetooth Keyboard](#pairing-a-bluetooth-keyboard)
<!--- cSpell:enable --->

## vcgencmd

`vcgencmd measure_temp`: Get temp of Pi\
`vcgencmd commands`: show other vcgencmd commands

More info:

* <https://github.com/raspberrypi/documentation/blob/bd97e2f9aaf9f41ae36e6c8b54083ae6573d9d28/raspbian/applications/vcgencmd.md>
* <https://github.com/raspberrypi/documentation/blob/bd97e2f9aaf9f41ae36e6c8b54083ae6573d9d28/raspbian/applications/vcdbg.md>

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
