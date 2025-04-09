---
title: Exchange Commands
description: Mostly Exchange Online but some legacy onprem stuff as well
published: true
categories:
    - Tech
type: pages
layout: pages
date: 2025-04-09T13:03:20.971Z
lastmod: 2025-04-09T13:46:37.923Z
tags:
    - Exchange
    - PowerShell
    - Microsoft365
isdraft: true
fmContentType: pages
mermaid: false
preview: ""
keywords:
    - Exchange
    - Exchange Online
---

<!--- cSpell:disable --->
* [Exchange Online Powershell](#exchange-online-powershell)
  * [Setup](#setup)
  * [Removing OWA Signatures from Email](#removing-owa-signatures-from-email)
  * [Mail tracing](#mail-tracing)
  * [Temporarily increase mailbox size](#temporarily-increase-mailbox-size)
  * [Archive Mailbox](#archive-mailbox)
  * [Mailbox Access Checks](#mailbox-access-checks)
  * [Mailbox Access](#mailbox-access)
  * [Exchange Audit Log search](#exchange-audit-log-search)
    * [Searching for Exchange Rule Changes](#searching-for-exchange-rule-changes)
    * [Searxhing for Exchange Connector Changes](#searxhing-for-exchange-connector-changes)
* [Eseutil](#eseutil)
* [Other References](#other-references)
<!--- cSpell:enable --->

## Exchange Online Powershell

<https://learn.microsoft.com/en-us/powershell/exchange/exchange-online-powershell?view=exchange-ps>\
[Other Exchange PowerShells](https://learn.microsoft.com/en-us/powershell/module/exchange/?view=exchange-ps)\
<https://aka.ms/exov3-module>

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

NB: Sometimes this is easier in mail trace in EAC

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

Searches:

```powershell
# See previous searches (larger traces)
Get-HistoricalSearch
Get-HistoricalSearch | fl

# Start a new searches
Start-HistoricalSearch
     -EndDate <DateTime>
     -ReportTitle <String>
     -ReportType <HistoricalSearchReportType>
     -StartDate <DateTime>
     [-BlockStatus <String>]
     [-CompressFile <Boolean>]
     [-ConnectorType <String>]
     [-DeliveryStatus <String>]
     [-Direction <MessageDirection>]
     [-DLPPolicy <MultiValuedProperty>]
     [-EncryptionTemplate <String>]
     [-EncryptionType <String>]
     [-Locale <CultureInfo>]
     [-MessageID <MultiValuedProperty>]
     [-NetworkMessageID <MultiValuedProperty>]
     [-NotifyAddress <MultiValuedProperty>]
     [-OriginalClientIP <String>]
     [-RecipientAddress <MultiValuedProperty>]
     [-SenderAddress <MultiValuedProperty>]
     [-SmtpSecurityError <String>]
     [-TLSUsed <String>]
     [-TransportRule <MultiValuedProperty>]
     [-Url <String>]
     [<CommonParameters>]

# Example
Start-HistoricalSearch -ReportTitle "Fabrikam Search" -StartDate 1/1/2023 -EndDate 1/7/2023 -ReportType MessageTrace -SenderAddress michelle@fabrikam.com -NotifyAddress chris@contoso.com

# Stop
Stop-HistoricalSearch -JobId <<GUID>>
```

**<https://learn.microsoft.com/en-us/powershell/module/exchange/start-historicalsearch?view=exchange-ps>**

### Temporarily increase mailbox size

> [!IMPORTANT] ASSUMPTION!
> This assumes you never give users their full mailbox in the first place.

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

### Exchange Audit Log search

#### Searching for Exchange Rule Changes

`Search-UnifiedAuditLog -StartDate 25/11/2024 -EndDate 27/11/2024 -Operations New-TransportRule, Set-TransportRule, Enable-TransportRule, Disable-TransportRule, Remove-TransportRule | Format-Table`

#### Searxhing for Exchange Connector Changes

`Search-UnifiedAuditLog -StartDate -StartDate 25/11/2024 -EndDate 27/11/2024 -Operations "New-InboundConnector","Set-InboundConnector","Remove-InboundConnector`

## Eseutil

TBC

## Other References

[PowerShell Commands](powershell-commands.md)\
[Microsoft365 Tips](microsoft-365-tips.md)
