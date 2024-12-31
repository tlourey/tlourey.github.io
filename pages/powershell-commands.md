---
title: Powershell Commands
description: Powershell Commands to remember
---

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
Get-MailboxMessageConfiguration -id charles.mcgregor-shaw@careflight.org | select *sig*
 
# Blank out signature value
Set-MailboxMessageConfiguration -id charles.mcgregor-shaw@careflight.org -SignatureHtml $null -SignatureText $null
 
# set values to use signature to none
Set-MailboxMessageConfiguration -id charles.mcgregor-shaw@careflight.org -AutoAddSignature $false -AutoAddSignatureOnMobile $false -AutoAddSignatureOnReply $false -UseDefaultSignatureOnMobile $false
```

Mail tracing

```powershell
# get messages sent to tracey from tim, from exactly 1 day ago until this very second
Get-MessageTrace -RecipientAddress tracey.patch@careflight.org -StartDate ((get-date).AddDays(-1)) -EndDate (get-date) -SenderAddress tim.lourey@careflight.org
# If the above only returns one result
Get-MessageTrace -RecipientAddress tracey.patch@careflight.org -StartDate ((get-date).AddDays(-1)) -EndDate (get-date) -SenderAddress tim.lourey@careflight.org | fl
# if it returns many results, you can adjust filter further or browse objects by using one of the below
Get-MessageTrace -RecipientAddress tracey.patch@careflight.org -StartDate ((get-date).AddDays(-1)) -EndDate (get-date) -SenderAddress tim.lourey@careflight.org | out-gridview -passthrough | fl
 
#To get the trace details
Get-MessageTrace -RecipientAddress tracey.patch@careflight.org -StartDate ((get-date).AddDays(-1)) -EndDate (get-date) -SenderAddress tim.lourey@careflight.org | get-messagetracedetail
#To expand the trace details
Get-MessageTrace -RecipientAddress tracey.patch@careflight.org -StartDate ((get-date).AddDays(-1)) -EndDate (get-date) -SenderAddress tim.lourey@careflight.org | get-messagetracedetail | fl
```
