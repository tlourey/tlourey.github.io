---
title: PowerShell Commands
description: PowerShell Commands to remember
categories:
    - Tech
type: pages
layout: pages
published: true
date: 2024-12-31T10:54:00
lastmod: 2025-03-12T02:45:43.479Z
tags:
    - Commands
    - Exchange
    - Language
    - Microsoft365
    - PowerShell
    - References
    - SharePoint
    - Windows
isdraft: true
---


<!--- cSpell:disable --->
* [PowerShell Basics](#powershell-basics)
  * [Commands and Help](#commands-and-help)
  * [Common Pipeline Modifiers](#common-pipeline-modifiers)
  * [Comparison Operators](#comparison-operators)
    * [Dates](#dates)
    * [Times and TimeZones](#times-and-timezones)
  * [-WhatIf](#-whatif)
  * [Force](#force)
* [Module Management](#module-management)
  * [PowerShellGet and PSResourceGet](#powershellget-and-psresourceget)
* [Oneliners](#oneliners)
  * [Connecting to a remote server via powershell](#connecting-to-a-remote-server-via-powershell)
  * [Also See](#also-see)
* [Active Directory](#active-directory)
  * [User Management OneLiners](#user-management-oneliners)
* [Exchange Powershell](#exchange-powershell)
  * [Setup](#setup)
  * [Removing OWA Signatures from Email](#removing-owa-signatures-from-email)
  * [Mail tracing](#mail-tracing)
  * [Temporarily increase mailbox size (This assumes you never give users their full mailbox in the first place)](#temporarily-increase-mailbox-size-this-assumes-you-never-give-users-their-full-mailbox-in-the-first-place)
  * [Archive Mailbox](#archive-mailbox)
  * [Mailbox Access Checks](#mailbox-access-checks)
  * [Mailbox Access](#mailbox-access)
* [Local System Management](#local-system-management)
  * [File and Space Management OneLiners](#file-and-space-management-oneliners)
  * [Uptime, wake on lan, reboot](#uptime-wake-on-lan-reboot)
  * [Remote Desktop](#remote-desktop)
* [SharePoint PowerShell](#sharepoint-powershell)
* [Commands often forgotten](#commands-often-forgotten)
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

`fl` - [`format-list`](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/format-list)\
`ft` - [`format-table`](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/format-table)\
`sort` - [`sort-objects`](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/sort-object)\
`select` - [`select-object`](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/select-object)\
`where` - [`where-object`](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/where-object)

### Comparison Operators

<https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_comparison_operators>

`-contains`: Finds an item in a array/List, not great with wildcards\
`-like`: finds things like. good for wildcards

#### Dates

`-gt`: TBC\
`-lt`: TBC

#### Times and TimeZones

TBC

### -WhatIf

TBC

### Force

TBC

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

## Exchange Powershell

<https://learn.microsoft.com/en-us/powershell/exchange/exchange-online-powershell?view=exchange-ps>\
[Other Exchange PowerShells](https://learn.microsoft.com/en-us/powershell/module/exchange/?view=exchange-ps)\
<https://aka.ms/exov3-module>

NB: Sometimes this is easier in mail trace in EAC

### Setup

Install

```powershell
Install-Module ExchangeOnlineManagement
# OR
Install-Module ExchangeOnlineManagement -Scope CurrentUser
```

Update:

```powershell
Update-Module ExchangeOnlineManagement
```

If you get `Module 'ExchangeOnlineManagement' was not installed by using Install-Module, so it cannot be updated.`:

* Module may have more installed via MSI
* More Likely: It was installed for a different version of PowerShell - eg V7 and your using V5.1 [^1]

[^1]: <https://www.reddit.com/r/PowerShell/comments/yf07e3/comment/iu1bmh2/>

Import and connect

```powershell
# First time ever you need to install the module
Import-Module ExchangeOnlineManagement

# Normally you just need to type
Connect-ExchangeOnline
# You should get modern prompt that will deal with mfa

# When you are finished you should disconnect by typing:
disconnect-exchangeonline
```

<https://docs.microsoft.com/en-au/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps>

### Removing OWA Signatures from Email

```powershell
# check signature settings
Get-MailboxMessageConfiguration -id john.doe@domain.com | select *sig*

# Blank out signature value
Set-MailboxMessageConfiguration -id john.doe@domain.com -SignatureHtml $null -SignatureText $null

# set values to use signature to none
Set-MailboxMessageConfiguration -id john.doe@domain.com -AutoAddSignature $false -AutoAddSignatureOnMobile $false -AutoAddSignatureOnReply $false -UseDefaultSignatureOnMobile $false
```

### Mail tracing

```powershell
# get messages sent to john from joe, from exactly 1 day ago until this very second
Get-MessageTrace -RecipientAddress john.doe@domain.com -StartDate ((get-date).AddDays(-1)) -EndDate (get-date) -SenderAddress joe.blogs@domain.com
# If the above only returns one result
Get-MessageTrace -RecipientAddress john.doe@domain.com -StartDate ((get-date).AddDays(-1)) -EndDate (get-date) -SenderAddress joe.blogs@domain.com | fl
# if it returns many results, you can adjust filter further or browse objects by using one of the below
Get-MessageTrace -RecipientAddress john.doe@domain.com -StartDate ((get-date).AddDays(-1)) -EndDate (get-date) -SenderAddress joe.blogs@domain.com | out-gridview -passthrough | fl

#To get the trace details
Get-MessageTrace -RecipientAddress john.doe@domain.com -StartDate ((get-date).AddDays(-1)) -EndDate (get-date) -SenderAddress joe.blogs@domain.com | get-messagetracedetail
#To expand the trace details
Get-MessageTrace -RecipientAddress john.doe@domain.com -StartDate ((get-date).AddDays(-1)) -EndDate (get-date) -SenderAddress joe.blogs@domain.com | get-messagetracedetail | fl
```

### Temporarily increase mailbox size (This assumes you never give users their full mailbox in the first place)

```powershell
Set-Mailbox -id <<email@domain.com>> -ProhibitSendQuota <<Value>> -ProhibitSendReceiveQuota <<Value>>

# All our mailboxes are by default 40GB, so to increase to 45:
Set-Mailbox <<email@domain.com>> -ProhibitSendQuota 43GB -ProhibitSendReceiveQuota 45GB


# set mailbox sizses back to defaults afterwards:
Set-Mailbox -id <<email@domain.com>> -ProhibitSendReceiveQuota 40GB -ProhibitSendQuota 39GB -IssueWarningQuota 36GB
```

Make sure to lower mailbox sizes afterwards back to defaults

### Archive Mailbox

enable archive mailbox

```powershell
Enable-Mailbox -Identity mailbox -Archive
```

Turn on auto expanding archive (only use if licensed for exchange archive)

```powershell
Enable-Mailbox -Identity user -AutoExpandingArchive
```

force older content to move to archive mailbox once available

```powershell
Start-ManagedFolderAssistant -Identity <<email@domain.com>>

# Consider the below if doing in bulk. Use -whatif and -confirm to check (make sure you know how this works before doing it)
$Mailboxes = Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"}
$Mailboxes.Identity | Start-ManagedFolderAssistant
```

Make sure to lower mailbox sizes afterwards back to defaults

### Mailbox Access Checks

Search what permissions are on a particular mailbox

```powershell
# Search what permissions are on a particular mailbox
Get-MailboxPermission -Identity john.doe@domain.com
```

> [!WARNING] Queries against all mailboxes
> The below queries, unless filtered run across all mailboxes. These queries may take some time to run.

Search if a particular personal has access to any mailboxes

```powershell
# Search if a particular personal has access to any mailboxes
Get-Mailbox -ResultSize Unlimited | Get-MailboxFolderPermission -User john.doe@domain.com | ft User,Identity,AccessRights
```

### Mailbox Access

From and More info: <https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/manage-permissions-for-recipients>

Full Access

```powershell
Add-MailboxPermission -Identity <MailboxIdentity> -User <DelegateIdentity> -AccessRights FullAccess -InheritanceType All
Remove-MailboxPermission -Identity <MailboxIdentity> -User <DelegateIdentity> -AccessRights FullAccess -InheritanceType All

# This example assigns the delegate Raymond Sam the Full Access permission to the mailbox of Terry Adams.
Add-MailboxPermission -Identity "Terry Adams" -User raymonds -AccessRights FullAccess -InheritanceType All

# This does the same but *without* Automapping
Add-MailboxPermission -Identity "Terry Adams" -User raymonds -AccessRights FullAccess -InheritanceType All -AutoMapping $false
# There is no way to adjust automapping. To change it you need to remove the mailbox permission then re-add it with the new setting

# To test it worked
Get-MailboxPermission <MailboxIdentity> | where {$_.AccessRights -like 'Full*'} | Format-Table User,Deny,IsInherited,AccessRights -Auto
```

Send as

```powershell
# This example assigns the Send As permission to the Printer Support group on the shared mailbox named Contoso Printer Support.
Add-RecipientPermission -Identity "Contoso Printer Support" -Trustee "Printer Support" -AccessRights SendAs

# To test it worked:
Get-RecipientPermission -Identity <MailboxIdentity> -Trustee <DelegateIdentity>
```

Send be behalf

```powershell
# <Cmdlet> -Identity <MailboxOrGroupIdentity> -GrantSendOnBehalfTo <Delegates>
# This will reset whoever had the ability to send on behalf of Sean and only grant it to Holly
Set-Mailbox -Identity seanc@contoso.com -GrantSendOnBehalfTo hollyh

# This will add tempassistants to whoever can already send on behalf of Exec's shared mailbox
Set-Mailbox "Contoso Executives" -GrantSendOnBehalfTo @{Add="tempassistants@contoso.com"}

# This will reset whoever had the ability to send on behalf of PrinterSupport and only grant it to sarad
Set-DistributionGroup -Identity printersupport@contoso.com -GrantSendOnBehalfTo sarad

# This will only remove administrator
Set-DynamicDistributionGroup "All Employees" -GrantSendOnBehalfTo @{Remove="Administrator"}
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

## Commands often forgotten

`Get-Content -Path c:\temp\my-log-file.log -wait`: like cat. using -wait makes it like tail -f: <https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-content#-wait>\
`Select-String`: kind of like grep (need to check if it does work like grep)\
`Out-GridView`: really cool wait view tables/rows. -passthru is also really awesome. You should read the help page in full esp the Notes stuff: <https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/out-gridview>

## Additional Resources

[PowerShell Module Browser - PowerShell - Microsoft Learn](https://learn.microsoft.com/en-au/powershell/module/)\
[Find Azure AD PowerShell and MSOnline cmdlets in Microsoft Graph PowerShell](https://learn.microsoft.com/en-us/powershell/microsoftgraph/azuread-msoline-cmdlet-map?view=graph-powershell-1.0&pivots=azure-ad-powershell)\
<https://microsoft365dsc.com/>

## Other resources to add

* [ ] Implement oneliners from comments
