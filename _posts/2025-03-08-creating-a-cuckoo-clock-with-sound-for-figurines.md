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
lastmod: 2025-03-10T11:56:40.758Z
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
  * [Parts under consieration](#parts-under-consieration)
* [Stats](#stats)
* [Drawning](#drawning)
* [Summary](#summary)
<!--- cSpell:enable --->

## TL;DR

## Intro

## Ideas

Imagine a Warhammer Cuckoo Clock that plays a sound on the hour.

### Functions

* Starting with a 4 Digit LCD 7 Segment Display, but may move to a analoge clock
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

![Funkpopstand](/assets/images/VarietyPopStandBases10-Pack-hi-res.png)

### Parts under consieration

* <https://au.rs-online.com/web/p/lcd-monochrome-displays/1850193?gb=s>
* <https://au.element14.com/c/automation-process-control/panel-displays-instrumentation/panel-display-technology/panel-displays?rd=lcd+display>
* <https://www.adafruit.com/product/815>
* <https://www.aliexpress.com/item/1005006857502103.html> 4 bit 0.8" Red display
* <https://www.robotgear.com.au/Product.aspx/Details/2082-7-Segment-Display-20mm-Red>
* <https://www.robotgear.com.au/Product.aspx/Details/2096-SparkFun-7-Segment-Serial-Display-Red> - has ATMega328 included to control display
* <https://www.jaycar.com.au/sealed-abs-enclosure-240-x-160-x-90mm/p/HB6134>

## Stats

* Average Funko Pop Pop Vynal Height: 3.75 Inches = 9.525cm
* Width = 2.5 inches (assumption from internet) = 6.35cm
* Average Weight = 280-340 grams

## Drawning

![Clock](/assets/images/clock1-with%20Plate.drawio.png)

## Summary
