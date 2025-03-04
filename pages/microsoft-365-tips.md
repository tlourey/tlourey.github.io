---
title: Microsoft 365 Tips
description: Bottomless pit
published: true
categories:
    - Tech
type: pages
layout: pages
draft: true
tags:
    - Entra
    - Exchange
    - Microsoft365
    - Office
    - OneDrive
    - References
    - SharePoint
    - Tips
fmContentType: pages
date: 2025-01-26T06:42:13.247Z
lastmod: 2025-03-01T06:04:04.417Z
---

<!--- cSpell:disable --->
* [URLs and Landing Zones](#urls-and-landing-zones)
  * [Login, Signin and App Specific URLs](#login-signin-and-app-specific-urls)
  * [App Specific URLs](#app-specific-urls)
  * [Logout URLs](#logout-urls)
  * [References](#references)
* [SharePoint Language Settings for end user](#sharepoint-language-settings-for-end-user)
* [OneDrive Language Settings for end user](#onedrive-language-settings-for-end-user)
* [Microsoft 365 Language Settings](#microsoft-365-language-settings)
* [Network Details Upload](#network-details-upload)
* [DSC](#dsc)
* [Entra](#entra)
* [Diag Tools](#diag-tools)
<!--- cSpell:enable --->

## URLs and Landing Zones

### Login, Signin and App Specific URLs

Office.com
<https://myapps.microsoft.com/>\
<https://portal.office.com/myapps>\
<https://www.office.com/login?domain_hint=myemaildomain.com>\
<https://www.office.com/signin?domain_hint=myemaildomain.com> ? I think login is better\
<https://www.office.com/?auth=2&home=1&username=myusername%40yourtenantname.onmicrosoft.com&from=ShellLogo>\
<https://admin.microsoft.com/?auth_upn=myusename%40yourtenantname.onmicrosoft.com&source=applauncher>\
<https://go.microsoft.com/fwlink/?LinkId=309629&tenantIdentifier=TENANTGUIDHERE>

<https://myapps.microsoft.com/myemaildomain.com>\
<https://manage.windowsazure.com/myemaildomain.com> - IT ONLY!\
<https://login.microsoftonline.com/?whr=myemaildomain.com> - BEST LINK?

### App Specific URLs

<https://portal.office.com/onedrive> - NEW Entry!\
<https://mytenantname-my.sharepoint.com/_layouts/15/MyBraryFirstRun.aspx?FirstRunStage=waiting> - first run of OneDrive to setup\
<https://www.office.com/launch/sharepoint?auth=2> - NEW 2021
<https://www.office.com/launch/onedrive>
<https://www.office.com/launch/onenote>
<https://www.office.com/launch/forms>
<https://www.office.com/launch/word>
<https://www.office.com/launch/excel>
<https://www.office.com/launch/powerpoint>
<https://www.office.com/launch/onenote>

<https://outlook.com/myemaildomain.com>\

### Logout URLs

<https://login.microsoftonline.com/common/oauth2/logoutsession>
<https://www.office.com/estslogout?ru=%2F>
<https://login.microsoftonline.com/logout.srf>
<https://login.microsoftonline.com/common/oauth2/logout?post_logout_redirect_uri=https://www.office.com/signin?domain_hint=myemaildomain.com>

### References

* [End-user experiences for applications - Microsoft Entra ID | Microsoft Learn](https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/end-user-experiences)
* [Add custom tiles to the app launcher - Microsoft 365 admin | Microsoft Learn](https://learn.microsoft.com/en-us/microsoft-365/admin/manage/customize-the-app-launcher?view=o365-worldwide)
* [Pin apps to your users' app launcher - Microsoft 365 admin | Microsoft Learn](https://learn.microsoft.com/en-us/microsoft-365/admin/manage/pin-apps-to-app-launcher?view=o365-worldwide)
* [Office 365 URLS and IP Address ranges](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US&fromAR=1) [AKA](https://aka.ms/o365endpoints)
* <https://github.com/adamfowlerit/msportals.io/issues/122#issuecomment-823661332>
* <https://docs.microsoft.com/en-us/azure/active-directory/manage-apps/configure-authentication-for-federated-users-portal#domain-hints>
* <https://techcommunity.microsoft.com/t5/azure-active-directory-identity/using-azure-ad-to-land-users-on-their-custom-login-page-from/ba-p/243900>
* 12/10/23: MORE <https://learn.microsoft.com/bs-latn-ba/azure/active-directory/manage-apps/end-user-experiences#direct-sign-on-links> from
  * [End-user experiences for applications - Microsoft Entra | Microsoft Learn](https://learn.microsoft.com/bs-latn-ba/azure/active-directory/manage-apps/end-user-experiences)

## SharePoint Language Settings for end user

Based off <https://support.microsoft.com/en-US/office/change-sharepoint-online-language-settings-0f6a477a-dcab-4462-9d0c-e3b53d138183> - this article isn't update for copilot. you need to click the 'You can add more profile information here.' link. Will take you to go <https://tenant-name-here-my.sharepoint.com/_layouts/15/editprofile.aspx?UserSettingsProvider=dfb95e82-8132-404b-b693-25418fdac9b6>

This can affect things like validation. Refer to [Validation Tips](sharepoint-references.html#validation-tips)

## OneDrive Language Settings for end user

<https://tenant-name-here-my.sharepoint.com/?p=22&setting=1>

## Microsoft 365 Language Settings

<https://myaccount.microsoft.com/settingsandprivacy/language>

* [ ] include tip about presetting office 365, sharepoint and exchange language, region and timezone settings

## Network Details Upload

<https://learn.microsoft.com/en-us/microsoft-365/enterprise/office-365-network-mac-perf-overview>

<https://learn.microsoft.com/en-au/microsoft-365/enterprise/office-365-network-mac-perf-overview#csv-import-for-lan-subnet-office-locations>

1. Download CSV
2. Edit for accuracy, then upload.

<https://connectivity.office.com/> -  Microsoft 365 network connectivity test\

Also:
<https://learn.microsoft.com/en-us/microsoftteams/cqd-upload-tenant-building-data>\
[Call Quality Dashboard Tenant Data Upload](https://cqd.teams.microsoft.com/spd/#/TenantDataUpload)

<https://learn.microsoft.com/en-us/microsoftteams/location-based-routing-configure-network-settings> - while this is more for teams routing i've found it gives other parts of teams more context about issues.

## DSC

<https://microsoft365dsc.com/>

## Entra

> [!NOTE] Size
> This section may become big enough that it will become its own page.

<https://entra.news/>\
<https://github.com/merill/awesome-entra> - Github awesome list for Entra\
<https://azuread.github.io/MSIdentityTools/>\
<https://graphxray.merill.net/>

<https://learn.microsoft.com/en-us/troubleshoot/entra/entra-id/governance/verify-first-party-apps-sign-in> Verify First Party App ID's\
<https://github.com/MicrosoftDocs/entra-docs/blob/main/.docutune/dictionaries/known-guids.json> - Github List of known IDs\
<https://github.com/merill/microsoft-info/> - contains app GUIDs and permission GUIDs\
<https://raw.githubusercontent.com/merill/microsoft-info/main/_info/MicrosoftApps.json>

## Diag Tools

[Enterprise Version of Microsoft Support and Recovery Assistant](https://www.microsoft.com/en-au/download/details.aspx?id=103391)\
<https://support.microsoft.com/en-au/windows/microsoft-365-troubleshooters-486d7956-6a21-4c75-bc4f-0704077c583c> - NEW SARA
<https://support.microsoft.com/en-au/windows/running-troubleshooters-in-get-help-23bddffd-5495-47f6-a419-7efe166bf1a8> - Other MS Troubleshooters some of which may be still useful
