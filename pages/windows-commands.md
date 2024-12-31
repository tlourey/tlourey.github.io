---
title: Windows Commands
description: Windows Commands to remember
---

[home](/) [up](./)

## Query Commands

query user - show user sessions

```winbatch
# query user [<username> | <sessionname> | <sessionID>] [/server:<servername>]
query user
query user /server:remotemachine
quser
quser /server:remotemachine
```

query session - show user sessions

```winbatch
# query session [<sessionname> | <username> | <sessionID>] [/server:<servername>] [/mode] [/flow] [/connect] [/counter]
query session john.doe
qwinsta /server:servername
```

query session - show user processes

```winbatch
# query process [*|<processID>|<username>|<sessionname>|/id:<nn>|<programname>] [/server:<servername>]
query process john.doe
qprocess /server:servername
```

[query commands - Microsoft Learn](https://learn.microsoft.com/en-au/windows-server/administration/windows-commands/query)

[Common errors with query commands - How to Remotely Log Off User with Command Line? – TheITBros](https://theitbros.com/remotely-log-off-user-with-cmd/#:~:text=Possible%20errors%20when%20executing%20the%20logoff%20command%3A)

## Uptime

Find Uptime from System Info

```winbatch
systeminfo | find “System Boot Time”
```

Get Uptime from CIM via Powershell

```winbatch
Get-CimInstance -ClassName Win32_OperatingSystem | Select-Object LastBootUpTime
```

## Unformatted to add above

TBC

## Additional Resources

[Command-line reference A-Z - Windows commands - Microsoft Learn](https://learn.microsoft.com/en-au/windows-server/administration/windows-commands/windows-commands#command-line-reference-a-z)
