---
title: Windows Commands
description: Windows Commands to remember
categories:
    - Tech
type: pages
layout: pages
published: true
date: 2024-12-31T11:24:00
lastmod: 2025-04-21T23:31:45.879Z
tags:
    - Commands
    - References
    - Windows
isdraft: true
keywords:
    - Commands
    - Windows
---


<!--- cSpell:disable --->
* [Query Commands](#query-commands)
* [Uptime](#uptime)
* [User Profile Management](#user-profile-management)
* [Bitlocker Status](#bitlocker-status)
* [Unformatted to add above](#unformatted-to-add-above)
* [Additional Resources](#additional-resources)
<!--- cSpell:enable --->

## Query Commands

query user - show user sessions

```bat
# query user [<username> | <sessionname> | <sessionID>] [/server:<servername>]
query user
query user /server:remotemachine
quser
quser /server:remotemachine
```

query session - show user sessions

```bat
# query session [<sessionname> | <username> | <sessionID>] [/server:<servername>] [/mode] [/flow] [/connect] [/counter]
query session john.doe
qwinsta /server:servername
```

query session - show user processes

```bat
# query process [*|<processID>|<username>|<sessionname>|/id:<nn>|<programname>] [/server:<servername>]
query process john.doe
qprocess /server:servername
```

[query commands - Microsoft Learn](https://learn.microsoft.com/en-au/windows-server/administration/windows-commands/query)

[Common errors with query commands - How to Remotely Log Off User with Command Line? – TheITBros](https://theitbros.com/remotely-log-off-user-with-cmd/#:~:text=Possible%20errors%20when%20executing%20the%20logoff%20command%3A)

## Uptime

Find Uptime from System Info

> [!NOTE] NOTE
> The below records the time system last registered a **full** boot up.
> If you have FastBoot enabled, it doesn't reset.
> Task Manager shows you the 'duration' of your uptime from this date, not the actual duration - ie hibernation doesn't stop this

Get Uptime from Command Prompt

```bat
systeminfo | find "System Boot Time"
```

Get Uptime from CIM via Powershell

```powershell
Get-CimInstance -ClassName Win32_OperatingSystem | Select-Object LastBootUpTime
```

## User Profile Management

From an administrative command prompt:

```bat
rundll32.exe sysdm.cpl,EditUserProfiles
rem OR

SystemPropertiesAdvanced.exe
rem from run (will prompt for admin)
```

## Bitlocker Status

Check Bitlocker Status

```bat
manage-bde -status
```

## Unformatted to add above

TBC

## Additional Resources

[Command-line reference A-Z - Windows commands - Microsoft Learn](https://learn.microsoft.com/en-au/windows-server/administration/windows-commands/windows-commands#command-line-reference-a-z)
