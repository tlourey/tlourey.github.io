---
title: Windows Commands
description: Windows Commands to remember
categories:
    - Tech
type: pages
layout: pages
published: true
date: 2024-12-31T11:24:00
lastmod: 2026-01-19T04:40:56.474Z
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
* [Netsh](#netsh)
  * [Common Netsh oneliners](#common-netsh-oneliners)
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

> [!WARNING] Don't just delete folders from c:\users\
> Deleting folders of old user profiles from `c:\users` is not wise. Why?
> If that user account ties to login again, the system registry will still expect their profile folder to be there. When it isn't, it will have an error and load a temporary profile.

To <ins>***cleanly***</ins> remove old profiles from a machine run one of the following:

```bat
rem Run this from an administrative command prompt
rundll32.exe sysdm.cpl,EditUserProfiles
rem OR 
rem run the below from anywhere (it will prompt for admin rights)
c:\Windows\system32\SystemPropertiesAdvanced.exe
```

Then press "Settings" inside the "User Profiles" frame. Then delete the users from there.

## Bitlocker Status

Check Bitlocker Status

```bat
manage-bde -status
```

## Netsh

<https://learn.microsoft.com/en-us/windows-server/networking/technologies/netsh/netsh>\
<https://learn.microsoft.com/en-us/windows-server/networking/technologies/netsh/netsh-contexts>\
<https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/netsh>

```text
netsh
netsh [-a AliasFile] [-c Context] [-r RemoteMachine] [-u [DomainName\]UserName] [-p Password | *] [Command | -f ScriptFile]
```

|Parameter|Description|
|-|-|
|-a|Specifies that you're returned to the netsh shell after running AliasFile.|
|AliasFile|Specifies the name of the text file that contains one or more netsh commands.|
|-c|Specifies that netsh enters the specified netsh context.|
|Context|Specifies the netsh context that you want to enter.|
|-r|Specifies that you want the command to run on a remote computer. The Remote Registry service must be running on the remote computer. If it's not running, Windows displays a "Network Path Not Found" error message.|
|RemoteComputer|Specifies the remote computer that you want to configure.|
|-u|Specifies that you want to run the netsh command under a user account.|
|DomainName\\ |Specifies the domain where the user account is located. The default is the local domain if DomainName\ isn't specified.|
|UserName|Specifies the user account name.|
|-p|Specifies that you want to provide a password for the user account.|
|Password|Specifies the password for the user account that you specified with -u UserName.|
|Command|Specifies the netsh command that you want to run.|
|-f|Exits netsh after running the script that you designate with ScriptFile.|
|ScriptFile|Specifies the script that you want to run.|

### Common Netsh oneliners

Show connected WiFi Network: `netsh WLAN show interfaces`\
Show all WiFi Networks: `netsh wlan show networks`\
Show all WiFi Profiles: `netsh wlan show profiles`\
Connect a Wifi interface using a profile name: `netsh wlan connect name="ProfileName" interface="InterfaceName"`

## Unformatted to add above

TBC

## Additional Resources

[Command-line reference A-Z - Windows commands - Microsoft Learn](https://learn.microsoft.com/en-au/windows-server/administration/windows-commands/windows-commands#command-line-reference-a-z)\
[Netsh Commands for Wireless Local Area Network (WLAN) in Windows Server 2008 R2](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd744890(v=ws.10))

<https://superuser.com/questions/991457/how-do-i-display-a-list-of-wi-fi-connections-using-netsh>
