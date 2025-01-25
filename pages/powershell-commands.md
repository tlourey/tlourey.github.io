---
title: PowerShell Commands
description: PowerShell Commands to remember
categories:
  - Tech
type: pages
layout: pages
published: true
date: 2024-12-31T10:54:00
lastmod: 2025-01-24T03:23:15.410Z
tags:
  - Commands
  - Language
  - PowerShell
  - Reference
---


<!--- cSpell:disable --->
* [Oneliners](#oneliners)
  * [User Management](#user-management)
  * [Connecting to a remote server via powershell](#connecting-to-a-remote-server-via-powershell)
  * [Exchange Powershell](#exchange-powershell)
    * [Archive Mailbox](#archive-mailbox)
    * [Mailbox Access Checks](#mailbox-access-checks)
    * [Mailbox Access](#mailbox-access)
  * [Local System Management](#local-system-management)
    * [Uptime, wake on lan, reboot](#uptime-wake-on-lan-reboot)
    * [Remote Desktop](#remote-desktop)
* [Commands often forgotten](#commands-often-forgotten)
* [Additional Resources](#additional-resources)
* [Other resources to add](#other-resources-to-add)
<!--- cSpell:enable --->

## Oneliners

### User Management

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

### Connecting to a remote server via powershell

```powershell
enter-pssession
# connect as current user
enter-pssession servername

# prompt for a different user
enter-pssession servername -Credential (Get-Credential)
```

### Exchange Powershell

NB: Sometimes this is easier in mail trace in EAC

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

Removing OWA Signatures from Email

```powershell
# check signature settings
Get-MailboxMessageConfiguration -id john.doe@domain.com | select *sig*

# Blank out signature value
Set-MailboxMessageConfiguration -id john.doe@domain.com -SignatureHtml $null -SignatureText $null

# set values to use signature to none
Set-MailboxMessageConfiguration -id john.doe@domain.com -AutoAddSignature $false -AutoAddSignatureOnMobile $false -AutoAddSignatureOnReply $false -UseDefaultSignatureOnMobile $false
```

Mail tracing

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

Temporarily increase mailbox size (This assumes you never give users their full mailbox in the first place)

```powershell
Set-Mailbox -id <<email@domain.com>> -ProhibitSendQuota <<Value>> -ProhibitSendReceiveQuota <<Value>>

# All our mailboxes are by default 40GB, so to increase to 45:
Set-Mailbox <<email@domain.com>> -ProhibitSendQuota 43GB -ProhibitSendReceiveQuota 45GB


# set mailbox sizses back to defaults afterwards:
Set-Mailbox -id <<email@domain.com>> -ProhibitSendReceiveQuota 40GB -ProhibitSendQuota 39GB -IssueWarningQuota 36GB
```

Make sure to lower mailbox sizes afterwards back to defaults

#### Archive Mailbox

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

#### Mailbox Access Checks

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

#### Mailbox Access

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

### Local System Management

#### Uptime, wake on lan, reboot

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

#### Remote Desktop

Refer to [RemoteDesktop Powershell Module and Commands - Microsoft Learn](https://learn.microsoft.com/en-au/powershell/module/remotedesktop/)

> [!TIP] Old Query Commands
> Check the [old query commands](windows-commands.md)

## Commands often forgotten

`get-content -path c:\temp\mylogfile.log -wait`: like cat. using -wait makes it like tail -f
`select-string`: kind of like grep (need to check if it does work like grep)
`out-gridview`: really cool wait view tables/rows

## Additional Resources

[PowerShell Module Browser - PowerShell - Microsoft Learn](https://learn.microsoft.com/en-au/powershell/module/)

## Other resources to add

* [ ] Implement oneliners from comments
