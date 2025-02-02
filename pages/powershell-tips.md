---
title: PowerShell Tips
description: ""
published: false
categories:
    - Tech
type: pages
layout: pages
date: 2025-02-01T01:47:46.278Z
lastmod: 2025-02-02T03:15:46.636Z
tags:
    - Tips
    - PowerShell
draft: true
fmContentType: pages
preview: ""
---

<!--- cSpell:disable --->
* [Installing Modules](#installing-modules)
* [Terminal Emulator Quake Mode on startup](#terminal-emulator-quake-mode-on-startup)
* [File Locations of PS Components](#file-locations-of-ps-components)
  * [Modules](#modules)
* [Authentication Methods](#authentication-methods)
  * [Using Single Browser with Multple profiles](#using-single-browser-with-multple-profiles)
* [Tools](#tools)
<!--- cSpell:enable --->

## Installing Modules

Unless you're working on a server, a PAW, with a lot of different local profiles, or with an automation solution, strongly consider always installing modules to CurrentUser scope. Its easier to maintain, update, etc

## Terminal Emulator Quake Mode on startup

Use a shell/terminal emulator that you can start on startup and that supports what is often called quake mode. [cmder](https://cmder.app/) and [Windows Terminal](https://aka.ms/terminal) support quake mode and it shouldn't be too hard tell windows to launch them on startup.

The idea is that you will use a very quick keyboard shortcut (normally CTRL + ~) to bring up the shell and hide it (but not close it) again and often, so its quickly available for you. By reducing the time to get to the shell and also your brain becoming more aware that its quicker to get to, you will start using it more often, thus getting you more experience.

## File Locations of PS Components

### Modules

`C:\Program Files\WindowsPowerShell\Modules`: Windows PowerShell 5.1 Modules for all users
`C:\Users\user.name\OneDrive - Contoso\Documents\WindowsPowerShell\Modules`: Windows PowerShell 5.1 Modules for current user but you have OneDrive known Office folder move on. There are some hiccups and a little pain with this but its managable.

* [ ] Add PS7 paths

## Authentication Methods

`-DeviceLogin`: Really good if you access multiple tenants or have multiple accounts.

`-Interactive`

### Using Single Browser with Multple profiles

* [ ] Type up tip about moving tabs when using `-devicelogin`

## Tools

**<https://cmder.app/>**: Nice terminal emulater that has a bunch of great inclues.
<https://aka.ms/terminal> / <https://github.com/microsoft/terminal> - i'm not totally on the Windows Terminal Bandagon yet but its not shit.

Also check [Misc Tools](misc-tools.md)
