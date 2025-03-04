---
title: Raspberry Pi Tips
description: Tips and tricks for the PI.
published: false
categories:
    - Tech
type: pages
layout: pages
date: 2025-03-02T12:22:10.320Z
lastmod: 2025-03-02T12:48:25.451Z
tags:
    - Tips
    - Raspberry Pi
draft: true
fmContentType: pages
mermaid: "false"
preview: ""
---

<!--- cSpell:disable --->
* [Getting the Temp](#getting-the-temp)
* [Controlling a Raspberry Pi Fan](#controlling-a-raspberry-pi-fan)
* [rfkill](#rfkill)
* [Pairing a Bluetooth Keyboard](#pairing-a-bluetooth-keyboard)
<!--- cSpell:enable --->

## Getting the Temp

* [ ] add in vcgencmd commands

## Controlling a Raspberry Pi Fan

* [ ] insert link to article

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

from: http://wiki.sunfounder.cc/index.php?title=Connecting_Raspberry_Pi_with_the_Bluetooth_keyboard#:~:text=Switch%20on%20the%20keyboard%20and,%5Bbluetooth%5D%23%20scan%20off

Some Exta Commands inside bluetoothctl to help:
`remove <<INSERT MAC ADDRESS OF DEVICE>>`: removes device from list. This should be tried before all others. Ideally either before or after `trust`
`pair <<INSERT MAC ADDRESS OF DEVICE>>`: shouldn't be needed for keyboard and mouse but may be.
`info <<INSERT MAC ADDRESS OF DEVICE>>`: show info about the device.
`power off`: turn the bluetooth controlled off (this isn't rfkill)
