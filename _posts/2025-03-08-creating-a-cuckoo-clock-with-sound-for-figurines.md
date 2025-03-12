---
title: Creating a Cuckoo Clock with Sound for Figurines
description: Using XXX
published: false
categories:
    - NotTech
    - Tech
type: posts
layout: posts
date: 2025-03-08T12:56:35.139Z
lastmod: 2025-03-12T07:54:35.534Z
tags:
    - Project
    - Arduino
isdraft: true
fmContentType: posts
mermaid: false
preview: ""
---

<!--- cSpell:disable --->
* [TL;DR](#tldr)
* [Intro](#intro)
* [Ideas](#ideas)
  * [Functions](#functions)
  * [Ideation and Thoughts](#ideation-and-thoughts)
* [Stats](#stats)
* [Drawing](#drawing)
* [Actuator](#actuator)
  * [Parts under consideration](#parts-under-consideration)
* [Reference Material](#reference-material)
* [Summary](#summary)
<!--- cSpell:enable --->

## TL;DR

## Intro

## Ideas

Imagine a Warhammer Cuckoo Clock that plays a sound on the hour.

### Functions

* Starting with a 4 Digit LCD 7 Segment Display, but may move to a analog clock
* Can be muted
* Muting resets each day
* Web interface or google interface for muting
* Doesn't ring until at least 8 AM if not 9
* Rings every hour until 11
* Plays sound on the hour between 8 AM and 11 PM IF the light is on
* Sound can be changed
* Moves Motor on the hour
* Light sensor detects when light is on.
* Advanced: Motor drivers plate with notch
* Advanced: Stub is where 3d models attach.
* Advanced: gets time from NTP
* Advanced: Updates for DST
* Advanced: LCD Screen with date
* Advanced: Clock can tell which model is present (NFC) OR can have multiple models and randomly chooses one
* Note: 3D Models are static, not moving

### Ideation and Thoughts

* <https://www.instructables.com/I-Cuckoo-Clock-Using-an-Arduino-Stepper-Motor-to-R/>
* <https://www.instructables.com/Cuckoo-Clock-arduino>
* We may need an RTC component
* <https://www.reddit.com/r/AskElectronics/comments/drngnh/large_7_segment_4_digit_display/>
* Ideally could support up to a funko pop
  * <https://funko.com/variety-pop-stand-bases-10-pack/51033.html>
* <https://www.reddit.com/r/raspberry_pi/comments/4ztkza/wanting_to_learn_raspberry_pi_by_making_an_analog>
* <https://learn.adafruit.com/adafruit-16-channel-servo-driver-with-raspberry-pi/configuring-your-pi-for-i2c?view=all>
* <https://www.aliexpress.com/w/wholesale-clock-lcd-display.html?spm=a2g0o.productlist.auto_suggest.1.4c8357c7qshx7Q>
* <https://www.instructables.com/Arduino-and-MAX7219-8-Digit-7-Segment-BCD-Counter/>
* <https://kitstop.com.au/?s=4+digit+7+segment>
* <https://kitstop.com.au/product-category/led-7-segment/>
* <https://core-electronics.com.au/concentric-lact4-12v-20-linear-actuator-4-stroke-12v-0-5-s.html>
* If using PI
  * Consider SDCard in read only mode - but how can it then do Update
  * Sounds come from plugged in usb drive
  * Consider: <https://core-electronics.com.au/guides/ups-with-raspberry-pi-4/> to keep the clock going when no power
  * <https://raspi.tv/2015/how-to-drive-a-7-segment-display-directly-on-raspberry-pi-in-python>
    * <https://rasp.io/breakout/>

![Funkpopstand](/assets/images/VarietyPopStandBases10-Pack-hi-res.png)

## Stats

* Average Funko Pop Pop Vinyl Height: 3.75 Inches = 9.525cm
* Width = 2.5 inches (assumption from internet) = 6.35cm
* Depth = 2.5 inches (assumption from internet) = 6.35cm
* Average Weight = 280-340 grams

## Drawing

![Clock](/assets/images/clock1-with%20Plate.drawio.png)

## Actuator

After reading parts of [Servos, Steppers or Solenoids? | Choosing an Actuator to Move Your Project](https://core-electronics.com.au/guides/servos-steppers-or-solenoids-choosing-an-actuator-to-move-your-project) and watching part of <https://www.youtube.com/watch?v=s0ABQYxSVdg&t=1s> I think we are after a <ins>*Linear Actuator*</ins> with the following attributes:

* Stroke length: 8.5CM ~ 10CM
* Rated Voltage: Something that can also run a pi (can't run this off a PI)
* Lower Gear Ratio (we need it to be fast but it doesn't have to move much)
* Able to (move?) 0.5nm

### Parts under consideration

* <https://au.rs-online.com/web/p/lcd-monochrome-displays/1850193?gb=s>
* <https://au.element14.com/c/automation-process-control/panel-displays-instrumentation/panel-display-technology/panel-displays?rd=lcd+display>
* <https://www.adafruit.com/product/815>
  * More in <https://www.adafruit.com/category/37_103>
* <https://www.aliexpress.com/item/1005006857502103.html> 4 bit 0.8" Red display
* <https://www.robotgear.com.au/Product.aspx/Details/2082-7-Segment-Display-20mm-Red>
* <https://www.robotgear.com.au/Product.aspx/Details/2096-SparkFun-7-Segment-Serial-Display-Red> - has ATMega328 included to control display
* <https://www.jaycar.com.au/sealed-abs-enclosure-240-x-160-x-90mm/p/HB6134>
* <https://www.digikey.com.au/en/products/detail/actuonix-motion-devices-inc/P8-100-165-12-S/24474910?gQT=1> / <https://www.actuonix.com/assets/images/datasheets/Actuonix%20P8%20Datasheet.pdf>
* <https://www.digikey.com.au/en/products/filter/electric-actuators-cylinders/1157?s=N4IgjCBcoKwMwWiAxlAZgQwDYGcCmANCAPZQDa4A7AJwyVwgC6RADgC5QgDKbATgJYA7AOYgAvkQC0MKKFSRMuQiXIgAHAAYALEzESQANlkh%2BAE06SwGiKw6QQIImwCeLPJww5UeoA>
* [2495-L12-100-50-6-S-ND](https://www.digikey.com.au/en/products/detail/actuonix-motion-devices-inc/L12-100-50-6-S/12317300)
  * 100MM Stroke length
  * Unit length 152mm
  * 25mm/s speed
* [2495-P8-100-49-3-ST-ND](https://www.digikey.com.au/en/products/detail/actuonix-motion-devices-inc/P8-100-49-3-ST/15997551)
  * 100mm stroke length
  * unit length 135mm
  * The speed of travel is determined by the step frequency, and maximum force by the current applied. Looking at data sheet graph we should be ok.
  * 4.2VDC
  * <https://www.actuonix.com/p8-100-49-3-st>
  * <https://www.actuonix.com/assets/images/datasheets/ActuonixP8StepperDatasheet.pdf>
  * Note: Tic T825 USB Multi-Interface Stepper Motor Controller to control, if not PI i2C?
* <https://littlebirdelectronics.com.au/collections/linear-actuators/products/6v-electric-push-rod-100mm-128n> / <https://www.dfrobot.com/product-2369.html> / <https://core-electronics.com.au/6v-electric-push-rod-100mm-128n.html>
* L298N dual H-Bridge motor driver
  * <https://howtomechatronics.com/tutorials/arduino/arduino-dc-motor-control-tutorial-l298n-pwm-h-bridge/#h-l298n-driver>

## Reference Material

* <https://newbiely.com/tutorials/raspberry-pi/raspberry-pi-actuator> - good guide from the looks of it
* <https://github.com/ericescobar/Chicken_Door> - simple example that we can copy from
  * <https://github.com/ericescobar/Chicken_Door/blob/master/Electrical_Diagram.jpg>

## Summary
