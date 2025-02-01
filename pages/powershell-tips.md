---
title: PowerShell Tips
description: ""
published: false
categories:
    - Tech
type: pages
layout: pages
date: 2025-02-01T01:47:46.278Z
lastmod: 2025-02-01T01:59:23.701Z
tags:
    - Tips
    - PowerShell
draft: true
fmContentType: pages
preview: ""
---

<!--- cSpell:disable --->
* [Installing Modules](#installing-modules)
* [Quake Mode on startup](#quake-mode-on-startup)
* [Tools](#tools)
<!--- cSpell:enable --->

## Installing Modules

Unless youare working on a server, a PAW, with a lot of different local profiles, or with an automation solution, strongly consier always installing modules to CurrentUser scope. Its easier to maintain, update, etc

## Quake Mode on startup

Use a shell/terminal emulater that you can start on startup and that supports what is often called quake mode. [cmder](https://cmder.app/) and [Windows Terminal](https://aka.ms/terminal) support quake mode and it shouldn't be too hard tell windows to launch them on startup.

The idea is that you will use a very quick keyboard shortcut (normally CTRL + ~) to bring up the shell and hide it (but not close it) again and often, so its quickly available for you. By reduicing the time to get to the shell and also your brain becoming more aware that its quicker to get to, you will start using it more often, thus getting you more experience.

## Tools

**<https://cmder.app/>**: Nice terminal emulater that has a bunch of great inclues.
<https://aka.ms/terminal> / <https://github.com/microsoft/terminal> - i'm not totally on the Windows Terminal Bandagon yet but its not shit.

Also check [Misc Tools](misc-tools.md)
