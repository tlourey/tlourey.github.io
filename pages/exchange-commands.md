---
title: Exchange Commands
description: ""
published: false
categories:
  - Tech
type: pages
layout: pages
date: 2025-01-29T07:27:17.598Z
lastmod: 2025-03-04T11:35:15.677Z
tags:
  - Exchange
isdraft: true
fmContentType: pages
preview: ""
---

<!--- cSpell:disable --->
* [Heading](#heading)
<!--- cSpell:enable --->

## Heading

<!--

## Import of very very old onenote for on prem

MISC

Get-excommand - shows just exchange commands and not everything
When opening exchange management shell, read the tip of the day. They are useful. 
#
# TIP: You can create your own customizations and put them in My Documents\WindowsPowerShell\profile.ps1
# Anything in profile.ps1 will then be run every time you start the shell. 
#
Quick Ref: http://technet.microsoft.com/en-us/library/jj619302(EXCHG.150).aspx

Remoting:
  $UserCredential = Get-Credential
  $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri http://ExServer.contoso.com/PowerShell/ -Authentication Kerberos -Credential $UserCredential
  Import-PSSession $Session
  From <http://technet.microsoft.com/en-us/library/jj619302(EXCHG.150).aspx> 

C:\Program Files\Microsoft\Exchange Server\V15\Scripts\New-TestCasConnectivityUser.ps1	Script for creating test user for testing CAS
Test-OutlookWebServices -ClientAccessServer "CASServerName"	Test outlook web service using CAS account created in script

Any-command | fl | more	Your best friend in powershell. Show all the attributes it can and let you page them through them

DAGs
Get-DatabaseAvailabilityGroup	Show available database availability groups
Get-DatabaseAvailabilityGroup -Identity DAGNAME | fl | more	Show details about Database Available Group specified
Get-DatabaseAvailabilityGroupNetwork | fl	Show details about all available Database Availability Group Networks
CollectOverMetrics.ps1 -DatabaseAvailabilityGroup EXCHDAG01 -Database:"MBDB01" -GenerateHTMLReport -ShowHTMLReport	Generate DAG stats

Mailbox Servers
Get-mailboxserver | Get-ADPermission -User "user filter"	Check server level permissions

Databases & Database Copies
Get-mailboxdatabase	Show mailbox databases
Get-mailboxdatabasecopy status 	check database copy status - copy and reply queue length
Get-MailboxDatabase | Get-ADPermissions -User "user filter" 	Check database level permissions
Test-replicationhealth	shows the dags health quickly and gives a good idea of where to look next
Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX3 -ActivationPreference 2 	Create a copy of an existing database on server MBX3 and set it's activation preference From <http://technet.microsoft.com/en-us/library/dd298080(v=exchg.150).aspx> 

Manual Seeding aritcle - risky - http://www.petri.co.il/seed-exchange-2010-dag-database.htm

Suspend-MailboxDatabasecopy "DBName\Servername"	Stop Database Copy on specified server. Normally only used on Active Database
Update-Mailboxdatabasecopy "DBName\Servername"	Update the content of the mailbox database. Normally used on passive server
Update-mailboxdatabasecopy "DBName\Servername" -CatalogOnly	Fixes content index state when failed (server name is name of server failed assuming other server is healthy)
Get-MailboxDatabaseCopyStatus DBName | fl *index*	Easy way to show error about content index state

When REALLY fucked:
Move-ActiveMailboxDatabase DBNAME -ActivateOnServer SERVERNAME -SkipHealthChecks -SkipActiveCopyChecks -SkipClientExperienceChecks -SkipLagChecks -MountDialOverride:BESTEFFORT

From <http://blogs.technet.com/b/timmcmic/archive/2012/05/30/exchange-2010-the-mystery-of-the-9223372036854775766-copy-queue.aspx> 

http://blogs.technet.com/b/timmcmic/archive/2012/05/30/exchange-2010-the-mystery-of-the-9223372036854775766-copy-queue.aspx

Certificates
Generate CSR
Set-Content -path "C:\Temp\Certname" -Value (New-ExchangeCertificate -GenerateRequest -KeySize 2048 -SubjectName "c=AU, s=NSW, l=Sydney, o=Company, ou=OU Name, cn=mail.domainname.com" -DomainName autodiscover.domainname.com -PrivateKeyExportable $True)	Generate Certificate request and put in c:\temp\certname - change values as required

Import & Enable Certificate
Import-ExchangeCertificate -FileData ([Byte[]]$(Get-Content -Path C:\temp\cert.p7s -Encoding byte -ReadCount 0)) | Enable-ExchangeCertificate -Services "IIS,POP,IMAP,SMTP"	Import certificate from CA and activate that certificate for these services. 

Recipients
Update Recipient Quota Policy
Get-RecipientEnforcementProvisioningPolicy -Identity "Engage\Recipient Quota Policy" | Format-List
Set-RecipientEnforcementProvisioningPolicy -Identity "Engage\Recipient Quota Policy" -MailboxCountQuota 25 -MailUserCountQuota 25

Mailboxes
Get-mailbox -identity "nam*" 	Show all mailboxes that start with nam
Get-mailbox -identity "name" | fl	Get all details of a specific mailbox
New-Mailbox "Firstname Lastname" -UserPrincipalName firstname.lastname@domain.tld [-Organization OrgName]	Create a new mailbox and specify the UPN. If using organisations, association it to OrgName
Get-casmailbox -Identity	Get CAS Settings for the mailbox
Set-casmailbox -Identify "Name" -MAPIEnabled $false -OWAEnabled $True	Set cas settings for mailbox (MAPI Disabled, OWA Enabled) - NB: MAPI Disabled means that OutlookAnywhere will not work. Even Over HTTPS in 2013

Recover Deleted mailboxes
  get-MailboxDatabase
  Clean-MailboxDatabase -Identity "Mailbox Database 0765792180"

Use this command to find failure messages for all failed moves:
Get-MoveRequest -MoveStatus Failed | Get-MoveRequestStatistics | ft Alias, percentcomplete, message -auto

get-mailbox -Database "Mailbox Database 0237090912" | New-MoveRequest -TargetDatabase "TARGETDATABASENAME”
get-mailbox -Database "Mailbox Database 0237090912" -arbitration | New-MoveRequest -TargetDatabase "TARGETDATABASENAME”
Where "Mailbox Database 0237090912" is the database Exchange 2010 made and "TARGETDATABSE" is the database you're moving everything to.

From <http://social.technet.microsoft.com/Forums/exchange/en-US/284b0267-180e-435a-85ab-c7692b05549a/move-the-discovery-search-mailbox> 

Distribution Groups
Get-DistributionGroup -Identity GroupName [-Organization Orgname] | Set-DistributionGroup -Requi
reSenderAuthenticationEnabled $false

Policies

Connectors
Get-SendConnector
Set-SendConnector "SENDCONNECTORNAME" -SmartHosts smarthost.domain.com
Set-TransportConfig -MaxReceiveSize 50MB -MaxSendSize 50MB
Receiving email
Set-ReceiveConnector -PermissionGroups 'AnonymousUsers, ExchangeUsers, ExchangeServers, ExchangeLegacyServers' -Identity 'Exchange\Default Exchange'
Sending external emails
new-SendConnector -Name 'Using SmartHost' -Usage 'Custom' -AddressSpaces 'SMTP:*;1' -IsScopedConnector $false -DNSRoutingEnabled $false -SmartHosts '[192.168.1.1]' -SmartHostAuthMechanism 'None' -UseExternalDNSServersEnabled $false -SourceTransportServers 'Exchange'
Set-SendConnector "Using SmartHost" -SmartHosts smarthost.domain.com
Sending Inter-Organization emails
new-SendConnector -Name 'HostedDemo' -Usage 'Internal' -AddressSpaces 'SMTP:hosted.domain.com;1','SMTP:domain.com;1' -IsScopedConnector $false -DNSRoutingEnabled $false -SmartHosts '[127.0.0.1]'-SmartHostAuthMechanism 'None' -UseExternalDNSServersEnabled $false  -SourceTransportServers 'Exchange'

Remote Domains
New-RemoteDomain -Name domainname-DomainName domainname.com
Set-RemoteDomain domainname -TNEFEnabled $false

UM

Autodiscover
Autodiscover Redirection 
Set-AutodiscoverVirtualDirectory -Identity 'Autodiscover (Default Web Site)' -ExternalURL 'https://exchange.domain.com/autodiscover' -InternalURL 'https://exchange.domain.com/autodiscover' -BasicAuthentication $true
Set-OABVirtualDirectory -Identity "EXCHANGE\OAB (Default Web Site)" -ExternalUrl "https://exchange.domain.com/OAB" -InternalURL "https://exchange.domain.com/OAB" -BasicAuthentication $true -RequireSSL $true
Set-WebServicesVirtualDirectory -Identity "EXCHANGE\EWS (Default Web Site)" -BasicAuthentication $true -ExternalUrl https://exchange.domain.com/EWS/exchange.asmx -InternalUrl https://exchange.domain.com/EWS/exchange.asmx

Outlook Anywhere 
Enable-OutlookAnywhere -Server 'exchange' -ExternalHostname 'exchange.domain.com' -DefaultAuthenticationMethod 'Basic' -SSLOffloading $false

Address Lists/book
Get-offlineaddressbook | fl 
Get-Offlineaddressbook | fl Name
Update-offlineaddressbook -Identity "Default Offline Address List"
Get-globaladdresslist

Remote Domains
Get-Remotedomain | fl 
Get-Remotedomain Default | fl
Get-RemoteDomain Name | fl
Get-RemoteDomain Default | Set-RemoteDomain -AutoForwardEnabled $true
Get-RemoteDomain Default | Set-RemoteDomain -TNEFEnable $false
New-Remotedomain -Name some-custom-domain -domainame somecustomdomain.com.au
get-RemoteDomain some-custom-domain | fl
get-RemoteDomain some-custom-domain | Set-RemoteDomain -AutoReplyEnabled $true
Remove-Remotedomain some-custom-domain

-->
