---
title: PowerShell Tips
description: Tips and Tricks with PowerShell
published: true
categories:
    - Tech
type: pages
layout: pages
date: 2025-02-01T01:47:46.278Z
lastmod: 2025-03-17T02:11:08.138Z
tags:
    - Tips
    - PowerShell
isdraft: true
fmContentType: pages
preview: ""
---

<!--- cSpell:disable --->
* [Installing Modules](#installing-modules)
* [Terminal Emulator Quake Mode on startup](#terminal-emulator-quake-mode-on-startup)
* [Commands often forgotten](#commands-often-forgotten)
* [File Locations of PS Components](#file-locations-of-ps-components)
  * [Modules](#modules)
* [Authentication Methods](#authentication-methods)
  * [Using Single Browser with Multple profiles](#using-single-browser-with-multple-profiles)
* [Tools](#tools)
* [Traps](#traps)
<!--- cSpell:enable --->

## Installing Modules

Unless you're working on a server, a PAW, with a lot of different local profiles, or with an automation solution, strongly consider always installing modules to CurrentUser scope. Its easier to maintain, update, etc

```powershell
Install-Module <<MODULENAME>> -Scope CurrentUser
```

See [Module Management in PowerShell Commands](powershell-commands.md#module-management) for more commands.

## Terminal Emulator Quake Mode on startup

Use a shell/terminal emulator that you can start on startup and that supports what is often called quake mode. [cmder](https://cmder.app/) and [Windows Terminal](https://aka.ms/terminal) support quake mode and it shouldn't be too hard tell windows to launch them on startup.

The idea is that you will use a very quick keyboard shortcut (normally CTRL + ~) to bring up the shell and hide it (but not close it) again and often, so its quickly available for you. By reducing the time to get to the shell and also your brain becoming more aware that its quicker to get to, you will start using it more often, thus getting you more experience.

## Commands often forgotten

`Get-Content -Path c:\temp\my-log-file.log -wait`: like cat. using -wait makes it like tail -f: <https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-content#-wait>\
`Select-String`: kind of like grep (need to check if it does work like grep)\
`Out-GridView`: really cool wait view tables/rows. -passthru is also really awesome. You should read the help page in full esp the Notes stuff: <https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/out-gridview>

Also check [PowerShell Commands often forgotten](powershell-commands.md#commands-often-forgotten)

## File Locations of PS Components

### Modules

PowerShell 7:

* Modules installed in the CurrentUser scope:
  * On Windows, these modules are stored in $HOME\Documents\PowerShell\Modules. The specific location of the Documents folder varies by version of Windows and when you use folder redirection. Also, Microsoft OneDrive can change the location of your Documents folder. To verify the location of your Documents folder, run use the following command: [Environment]::GetFolderPath('MyDocuments').
  * On non-Windows systems, these modules are stored in the $HOME/.local/share/powershell/Modules folder.
* Modules installed in the AllUsers scope:
  * On Windows, these modules are stored in $env:ProgramFiles\PowerShell\Modules.
  * On non-Windows systems, these modules are stored in /usr/local/share/powershell/Modules.
* Modules that ship with PowerShell are stored in $PSHOME\Modules

<https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_psmodulepath?view=powershell-7.5>

Windows PowerShell 5.1:

* Modules installed in the CurrentUser scope are stored in `$HOME\Documents\WindowsPowerShell\Modules`.
* Modules installed in the AllUsers scope are stored in `$env:ProgramFiles\WindowsPowerShell\Modules`.
* Modules that ship with Windows PowerShell stored in `$PSHOME\Modules`, which is `$env:SystemRoot\System32\WindowsPowerShell\1.0\Modules`.
* `$HOME\OneDrive - Contoso\Documents\WindowsPowerShell\Modules`: Windows PowerShell 5.1 Modules for current user but you have OneDrive known Office folder move on. There are some hiccups and a little pain with this but its managable.\

<https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_psmodulepath?view=powershell-5.1>

## Authentication Methods

`-DeviceLogin`: Really good if you access multiple tenants or have multiple accounts.

`-Interactive`

### Using Single Browser with Multple profiles

* [ ] Type up tip about moving tabs when using `-devicelogin`

## Tools

**<https://cmder.app/>**: Nice terminal emulater that has a bunch of great inclues.
<https://aka.ms/terminal> / <https://github.com/microsoft/terminal> - i'm not totally on the Windows Terminal Bandagon yet but its not shit.

Also check [Misc Tools](misc-tools.md)

## Traps

<https://github.com/nightroman/PowerShellTraps>
