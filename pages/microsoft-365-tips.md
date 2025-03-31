---
title: Microsoft 365 Tips
description: Bottomless pit of Microsoft 365, Office 365, Exchange, and even some Entra/Azure AD Tips
published: true
categories:
    - Tech
type: pages
layout: pages
isdraft: true
tags:
    - Entra
    - Exchange
    - Microsoft365
    - Office
    - OneDrive
    - References
    - SharePoint
    - Tips
    - Email
fmContentType: pages
date: 2025-01-26T06:42:13.247Z
lastmod: 2025-03-31T05:15:39.946Z
keywords:
    - Entra
    - Exchange
    - Microsoft 365
    - Tips
---

<!--- cSpell:disable --->
* [Licensing](#licensing)
* [Compliance and Security](#compliance-and-security)
* [URLs and Landing Zones](#urls-and-landing-zones)
  * [Login, Signin and App Specific URLs](#login-signin-and-app-specific-urls)
  * [App Specific URLs](#app-specific-urls)
  * [Logout URLs](#logout-urls)
  * [References](#references)
* [Microsoft 365 Language Settings](#microsoft-365-language-settings)
  * [Configuring Preferred Language for users](#configuring-preferred-language-for-users)
  * [Exchange Language Settings for end user via PowerShell](#exchange-language-settings-for-end-user-via-powershell)
  * [OneDrive Language Settings for end user via Web](#onedrive-language-settings-for-end-user-via-web)
  * [SharePoint Language Settings for end user via web](#sharepoint-language-settings-for-end-user-via-web)
  * [SharePoint or OneDrive Language Settings for enduser via PowerShell](#sharepoint-or-onedrive-language-settings-for-enduser-via-powershell)
* [Pre-create a users OneDrive](#pre-create-a-users-onedrive)
* [Force user to change password at next login](#force-user-to-change-password-at-next-login)
* [Exchange Email Header References](#exchange-email-header-references)
* [Finding the owner of a specifc MS Form](#finding-the-owner-of-a-specifc-ms-form)
* [Network Details Upload](#network-details-upload)
* [DSC](#dsc)
* [Entra](#entra)
  * [Microsoft Entra Connect Sync](#microsoft-entra-connect-sync)
  * [Microsoft Entra Cloud Sync](#microsoft-entra-cloud-sync)
* [Microsoft Graph](#microsoft-graph)
  * [Setting Data Storage Location for users](#setting-data-storage-location-for-users)
* [Diag Tools](#diag-tools)
<!--- cSpell:enable --->

## Licensing

**[Microsoft 365 Licensing Maps](https://m365maps.com)** - really really good site\
**[Compare Microsoft 365 Enterprise Plan](https://www.microsoft.com/en-au/microsoft-365/enterprise/microsoft365-plans-and-pricing)** - often used to compare\
**[Microsoft 365, Office 365, Enterprise Mobility + Security, and Windows 11 Subscriptions Comparison PDF](https://go.microsoft.com/fwlink/p/?LinkID=2139145&clcid=0xc09&culture=en-au&country=au)** - really good and contains lots of details about inclusions and add-ons

## Compliance and Security

[Microsoft Information Protection Deployment Accelerator Guide](https://microsoft.github.io/ComplianceCxE/dag/)

[Use Keyword Query Language to create search queries in eDiscovery](https://learn.microsoft.com/en-us/purview/edisc-keyword-query-language) - aka KeyQL (Doesn't looks to be the same as [KQL](kql-queries.md))\
[Use the condition builder to create search queries in eDiscovery](https://learn.microsoft.com/en-au/purview/edisc-condition-builder)\
[Keyword queries and search conditions for eDiscovery](https://learn.microsoft.com/en-au/purview/ediscovery-keyword-queries-and-search-conditions) - classic eDiscovery only apparently\
New Purview eDiscovery Guide: <https://mslearn.cloudguides.com/guides/Get%20started%20with%20Microsoft%20Purview%20eDiscovery>

More Info: [Learn about eDiscovery](https://learn.microsoft.com/en-au/purview/edisc)

## URLs and Landing Zones

### Login, Signin and App Specific URLs

Office.com\
<https://myapps.microsoft.com/>\
<https://portal.office.com/myapps>\
<https://www.office.com/login?domain_hint=myemaildomain.com>\
<https://www.office.com/signin?domain_hint=myemaildomain.com> ? I think login is better\
<https://www.office.com/?auth=2&home=1&username=myusername%40your-tenant-name.onmicrosoft.com&from=ShellLogo>\
<https://admin.microsoft.com/?auth_upn=myusename%40your-tenant-name.onmicrosoft.com&source=applauncher>\
<https://go.microsoft.com/fwlink/?LinkId=309629&tenantIdentifier=TENANTGUIDHERE>

<https://myapps.microsoft.com/myemaildomain.com>\
<https://manage.windowsazure.com/myemaildomain.com> - IT ONLY!\
<https://login.microsoftonline.com/?whr=myemaildomain.com> - BEST LINK?

### App Specific URLs

<https://portal.office.com/onedrive> - NEW Entry!\
<https://Your-Tenant-Name-my.sharepoint.com/_layouts/15/MyBraryFirstRun.aspx?FirstRunStage=waiting> - first run of OneDrive to setup\
<https://www.office.com/launch/sharepoint?auth=2> - NEW 2021\
<https://www.office.com/launch/onedrive>\
<https://www.office.com/launch/onenote>\
<https://www.office.com/launch/forms>\
<https://www.office.com/launch/word>\
<https://www.office.com/launch/excel>\
<https://www.office.com/launch/powerpoint>\
<https://www.office.com/launch/onenote>

<https://outlook.com/myemaildomain.com>\

### Logout URLs

<https://login.microsoftonline.com/common/oauth2/logoutsession>\
<https://www.office.com/estslogout?ru=%2F>\
<https://login.microsoftonline.com/logout.srf>\
<https://login.microsoftonline.com/common/oauth2/logout?post_logout_redirect_uri=https://www.office.com/signin?domain_hint=myemaildomain.com>

### References

* [End-user experiences for applications - Microsoft Entra ID - Microsoft Learn](https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/end-user-experiences)\
* [Add custom tiles to the app launcher - Microsoft 365 admin - Microsoft Learn](https://learn.microsoft.com/en-us/microsoft-365/admin/manage/customize-the-app-launcher?view=o365-worldwide)
* [Pin apps to your users' app launcher - Microsoft 365 admin - Microsoft Learn](https://learn.microsoft.com/en-us/microsoft-365/admin/manage/pin-apps-to-app-launcher?view=o365-worldwide)
* [Office 365 URLS and IP Address ranges](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US&fromAR=1) [AKA](https://aka.ms/o365endpoints)
* <https://github.com/adamfowlerit/msportals.io/issues/122#issuecomment-823661332>
* <https://docs.microsoft.com/en-us/azure/active-directory/manage-apps/configure-authentication-for-federated-users-portal#domain-hints>
* <https://techcommunity.microsoft.com/t5/azure-active-directory-identity/using-azure-ad-to-land-users-on-their-custom-login-page-from/ba-p/243900>
* 12/10/23: MORE <https://learn.microsoft.com/bs-latn-ba/azure/active-directory/manage-apps/end-user-experiences#direct-sign-on-links> from
  * [End-user experiences for applications - Microsoft Entra - Microsoft Learn](https://learn.microsoft.com/bs-latn-ba/azure/active-directory/manage-apps/end-user-experiences)

## Microsoft 365 Language Settings

<https://myaccount.microsoft.com/settingsandprivacy/language>

### Configuring Preferred Language for users

**<https://learn.microsoft.com/en-au/microsoft-365/troubleshoot/access-management/set-language-and-region>**

```powershell
# Update the User's Preferred Language details. Assumes Microsoft.Graph.Users or Microsoft.Graph module is already installed.
Import-Module Microsoft.Graph.Users

Connect-MgGraph  -Scopes 'User.ReadWrite.All'

$preferredLanguage = 'en-au'
$userId = Get-MgUser -UserId user1@contoso.com
Update-MgUser -UserId $userId.Id -PreferredLanguage $preferredLanguage
```

> [!IMPORTANT] Synchronized identity model
> If you are using ADSync or AD Connect Sync or Entra Connect Sync or whatever the hell they are calling it now, you **can't** set the above setting in M365.
> It must be set in AD (but I don't think its a drop down option). Per the MS KB Above you can use this:
> `Set-ADUser samacccountname -replace @{PreferredLanguage="en-au"}` then wait for it to sync to 365

See [Installing Modules in PowerShell Tips](powershell-tips.md#installing-modules) and [Module Management in PowerShell Commands](powershell-commands.md#module-management)

### Exchange Language Settings for end user via PowerShell

`Set-MailboxRegionalConfiguration -Identity $upn -Language 3081 -TimeZone "AUS Eastern Standard Time" -DateFormat "d/MM/yyyy"`\
<https://learn.microsoft.com/en-au/powershell/module/exchange/set-mailboxregionalconfiguration?view=exchange-ps>

> [!TIP] TIP
> Graph may be able to do the same but I haven't looked into it yet. For those who are keen you can look into: [Update-MgUserMailboxSetting](https://learn.microsoft.com/en-us/powershell/module/microsoft.graph.users/update-mgusermailboxsetting?view=graph-powershell-1.0)

### OneDrive Language Settings for end user via Web

<https://Your-Tenant-Name-my.sharepoint.com/?p=22&setting=1> and click 'Regional Settings'

### SharePoint Language Settings for end user via web

1. Go to <https://Your-Tenant-Name-my.sharepoint.com/_layouts/15/editprofile.aspx?UserSettingsProvider=dfb95e82-8132-404b-b693-25418fdac9b6>
2. Select the 3 dots next to 'Details'
3. Select 'Language and Region'

> [!TIP] TIP
> If you do the [Configuring Preferred Language for users](#configuring-preferred-language-for-users), then the [Exchange Language Settings for end user via PowerShell](#exchange-language-settings-for-end-user via PowerShell) then [OneDrive Language Settings for end user via web](#onedrive-language-settings-for-end-user-via-web) first, this one should already be done for you!

Based off <https://support.microsoft.com/en-US/office/change-sharepoint-online-language-settings-0f6a477a-dcab-4462-9d0c-e3b53d138183> - this article isn't updated for CoPilot additions/changes. You need to click the 'You can add more profile information here.' link. Will end up taking you to <https://Your-Tenant-Name-my.sharepoint.com/_layouts/15/editprofile.aspx?UserSettingsProvider=dfb95e82-8132-404b-b693-25418fdac9b6>

This can affect things like validation. Refer to [Validation Tips](sharepoint-references.html#validation-tips)

### SharePoint or OneDrive Language Settings for enduser via PowerShell

<https://pnp.github.io/script-samples/spo-set-sharepoint-regional-settings/README.html?tabs=pnpps>\

<https://pkbullock.com/blog/2020/the-many-ways-to-set-uk-locale-in-sharepoint/> - I think this example has a bug or two but its where the above but it gives you an idea on other options.

Refer to [PnP PowerShell in SharePoint References](sharepoint-references.md#pnp-powershell) for more info on PnPPowerShell

## Pre-create a users OneDrive

<https://learn.microsoft.com/en-us/powershell/module/sharepoint-online/request-spopersonalsite?view=sharepoint-ps>

```powershell
Import-Module Microsoft.Online.SharePoint.PowerShell
Connect-SPOService -Url https://<<YOUR_TENANT_NAME>>-admin.sharepoint.com

$emails = "user1@contoso.com", "user2@contoso.com"
Request-SPOPersonalSite -UserEmails $emails
Disconnect-SPOService
```

* Max 200 Users
* Variable cannot have any empty strings
* Not MultiGeo aware

See more info about SharePoint PowerShell in [SharePoint References](sharepoint-references.md#connect-via-sharepoint-online-powershell)

## Force user to change password at next login

```powershell
# Set user account to change password on next login. Assumes Microsoft.Graph.Users or Microsoft.Graph module is already installed.
Import-Module Microsoft.Graph.Users

Connect-MgGraph  -Scopes 'User.ReadWrite.All'
$userId = Get-MgUser -UserId "user1@contoso.com"

Update-MgUser -UserId $userid.id -PasswordProfile @{ ForceChangePasswordNextSignIn = $true }
```

## Exchange Email Header References

<https://learn.microsoft.com/en-us/defender-office-365/message-headers-eop-mdo>\
<https://learn.microsoft.com/en-us/exchange/header-firewall-exchange-2013-help>\
<https://learn.microsoft.com/en-us/exchange/anti-spam-stamps-exchange-2013-help>

**<https://mha.azurewebsites.net>**

More Mail header info at [Mail Headers](mail-headers.md)

More Mail tools under [Postmaster Tools in Misc Tools](misc-tools.md#postmaster) and Standards links under [SMTP in Misc References](misc-references.md#smtp)

## Finding the owner of a specifc MS Form

<https://itspartlycloudy.com/2022/01/20/who-created-this-microsoft-form/>\
<https://techcommunity.microsoft.com/discussions/microsoftforms/how-to-find-out-who-created-a-form/1325365/replies/4014059>
<https://techcommunity.microsoft.com/discussions/microsoftforms/how-to-find-out-who-created-a-form/1325365/replies/3050250#M10414>

## Network Details Upload

<https://learn.microsoft.com/en-us/microsoft-365/enterprise/office-365-network-mac-perf-overview>

<https://learn.microsoft.com/en-au/microsoft-365/enterprise/office-365-network-mac-perf-overview#csv-import-for-lan-subnet-office-locations>

1. Download CSV
2. Edit for accuracy, then upload.

<https://connectivity.office.com/> -  Microsoft 365 network connectivity test\

Also:
<https://learn.microsoft.com/en-us/microsoftteams/cqd-upload-tenant-building-data>\
[Call Quality Dashboard Tenant Data Upload](https://cqd.teams.microsoft.com/spd/#/TenantDataUpload)
<!--- cSpell:words PSTN -->
<https://learn.microsoft.com/en-us/microsoftteams/location-based-routing-configure-network-settings> - while this is more for teams calling (PSTN Voice), I've found it gives other parts of teams more context about issues.

## DSC

<https://microsoft365dsc.com/>

## Entra

> [!NOTE] Size
> This section may become big enough that it will become its own page.

<https://entra.news/>\
<https://entra.news/p/entra-mind-maps> - entra mind map\
<https://github.com/merill/awesome-entra> - Github awesome list for Entra\
<https://azuread.github.io/MSIdentityTools/>\
<https://graphxray.merill.net/>

<https://learn.microsoft.com/en-us/troubleshoot/entra/entra-id/governance/verify-first-party-apps-sign-in> Verify First Party App ID's\
<https://github.com/MicrosoftDocs/entra-docs/blob/main/.docutune/dictionaries/known-guids.json> - Github List of known IDs\
<https://github.com/merill/microsoft-info/> - contains app GUIDs and permission GUIDs\
<https://raw.githubusercontent.com/merill/microsoft-info/main/_info/MicrosoftApps.json>

### Microsoft Entra Connect Sync

<https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/whatis-azure-ad-connect-v2>\
<https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/reference-connect-adsync>

Syncs:
<https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/reference-connect-adsync#start-adsyncsynccycle>\
**Force Delta Sync: `Start-AdSyncSyncCycle -PolicyType Delta`**\
Full Sync: `Start-AdSyncSyncCycle -PolicyType Delta` - I don't know why but I don't like doing full syncs from PowerShell, only from the interface.\
<https://techcommunity.microsoft.com/blog/itopstalkblog/powershell-basics-how-to-force-azuread-connect-to-sync/887043>\
<https://lazyadmin.nl/it/force-azure-ad-sync-delta/>

* [ ] Add in guidance and abuse notes around this.

AutoUpgrade:
<https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-install-automatic-upgrade> - contains overview and troubleshooting details - including event log events to look out for.

> [!TIP] Azure AD Connect Upgrade Event source
> If you can't find the event log source `Microsoft Entra Connect Upgrade` it might be under its oldername `Azure AD Connect Upgrade`

<https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/reference-connect-adsync#get-adsyncautoupgrade>\
`Get-ADSyncAutoUpgrade`\
`Get-ADSyncAutoUpgrade -Detail`\
<https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/reference-connect-adsync#set-adsyncautoupgrade>\
`Set-ADSyncAutoUpgrade -AutoUpgradeState Enabled`\
`Set-ADSyncAutoUpgrade [-AutoUpgradeState] <AutoUpgradeConfigurationState> [[-SuspensionReason] <String>] [<CommonParameters>]`

<https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/reference-connect-version-history>\
<https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/reference-connect-health-version-history>\
<https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/reference-connect-version-history-archive>

### Microsoft Entra Cloud Sync

<https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/what-is-cloud-sync>

## Microsoft Graph

**<https://aka.ms/GE> - MS Graph Explorer**

* [ ] Add in MS Graph Stuff

Places you will see graph references:

* [PowerShell Commands](powershell-commands.md)

### Setting Data Storage Location for users

```powershell
# Update User's Usage Location details. Assumes Microsoft.Graph.Users or Microsoft.Graph module is already installed.
Import-Module Microsoft.Graph.Users

Connect-MgGraph  -Scopes 'User.ReadWrite.All'

$usageLocation = 'AU'
$userId = Get-MgUser -UserId user1@contoso.com
Update-MgUser -UserId $userId.Id -Usagelocation $usageLocation
```

See [Installing Modules in PowerShell Tips](powershell-tips.md#installing-modules) and [Module Management in PowerShell Commands](powershell-commands.md#module-management)

## Diag Tools

[Enterprise Version of Microsoft Support and Recovery Assistant](https://www.microsoft.com/en-au/download/details.aspx?id=103391)\
<https://support.microsoft.com/en-au/windows/microsoft-365-troubleshooters-486d7956-6a21-4c75-bc4f-0704077c583c> - NEW SARA\
<https://support.microsoft.com/en-au/windows/running-troubleshooters-in-get-help-23bddffd-5495-47f6-a419-7efe166bf1a8> - Other MS Troubleshooters some of which may be still useful
