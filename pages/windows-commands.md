---
title: Windows Commands
description: Windows Commands to remember
categories: Reference Commands
---

[home](/) [up](./)

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

```bat
systeminfo | find “System Boot Time”
```

Get Uptime from CIM via Powershell

```bat
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