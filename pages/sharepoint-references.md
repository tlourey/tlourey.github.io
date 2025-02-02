---
title: SharePoint References
description: '"SharePoint is old pig in lipstick, wearing trendy clothes and trying to fit in with the young kids" - Me'
published: true
categories:
    - Tech
type: pages
layout: pages
draft: true
tags:
    - SharePoint
    - References
fmContentType: pages
lastmod: 2025-02-02T13:45:47.045Z
date: 2025-01-28T05:47:28.059Z
---

<!--- cSpell:disable --->
* [Good points to remember](#good-points-to-remember)
* [Concepts](#concepts)
  * [SharePoint (Online) Hierarchy](#sharepoint-online-hierarchy)
  * [Copy vs Move](#copy-vs-move)
* [Validation Tips](#validation-tips)
* [SharePoint Formulas](#sharepoint-formulas)
  * [Common Formulas](#common-formulas)
* [Audience Targeting](#audience-targeting)
* [Styling and Theming](#styling-and-theming)
  * [Theming](#theming)
  * [Custom Theming](#custom-theming)
* [Tools](#tools)
  * [SharePoint Online PowerShell](#sharepoint-online-powershell)
    * [Install SharePoint Online PowerShell](#install-sharepoint-online-powershell)
    * [Connect via SharePoint Online PowerShell](#connect-via-sharepoint-online-powershell)
  * [PnP PowerShell](#pnp-powershell)
    * [Installing](#installing)
    * [Connecting](#connecting)
  * [PnP Provisioning Engine](#pnp-provisioning-engine)
  * [CSOM](#csom)
* [Permissions](#permissions)
* [Site Collection Features](#site-collection-features)
* [Formatting](#formatting)
  * [Lists and Views](#lists-and-views)
    * [Formatting JSON Schemas](#formatting-json-schemas)
  * [Columns](#columns)
* [BrandCentre](#brandcentre)
* [Training](#training)
* [Microsoft Lists](#microsoft-lists)
* [Teams and SharePoint](#teams-and-sharepoint)
* [Specific Articles to save](#specific-articles-to-save)
  * [Disabling Comments and Social Bar (for one site only)](#disabling-comments-and-social-bar-for-one-site-only)
* [References](#references)
  * [High Level](#high-level)
  * [Adoption](#adoption)
  * [Microsoft 365 Community Content](#microsoft-365-community-content)
  * [Misc Sites](#misc-sites)
* [TODO](#todo)
<!--- cSpell:enable --->

## Good points to remember

> *"SharePoint has many personas and personalities"* - An Ex CIO turned aviation consultant

> *"SharePoint is not as forgiving as \[some other platforms like\] Confluence"* - A CIO I worked with

> *"SharePoint is old pig in lipstick, wearing trendy clothes and trying to fit in with the young kids"* - Me

## Concepts

* SharePoint Online via Microsoft 365 vs SharePoint On-Prem
* [SharePoint Lists Vs Libraries](https://sharepointmaven.com/lists-vs-libraries-in-sharepoint-online/)
* There is List/Library Validation and Column Validation
  * Column validation only works for new data entries [^1]
  * List/Library Validation ensures that the data was entered correctly with respect to other columns in the list or library. [^1]
  * A big limitation of the Column Validation I mentioned above is that you can not reference other columns. This is where the list/library validation comes into play. [^1]
* [Site-Wide Column vs Library Column](https://learn.microsoft.com/en-au/microsoft-365/community/list-column-or-site-column-which-one-to-choose)
* Audience Targeting is more about showing/not showing/promoting content and isn't really security
* Hubs vs Sites
* Modern vs Classic
* Comm Sites vs Team Sites
* News posts vs Pages
* Roll up
* Hierarchy
* Copy to vs Move To issues when enforcing uniqueness

[^1]: <https://sharepointmaven.com/how-to-do-column-validation-in-sharepoint/>

### SharePoint (Online) Hierarchy

[![Picture](https://learn.microsoft.com/en-us/sharepoint/sharepointonline/media/b7cf87f3-578c-4605-bb31-9d2ecf88877e.png)](https://learn.microsoft.com/en-us/sharepoint/sharepointonline/media/b7cf87f3-578c-4605-bb31-9d2ecf88877e.png)

The above diagram is from a MS Learn page about permissions but excluding Hubs, it still shows the correct order. Note that a Document Library is almost the same as List library except its around files and not list items.

### Copy vs Move

<https://support.microsoft.com/en-au/office/move-or-copy-files-in-sharepoint-00e2f483-4df3-46be-a861-1f5f0c1a87bc>

* When you use **Move to**, the **history** of the document **is copied** to the new destination.
* When you use **Copy to** with documents that have version **history**, **only the latest version is copied**.
* To copy earlier versions, you need to restore and copy each one. For more info about versioning, see [Enable and configure versioning for a list or library](https://support.microsoft.com/en-au/office/enable-and-configure-versioning-for-a-list-or-library-1555d642-23ee-446a-990a-bcab618c7a37)

If you have a column that has 'enforce unique values' enabled in your destination library:

* When you try to **Move \[to\]** a document from one Document Library to a destination library that has enforce unique values enabled, the move will fail
* When you **Copy \[to\]** a document from one Document Library to a destination library that has enforce unique values enabled, the file will copy but the meta data won't.

  > The Move to operation will fail if you attempt to move the document across libraries and the destination has enforced unique values.[^2]

[^2]: <https://support.microsoft.com/en-au/office/move-or-copy-files-in-sharepoint-00e2f483-4df3-46be-a861-1f5f0c1a87bc#:~:text=The%C2%A0Move%20to%20operation%20will%20fail%20if%20you%20attempt%20to%20move%20the%20document%20across%20libraries%20and%20the%20destination%20has%20enforced%20unique%20values>.

## Validation Tips

* If you're having trouble with the formulas try going into the library settings --> Advanced settings then select the column and enter the formula in the classic style interface.
* Today() and Now() seem to not always follow the timezone of the sharepoint site. Google for fixes. They are just semi-shitty workarounds like adding using created/modified dates or doing math to the today function.
  * <https://answers.microsoft.com/en-us/msoffice/forum/all/sharepoint-today-function-not-showing-correct-date/7d094e83-2a60-4d53-b06b-73c575008035> (expand to see app replies)

Consider if the regional, language or timezone settings are set which can import this. refer to [SharePoint Language Settings for end user](microsoft-365-tips.md#sharepoint-language-settings-for-end-user) and [SharePoint Language Settings for end user](microsoft-365-tips.md#onedrive-language-settings-for-end-user)

Also remember each site has its own regional settings in Site settings which also have a language and timezone setting.

## SharePoint Formulas

[Examples of common formulas in lists](https://support.microsoft.com/en-us/office/examples-of-common-formulas-in-lists-d81f5f21-2b4e-45ce-b170-bf7ebf6988b3)\
<https://learn.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN>

### Common Formulas

`=[My Column Name] > TODAY()`: Column name must be greater than today's date.
`=[My Column Name] <= TODAY()`: Column name must be less than or equal to today's date.

## Audience Targeting

<https://support.microsoft.com/en-au/office/target-content-to-a-specific-audience-on-a-sharepoint-site-68113d1b-be99-4d4c-a61c-73b087f48a81>

> [!TIP]
> Audience Targeting doesn't work with SharePoint groups, only AD, AAD, M365 etc

## Styling and Theming

<https://lookbook.microsoft.com/>

### Theming

TBC

### Custom Theming

Create Custom Theming for SharePoint site or hub using <https://www.aka.ms/themedesigner>

1. Set Primary Colour
2. Set Text Colour
3. Set Background Colour
4. Check how it looks
5. Click Export Theme
6. Create a PowerShell File (assumes [SharePoint Online PowerShell](#sharepoint-online-powershell) already installed)

   ```powershell
   $themepalette = @.... # paste the contents of the exported theme file
   Import-Module -Name Microsoft.Online.SharePoint.PowerShell
   Connect-SPOService -Url https://<<YOUR_TENANT_NAME>>-admin.sharepoint.com
   Add-SPOTheme -Identity "My custom theme" -Palette $themepalette -IsInverted $false -Whatif
       Add-SPOTheme -Identity "My custom theme" -Palette $themepalette -IsInverted $false -Confirm
   Disconnect-SPOService
   ```

More Info: <https://learn.microsoft.com/en-us/sharepoint/dev/declarative-customization/site-theming/sharepoint-site-theming-powershell>

## Tools

### SharePoint Online PowerShell

<https://learn.microsoft.com/en-us/powershell/sharepoint/sharepoint-online/introduction-sharepoint-online-management-shell?view=sharepoint-ps>\
<https://learn.microsoft.com/en-us/powershell/sharepoint/sharepoint-online/connect-sharepoint-online?view=sharepoint-ps>\
<https://learn.microsoft.com/en-us/powershell/module/sharepoint-online/?view=sharepoint-ps>

> [!TIP]
> **Gallery Module Easier**\
> Rather than download and install the MSI its easier to install and manage the SharePoint Online PowerShell Module via PowerShell Gallery

#### Install SharePoint Online PowerShell

> [!TIP]
> **PS5 not PS7**\
> this module only seems to work in PS5/Windows PowerShell.

```powershell
Install-Module -Name Microsoft.Online.SharePoint.PowerShell
# OR for no admin rights
Install-Module -Name Microsoft.Online.SharePoint.PowerShell -Scope CurrentUser
# To update already installed
Update-Module -Name Microsoft.Online.SharePoint.PowerShell
```

#### Connect via SharePoint Online PowerShell

With MFA:

`Connect-SPOService -Url https://contoso-admin.sharepoint.com`

> [!NOTE]
> There is a known issue between the SharePoint Online Management Shell module and SharePoint Client Components SDK where the module will fail to load if both are installed on the same computer. If you encounter this issue, uninstall the SharePoint Client Components SDK.

### PnP PowerShell

[PnP PowerShell Intro](https://learn.microsoft.com/en-au/powershell/sharepoint/sharepoint-pnp/sharepoint-pnp-cmdlets?view=sharepoint-ps)\
[PnP PowerShell](https://pnp.github.io/powershell/index.html)\
[PnP PowerShell Cmdlets](https://pnp.github.io/powershell/cmdlets/index.html)

#### Installing

```powershell
Install-Module PnP.PowerShell -Scope CurrentUser
```

If it hasn't been used in the tenant before

```powershell
Import-Module PnP.PowerShell
Register-PnPEntraIDAppForInteractiveLogin -ApplicationName "PnP Rocks" -Tenant [yourtennantnamehere].onmicrosoft.com -Interactive
```

> [!TIP]
> **Whats in a name**\
> You can change the name away from PnP Rocks to something else if you want just note it and the application id down.

#### Connecting

<https://pnp.github.io/powershell/articles/authentication.html>

```powershell
Connect-PnPOnline [yourtenant].sharepoint.com -Interactive -ClientId <client id of your Entra ID Application Registration>
# OR
Connect-PnPOnline [yourtenant].sharepoint.com -DeviceLogin -Tenant <tenant>.onmicrosoft.com -ClientId <client id of your Entra ID Application Registration>
```

### PnP Provisioning Engine

<https://learn.microsoft.com/en-us/sharepoint/dev/solution-guidance/introducing-the-pnp-provisioning-engine>\
<https://learn.microsoft.com/en-us/sharepoint/dev/solution-guidance/applying-pnp-templates>

### CSOM

CSOM: Client-Side Object Model

[Download SharePoint Online Client Components SDK](https://www.microsoft.com/en-us/download/details.aspx?id=42038)\
<https://www.sharepointdiary.com/2019/04/connect-to-sharepoint-online-using-csom-powershell.html>\
<https://www.sharepointdiary.com/2019/08/connect-sharepoint-online-powershell-using-mfa.html> - contains section on connecting with CSOM and MFA

More Info:\
<https://learn.microsoft.com/en-us/sharepoint/dev/general-development/get-started-using-the-client-object-model-with-external-data-in-sharepoint>\
<https://learn.microsoft.com/en-us/sharepoint/dev/sp-add-ins/complete-basic-operations-using-sharepoint-client-library-code>\
<https://learn.microsoft.com/en-us/sharepoint/dev/sp-add-ins-modernize/from-csom-to-pnp-libraries>

## Permissions

**<https://learn.microsoft.com/en-us/sharepoint/understanding-permission-levels>** - should refer to this more often\
<https://learn.microsoft.com/en-us/sharepoint/what-is-permissions-inheritance>\
<https://learn.microsoft.com/en-us/sharepoint/modern-experience-sharing-permissions>\
<https://support.microsoft.com/en-au/office/customize-permissions-for-a-sharepoint-list-or-library-02d770f3-59eb-4910-a608-5f84cc297782>

<https://www.reddit.com/r/sharepoint/comments/1c67ms4/create_items_in_libraries_but_not_new_libraries/>

<https://sharegate.com/blog/sharepoint-permissions-best-practices-2-ways-to-manage>\
<https://www.sharepointdiary.com/2013/04/sharepoint-permission-levels.html>

<https://learn.microsoft.com/en-us/sharepoint/change-external-sharing-site>\
<https://learn.microsoft.com/en-us/sharepoint/change-default-sharing-link>

> [!NOTE]
> To change the default link type for a Teams private or shared channel site, you must use the [Set-SPOSite](https://learn.microsoft.com/en-us/powershell/module/sharepoint-online/set-sposite?view=sharepoint-ps) PowerShell cmdlet.

## Site Collection Features

<https://support.microsoft.com/en-au/office/enable-or-disable-site-collection-features-a2f2a5c2-093d-4897-8b7f-37f86d83df04>

## Formatting

### Lists and Views

<https://support.microsoft.com/en-us/office/formatting-list-views-f737fb8b-afb7-45b9-b9b5-4505d4427dd1>\
<https://learn.microsoft.com/en-gb/sharepoint/dev/declarative-customization/view-formatting>\
<https://learn.microsoft.com/en-us/sharepoint/dev/declarative-customization/view-commandbar-formatting>

<https://pnp.github.io/List-Formatting/>\
<https://pnp.github.io/List-Formatting/tools/> - I haven't used this yet but it looks like it might be useful

#### Formatting JSON Schemas

<https://developer.microsoft.com/json-schemas/sp/v2/row-formatting.schema.json>\
<https://developer.microsoft.com/json-schemas/sp/v2/command-bar-formatting.schema.json>

### Columns

<https://support.microsoft.com/en-us/office/column-formatting-with-json-1f927342-2bed-4745-b727-ff8b7ff96b22>

## BrandCentre

<https://learn.microsoft.com/en-us/sharepoint/brand-center-overview>

## Training

<https://learn.microsoft.com/en-us/sharepoint/training-change-management>

* [ ] Add more of the links from the above
* [ ] Add links to adoption resources

## Microsoft Lists

* [ ] Add MS Lists Adoption resources

<https://learn.microsoft.com/en-us/sharepoint/control-lists>\
<https://learn.microsoft.com/en-us/sharepoint/lists-sync-policies> - windows\
<https://learn.microsoft.com/en-us/sharepoint/lists-sync-policies-macos> - mac

## Teams and SharePoint

<https://learn.microsoft.com/en-us/sharepoint/teams-connected-sites>

## Specific Articles to save

<https://techcommunity.microsoft.com/discussions/sharepoint_general/remove-items-in-new-button/3886747> - good tips on customising new button at site level.\
<https://techcommunity.microsoft.com/discussions/sharepoint_general/hide-folder-and-template-under-upload-on-sharepoint-document-library/3874653> - for use in advanced view formatting\
<https://www.reddit.com/r/sharepoint/comments/1c67ms4/create_items_in_libraries_but_not_new_libraries/>\
<https://sharepointmaven.com/how-to-copy-an-existing-document-library-in-sharepoint-online/> - also includes how to get around a very obscure error if you have audience targeting enabled on a the library.\
<https://learn.microsoft.com/en-us/answers/questions/1367728/how-do-you-use-powershell-to-copy-a-sharepoint-onl>\
**<https://stackoverflow.com/questions/78491086/get-pnpsitetemplate-gets-stuck-for-a-long-time-on-certain-handlers> - sometimes running PnP Commands in VSCode has strange issues**

### Disabling Comments and Social Bar (for one site only)

To disable comments and/or the social bar for a **specific site only** and not for the whole Tenant using PnP PowerShell (after connecting)

```powershell
Import-Module PnP.PowerShell
$SiteURL = https://tenantname.sharepoint.com/sites/comms-site-i-want-comments-and-likes-disabled-on
# Ensure Site URL does *not* have a trailing slash
connect-PnPOnline $siteUrl -DeviceLogin -Tenant yourtenantnamehere.onmicrosoft.com -ClientId <<PnP App ID GUID for your AAD here>>

Set-PnPSite -Identity $SiteURL -SocialBarOnSitePagesDisabled $True -CommentsOnSitePagesDisabled $True
```

More Info: [https://pnp.github.io/powershell/cmdlets/Set-PnPSite.html]

[Disable "Comments, Likes and Views" in SharePoint modern - Microsoft Community - includes social graph per site](https://answers.microsoft.com/en-us/msoffice/forum/all/disable-comments-likes-and-views-in-sharepoint/c523e324-e95e-4ace-b859-85782afc8135)
[SharePoint Online: Disable Page Comments in Modern Sites using PowerShell - SharePoint Diary - powershell per site](https://www.sharepointdiary.com/2018/11/sharepoint-online-disable-page-comments-using-powershell.html)
<https://sharepointmaven.com/2-ways-to-disable-modern-page-comments/>\
<https://sharepoint.stackexchange.com/questions/274969/remove-social-and-comments-footer-from-spo-site-page>

## References

### High Level

<https://learn.microsoft.com/en-us/sharepoint/information-architecture-modern-experience>

### Adoption

<https://adoption.microsoft.com/en-us/microsoft-lists/>\
<https://adoption.microsoft.com/en-us/microsoft-lists/resources/>\
<https://adoption.microsoft.com/en-us/sharepoint/>

### Microsoft 365 Community Content

[Site Builder/Owner: New Site Checklist](https://learn.microsoft.com/en-us/microsoft-365/community/new-site-checklist)\
<https://pnp.github.io/> - Microsoft 365 & Power Platform Community - used to be called Patterns and Practices. Make some good tools like PnP Tools for SharePoint/O365 plus a tonne of samples.

### Misc Sites

**<https://sharepointmaven.com/>** - really good\
<https://www.sharepointdiary.com/> - older but still ok.

## TODO

* [ ] Reorder topics
* [ ] Bring in links from process documents
* [ ] Look into lockdown mode
