---
title: SharePoint References
description: ""
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
lastmod: 2025-01-26T07:05:42.558Z
---

<!--- cSpell:disable --->
* [Good points to remember](#good-points-to-remember)
* [Concepts](#concepts)
* [Validation Tips](#validation-tips)
* [SharePoint Formulas](#sharepoint-formulas)
  * [Common Formulas](#common-formulas)
* [Audience Targeting](#audience-targeting)
* [Styling and Theming](#styling-and-theming)
  * [Theming](#theming)
    * [Custom Theming](#custom-theming)
  * [Connect to SharePoint Online](#connect-to-sharepoint-online)
* [Good sites](#good-sites)
  * [Microsoft 365 Community Content](#microsoft-365-community-content)
  * [Misc](#misc)
<!--- cSpell:enable --->

## Good points to remember

> *"SharePoint has many personas and personalities"* - An Ex CIO turned aviation consultant

> *"SharePoint is not as forgiving as \[some other platforms like\] Confluence"* - A CIO I worked with

> *"SharePoint is old pig in lipstick but wearing trendy clothes and hanging out with the young kids"* - Me

## Concepts

* SharePoint Online via Microsoft 365 vs SharePoint On-Prem
* [SharePoint Lists Vs Libraries](https://sharepointmaven.com/lists-vs-libraries-in-sharepoint-online/)
* There is List/Library Validation and Column Validation
  * Column validation only works for new data entries [^1]
  * List/Library Validation ensures that the data was entered correctly with respect to other columns in the list or library. [^1]
  * A big limitation of the Column Validation I mentioned above is that you can not reference other columns. This is where the list/library validation comes into play. [^1]
* [Site-Wide Column vs Library Column](https://learn.microsoft.com/en-au/microsoft-365/community/list-column-or-site-column-which-one-to-choose)
* Audience Targeting is more about showing/not showing/promoting content and isn't really security

[^1]: <https://sharepointmaven.com/how-to-do-column-validation-in-sharepoint/>

## Validation Tips

* If you're having trouble with the formulas try going into the library settings --> Advanced settings then select the column and enter the formula in the classic style interface.
* Today() and Now() seem to not always follow the timezone of the sharepoint site. Google for fixes. They are just semi-shitty workarounds like adding using created/modified dates or doing math to the today function.
  * <https://answers.microsoft.com/en-us/msoffice/forum/all/sharepoint-today-function-not-showing-correct-date/7d094e83-2a60-4d53-b06b-73c575008035> (expand to see app replies)

## SharePoint Formulas

[Examples of common formulas in lists](https://support.microsoft.com/en-us/office/examples-of-common-formulas-in-lists-d81f5f21-2b4e-45ce-b170-bf7ebf6988b3)\
<https://learn.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN>

### Common Formulas

`=[My Column Name] > TODAY()`: Column name must be greater than today's date.

## Audience Targeting

<https://support.microsoft.com/en-au/office/target-content-to-a-specific-audience-on-a-sharepoint-site-68113d1b-be99-4d4c-a61c-73b087f48a81>

> [!TIP]
> Audience Targeting doesn't work with SharePoint groups, only AD, AAD, M365 etc

## Styling and Theming

* [ ] Add LookBook Link

### Theming

TBC

#### Custom Theming

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
<https://learn.microsoft.com/en-us/powershell/sharepoint/sharepoint-online/connect-sharepoint-online?view=sharepoint-ps>

> [!TIP] Gallery Module Easier
> Rather than download and install the MSI its easier to install and manage teh SharePoint Online PowerShell Module via PowerShell Gallery

### Install SharePoint Online PowerShell

```powershell
Install-Module -Name Microsoft.Online.SharePoint.PowerShell
# OR for no admin rights
Install-Module -Name Microsoft.Online.SharePoint.PowerShell -Scope CurrentUser
# To update already installed
Update-Module -Name Microsoft.Online.SharePoint.PowerShell
```

### Connect to SharePoint Online

With MFA:

`Connect-SPOService -Url https://contoso-admin.sharepoint.com`

> [!NOTE]
> There is a known issue between the SharePoint Online Management Shell module and SharePoint Client Components SDK where the module will fail to load if both are installed on the same computer. If you encounter this issue, uninstall the SharePoint Client Components SDK.

## Good sites

### Microsoft 365 Community Content

[Site Builder/Owner: New Site Checklist](https://learn.microsoft.com/en-us/microsoft-365/community/new-site-checklist)\
<https://pnp.github.io/> - Microsoft 365 & Power Platform Community - used to be called Patterns and Practices. Make some good tools like PnP Tools for SharePoint/O365 plus a tonne of samples.

### Misc

**<https://sharepointmaven.com/>** - really good\
<https://www.sharepointdiary.com/> - older but still ok.
