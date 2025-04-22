---
title: PowerShell Commands
description: PowerShell Commands to remember
categories:
    - Tech
type: pages
layout: pages
published: true
date: 2024-12-31T10:54:00
lastmod: 2025-04-22T04:17:32.385Z
tags:
    - Commands
    - Language
    - Microsoft365
    - PowerShell
    - References
    - Windows
isdraft: true
---


<!--- cSpell:disable --->
* [PowerShell Basics](#powershell-basics)
  * [Commands and Help](#commands-and-help)
  * [Common Pipeline Modifiers](#common-pipeline-modifiers)
  * [Useful Expression Modifiers](#useful-expression-modifiers)
  * [Regular Expressions](#regular-expressions)
  * [Comparison Operators](#comparison-operators)
    * [Dates](#dates)
    * [Times and TimeZones](#times-and-timezones)
  * [-WhatIf](#-whatif)
  * [-Force](#-force)
* [Module Management](#module-management)
  * [PowerShellGet and PSResourceGet](#powershellget-and-psresourceget)
* [Oneliners](#oneliners)
  * [Connecting to a remote server via powershell](#connecting-to-a-remote-server-via-powershell)
  * [Also See](#also-see)
* [Active Directory](#active-directory)
  * [User Management OneLiners](#user-management-oneliners)
* [Local System Management](#local-system-management)
  * [File and Space Management OneLiners](#file-and-space-management-oneliners)
  * [Uptime, wake on lan, reboot](#uptime-wake-on-lan-reboot)
  * [Remote Desktop](#remote-desktop)
* [SharePoint PowerShell](#sharepoint-powershell)
* [Exchange PowerShell](#exchange-powershell)
* [Commands often forgotten](#commands-often-forgotten)
* [Variables often forgotten](#variables-often-forgotten)
* [Additional Resources](#additional-resources)
* [Other resources to add](#other-resources-to-add)
<!--- cSpell:enable --->

## PowerShell Basics

<https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/>\
<https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about>

### Commands and Help

`get-command`:\
`get-command -module <ModuleName>`:\
`get-help commandname`:\
`get-help commandname -full`:\
`get-help commandname -detailed`:\
`get-help commandname -examples`:\
`get-help commandname -online`:\
`update-help`

### Common Pipeline Modifiers

[Using Format commands to change output view](https://learn.microsoft.com/en-us/powershell/scripting/samples/using-format-commands-to-change-output-view?view=powershell-7.5)

**`ft` - [`format-table`](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/format-table)**\
`fl` - [`format-list`](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/format-list)\
`fw` - [`format-wide`](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/format-wide) - I don't use this much\
**`sort` - [`sort-objects`](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/sort-object)**\
`select` - [`select-object`](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/select-object)\
**`where` - [`where-object`](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/where-object)**

There is also `format-custom` and `format-hex` but I have never used them. Custom looks interesting...

### Useful Expression Modifiers

Based off:

* <https://stackoverflow.com/questions/46862290/time-format-in-powershell/46862871#46862871>
* <https://4sysops.com/archives/add-a-calculated-property-with-select-object-in-powershell/>

```powershell
Get-Something | Format-Table @{Label="Date"; Expression={$_.ConvertToDateTime($_.CreationTime) |Get-Date -Format "dd/mm/yyyy HH:mm"}}
```

```powershell
Get-MessageTrace -SenderAddress sender@domain.tld -StartDate ((Get-Date).AddDays(-1)) -EndDate (get-date) | Format-Table @{Label="Received"; Expression={($_.Received).ToLocalTime()}}
```

```powershell
Get-MessageTrace -SenderAddress sender@domain.tld -StartDate ((Get-Date).AddDays(-1)) -EndDate (get-date) | Select-Object @{Label="Received"; Expression={($_.Received).ToLocalTime()}},* | Format-Table
```

The last example works but includes all columns which you may not want. If thats the space, specify the columns you want instead of specifying `*`.

* [ ] extrapolate above example for timezones using `Get-MessageTrace`

### Regular Expressions

[about Regular Expressions (Windows PowerShell 5.1)](https://learn.microsoft.com/en-au/powershell/module/microsoft.powershell.core/about/about_regular_expressions?view=powershell-5.1)\
[about Regular Expressions (PowerShell 7.4)](https://learn.microsoft.com/en-au/powershell/module/microsoft.powershell.core/about/about_regular_expressions?view=powershell-7.4)

* [ ] Add in key notes on regular expressions and some examples.

### Comparison Operators

<https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_comparison_operators>

`-contains`: Finds an item in a array/List, not great with wildcards\
`-like`: finds things like. good for wildcards

#### Dates

<https://www.sharepointdiary.com/2021/11/date-format-in-powershell.html> maybe useful

`-gt`: TBA\
`-lt`: TBA

#### Times and TimeZones

TBC

* [ ] Finish Get-Date Stuff

<https://www.sharepointdiary.com/2021/11/date-format-in-powershell.html> maybe useful

[Get-Date for PowerShell 5.1](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/get-date?view=powershell-5.1)\
[Get-Date for PowerShell 7.4 (LTS)](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/get-date?view=powershell-7.4)

`get-date`: Get current date and time in **local** timezone\
`get-date "2021-08-26Z16:44:42"`: Adding a z makes it explicit that its UTC\

Get-Date uses OS Culture: `(Get-Culture).DateTimeFormat`

Parameters:

`Get-Date -DisplayHint Date`: Example: Tuesday, June 25, 2019\
`Get-Date -DisplayHint Time`: Example: 10:24:11 PM\
`Get-Date -DisplayHint DateTime`: Example: Wednesday 9 April 2025 10:23:48 PM

`Get-Date -Format "dddd MM/dd/yyyy HH:mm K"`: Specifies format you want date returned. Example: Tuesday 06/25/2019 16:17 -07:00\
Uses .Net Formats. See [Custom date and time format strings.](https://learn.microsoft.com/en-us/dotnet/standard/base-types/custom-date-and-time-format-strings)\
`Get-Date -UFormat "%A %m/%d/%Y %R %Z"`: Example: Tuesday 06/25/2019 16:19 -07\
[UFormat notes](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/get-date?view=powershell-5.1#notes)\
`Get-Date -UnixTimeSeconds`: Date and time represented in seconds since January 1, 1970, 0:00:00 (Added in PS7)

Properties and Methods:

`((Get-Date).AddDays(-1))`: Take current time and go back 1 day\
`((Get-Date).AddHours(30))`: Add 30 hours to curren time\
Other Add Methods:

```powershell
Name                 MemberType     Definition
----                 ----------     ----------
Add                  Method         datetime Add(timespan value)
AddDays              Method         datetime AddDays(double value)
AddHours             Method         datetime AddHours(double value)
AddMicroseconds      Method         datetime AddMicroseconds(double value)
AddMilliseconds      Method         datetime AddMilliseconds(double value)
AddMinutes           Method         datetime AddMinutes(double value)
AddMonths            Method         datetime AddMonths(int months)
AddSeconds           Method         datetime AddSeconds(double value)
AddTicks             Method         datetime AddTicks(long value)
AddYears             Method         datetime AddYears(int value)
```

`(get-date) | Get-Member`: Show all methods\
`(get-date "2021-08-26 16:44:42").ToLocalTime()`: Get a specific date (**assumes** UTC) and convert it to local time\
`(get-date "2021-08-26 16:44:42").ToUniversalTime()`: Get a specific date (**assumes** local) and convert it to UTC time

> [!NOTE] PS5 vs 7
> There are some differences in `Get-Date` between versions, like the `-asutc` Parameters

`Get-TimeZone`: Tells you current timezone

### -WhatIf

TBC

* [ ] Fill in -whatif section

### -Force

TBC

* [ ] Fill in -Force section

## Module Management

* [ ] Fill in the Module Management commands

`Get-Module`: TBC\
`Get-Module -ListAvailable`: TBC\
`Find-Module`
`Install-Module`: TBC\
`Install-Module -scope CurrentUser`: TBC\
`Install-Module -scope AllUsers`: TBC\
`Update-Module`: TBC\
`Uninstall-Module`: TBC - [REF](https://learn.microsoft.com/en-us/powershell/module/powershellget/uninstall-module)

* Consider Admin Rights
* Consider Module Locations
* Consider Multiple Versions

`Import-Module`: TBC\
`Remove-Module`: TBC\

`-AllowClobber`: TBC\
`-AllowPreRelease`: TBC

Also check [Modules in PowerShell Tips](powershell-tips.md#modules) for info on module paths

### PowerShellGet and PSResourceGet

TBC

## Oneliners

### Connecting to a remote server via powershell

```powershell
enter-pssession
# connect as current user
enter-pssession servername

# prompt for a different user
enter-pssession servername -Credential (Get-Credential)
```

### Also See

[User Management OneLiners](#user-management-oneliners)\
[File and Space Management OneLiners](#file-and-space-management-oneliners)

## Active Directory

[ActiveDirectory PowerShell Module](https://learn.microsoft.com/en-us/powershell/module/activedirectory/)\
[about_ActiveDirectory](https://learn.microsoft.com/en-us/powershell/module/activedirectory/about/about_activedirectory)

### User Management OneLiners

move a users direct reports to another user

```powershell
# Show a specific users direct reports and their title and department
# eg, show all John Doe direct reports, their title and department
(get-aduser -Properties directreports -id joe.doe).directreports | get-aduser -Properties Title,Department | sort Name | format-table Name,Title,Department -autosize

# Change all direct reports manager
# eg, set all John Doe direct reports manager to Joe Bob
(get-aduser -Properties directreports -id john.doe).directreports | set-aduser -Manager (Get-aduser -id joe.bob)
```

get the UPN's of AD members of a AD group and sort by UPN

```powershell
get-adgroup -id Sales | Get-ADGroupMember | get-aduser -Properties UserPrincipalName | sort UserPrincipalName | format-table Name,UserPrincipalName,Enabled -AutoSize
```

set, replace or remove extensionAttributes

```powershell
# To add the value if it isn't already present
Set-ADUser -Identity "anyUser" -Add @{extensionAttribute1="12345679"}
# To update the value:
Set-ADUser -Identity "anyUser" -Replace @{extensionAttribute1="myString"}
# to remove the value:
Set-ADUser -Identity "anyUser" -Remove @{extensionAttribute1="myString"}
# or
Set-ADUser -Identity "anyUser" -clear extensionAttribute1
```

Disabled Managers Direct Reports

```powershell
# show disabled managers who have direct reports
(get-aduser -filter {(Enabled -eq $false) -and (directreports -like "*")} -Properties directreports).name

# show disabled managers direct reports
(get-aduser -filter {(Enabled -eq $false) -and (directreports -like "*")} -Properties directreports).directreports

# show the 3rd disabled mangers name that has direct reports
(get-aduser -filter {(Enabled -eq $false) -and (directreports -like "*")} -Properties directreports)[2].name

# show the 3rd disabled mangers direct reports
(get-aduser -filter {(Enabled -eq $false) -and (directreports -like "*")} -Properties directreports)[2].directreports

# change the 3rd disabled managerts direct reports to another manager
(get-aduser -filter {(Enabled -eq $false) -and (directreports -like "*")} -Properties directreports)[2].directreports | set-aduser -manager (get-aduser -id newmanagerfirstname.lastname)
```

## Local System Management

### File and Space Management OneLiners

Find Files over than 30 days

```powershell
# List *.log files over 30 days
Get-ChildItem -Filter *.log -Path c:\windows\system32\logfiles | where {$_.CreationTime -lt ((Get-Date).AddDays(-30))}
```

Find and delete files over than 30 days

```powershell
# Delete *.log files over 30 days
Get-ChildItem -Filter *.log -Path c:\windows\system32\logfiles | where {$_.CreationTime -lt ((Get-Date).AddDays(-30))} | Remove-Item -Confirm
```

### Uptime, wake on lan, reboot

Get Uptime from CIM via Powershell

```powershell
Get-CimInstance -ClassName Win32_OperatingSystem | Select-Object LastBootUpTime
```

Send wake on lan magic packet via Powershell

```powershell
# change the mac address you need but make sure its all upper case and use "-". Don't use : as this sometimes isn't supported in earlier versions of Powershell.
# Computer needs to be on the same network.
# send a couple of times.

$mac = '01-23-45-67-89-AB';
[System.Net.NetworkInformation.NetworkInterface]::GetAllNetworkInterfaces() | Where-Object { $_.NetworkInterfaceType -ne [System.Net.NetworkInformation.NetworkInterfaceType]::Loopback -and $_.OperationalStatus -eq [System.Net.NetworkInformation.OperationalStatus]::Up } | ForEach-Object {
    $networkInterface = $_
    $localIpAddress = ($networkInterface.GetIPProperties().UnicastAddresses | Where-Object { $_.Address.AddressFamily -eq [System.Net.Sockets.AddressFamily]::InterNetwork })[0].Address
    $targetPhysicalAddress = [System.Net.NetworkInformation.PhysicalAddress]::Parse(($mac.ToUpper() -replace '[^0-9A-F]',''))
    $targetPhysicalAddressBytes = $targetPhysicalAddress.GetAddressBytes()
    $packet = [byte[]](,0xFF * 102)
    6..101 | Foreach-Object { $packet[$_] = $targetPhysicalAddressBytes[($_ % 6)] }
    $localEndpoint = [System.Net.IPEndPoint]::new($localIpAddress, 0)
    $targetEndpoint = [System.Net.IPEndPoint]::new([System.Net.IPAddress]::Broadcast, 9)
    $client = [System.Net.Sockets.UdpClient]::new($localEndpoint)
    try { $client.Send($packet, $packet.Length, $targetEndpoint) | Out-Null } finally { $client.Dispose() }
}
```

### Remote Desktop

Refer to [RemoteDesktop Powershell Module and Commands - Microsoft Learn](https://learn.microsoft.com/en-au/powershell/module/remotedesktop/)

> [!TIP] Old Query Commands
> Check the [old query commands](windows-commands.md#query-commands)

## SharePoint PowerShell

[SharePoint Online PowerShell](sharepoint-references.md#sharepoint-online-powershell)\
[PnP PowerShell Intro](https://learn.microsoft.com/en-au/powershell/sharepoint/sharepoint-pnp/sharepoint-pnp-cmdlets?view=sharepoint-ps)\
[PnP PowerShell](https://pnp.github.io/powershell/index.html)

## Exchange PowerShell

[Exchange Online PowerShell](exchange-commands.md#exchange-online-powershell)\
[Eseutil](exchange-commands.md#eseutil)

## Commands often forgotten

`Get-Content -Path c:\temp\my-log-file.log -wait`: like cat. using -wait makes it like tail -f: <https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-content#-wait>\
`Select-String`: kind of like `grep` (need to check if it does work like grep).See: <https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/select-string?view=powershell-7.5>\
`Out-GridView`: really cool wait view tables/rows. -passthru is also really awesome. You should read the help page in full esp the Notes stuff: <https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/out-gridview>\
`New-Item -ItemType File -Path .\filename.ext -Force`: closest thing in powershell to linux `touch`
`. $profile`: reload powershell profile (assumes its in the current folder)

[Redirecting Output](https://learn.microsoft.com/en-us/powershell/scripting/samples/redirecting-data-with-out---cmdlets?view=powershell-7.5)

## Variables often forgotten

`$PSVersionTable`: shows powershell version\
`$profile`: Show where current powershell profile is\
`. $profile`: reload powershell profile (assumes its in the current folder)

## Additional Resources

[PowerShell Tips](powershell-tips.md)

[PowerShell Module Browser - PowerShell - Microsoft Learn](https://learn.microsoft.com/en-au/powershell/module/)\
[Find Azure AD PowerShell and MSOnline cmdlets in Microsoft Graph PowerShell](https://learn.microsoft.com/en-us/powershell/microsoftgraph/azuread-msoline-cmdlet-map?view=graph-powershell-1.0&pivots=azure-ad-powershell)\
<https://microsoft365dsc.com/>

## Other resources to add

* [ ] Implement oneliners from comments
* [ ] Add MSGraph PowerShell stuff
