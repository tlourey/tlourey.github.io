---
title: A different answer to Byobu Function keys via PuTTY
description: An unexpected alternative to getting Byobu working with the function keys via PuTTY.
published: true
categories:
    - Tech
type: posts
layout: posts
date: 2025-10-11T01:57:34.454Z
lastmod: 2025-10-11T04:11:53.432Z
tags:
    - Tips
    - Tools
    - Windows
    - Linux
isdraft: true
fmContentType: posts
mermaid: false
preview: ""
keywords:
    - Byobu
    - PuTTY
---
<!--- cSpell:words Byobu -->
<!--- cSpell:ignore -->
<!--- cSpell:disable --->
* [TL;DR](#tldr)
* [Intro](#intro)
* [Summary](#summary)
* [Misc References on this site](#misc-references-on-this-site)
<!--- cSpell:enable --->

## TL;DR

* There is an old known issue around using Byobu via PuTTY. Mostly around the function keys not working as expected/needed with Byobu.
* Most common solution is to set *Keyboard --> Function Keys and Keypad* to `Xterm R6` and *Connections --> Data --> Terminal-type string* to `putty-256colour`
* It makes sense and seems to address the issue for most
* BUT NOT ME BABY! (Windows 10, Putty 0.81, Raspberry Pi 4, Raspberry OS Bookworm, Byobu using tmux backend).
* Mostly the issue was around creating spilt's.
* What fixed it was setting Terminal-type string to `xterm` and Keyboard --> Function Keys and Keypad to `Xterm 216+`
* Not sure what other issues it will cause me but it fixed the function keys not working issue without making it worse.

## Intro

This was a quick write up because, I stumbled upon this answer when the most common answers were not giving me love.

None of this makes sense? here's some background info if you need it:

* [Terminal Emulator](https://en.wikipedia.org/wiki/Terminal_emulator)
* [PuTTY](https://en.wikipedia.org/wiki/PuTTY)
* [Xterm](https://en.wikipedia.org/wiki/Xterm)
* [Byobu (software)](https://en.wikipedia.org/wiki/Byobu_(software))
* [byobu f2 function keys not working in putty - Google Search](https://www.google.com/search?q=byobu+f2+function+keys+not+working+in+putty)

**My bias'**:

* PuTTY is not my day to day (it's SecureCRT)
* Still have a lot of love for PuTTY and as soon as things get weird, PuTTY is where I go
* Have installed all the PuTTY tools via Microsoft Store (keeps them up to date)
* I am not Terminal Emulator setting expert but I get the main points of it and to some degree how we got here

**The problem**: When I was using Byobu via PuTTY I couldn't get the splits to respond to the default keys. Some things did work and others didn't. Tinkering let me to the very common solutions such as:

* set *Keyboard --> Function Keys and Keypad* to `Xterm R6`
* set *Connections --> Data --> Terminal-type string* to `putty-256colour`
* check version of PuTTY
* Look at some forks (KiTTY, etc)

The first two were the most common, but for me they didn't work. I decided on the old, try one at a time and got some mixed results. I'd also had some other issues in the past with some networking gear and terminal type of xterm so I decided to adjust bits and pieces until I tried:

* set *Connections --> Data --> Terminal-type string* to `xterm`
* set *Keyboard --> Function Keys and Keypad* to `Xterm 216+`

The terminal type wasn't a complete short in the dark as I'd had some success on unrelated efforts using the `xterm` value, but the Function key setting of `Xterm 216+` was just a "Why not give it a go" choice and I was surprised it got me there. I don't know much about Xterm 216+ but at this point I'm not complaining.

I'd still recommend checking the most common solution first, but if, like me, you still had some issues, maybe give this a try.

My gut tells me that there is still something else at play somewhere I can't pin point that may make this solution valid but I couldn't easily figure it out and wanted to share.

[![It works on my machine](/assets/images/it-works-on-my-machine.jpg)](/assets/images/it-works-on-my-machine.jpg)

## Summary

It works for me. It may work for you. There may be an underlying reason I can't see that makes it work, but its happened to me a few times over the years that i'm going with it.

The end.

## Misc References on this site

* [PuTTY Commands](../pages/putty-commands.md)
* [SSH Tips and Tricks](../pages/ssh-tips-and-tricks.md)
* [Bash Tips](../pages/bash-tips.md)
