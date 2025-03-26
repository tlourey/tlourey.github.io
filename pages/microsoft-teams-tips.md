---
title: Microsoft Teams Tips
description: Tips, tricks and shortcuts for MS Teams
published: false
categories:
    - Tech
type: pages
layout: pages
date: 2025-02-01T05:30:26.931Z
lastmod: 2025-03-26T12:56:57.678Z
tags:
    - Microsoft365
    - Teams
    - Tips
isdraft: true
fmContentType: pages
preview: ""
keywords:
    - Teams
---

<!--- cSpell:disable --->
* [Keyboard Shortcuts](#keyboard-shortcuts)
* [Social Share to Teams](#social-share-to-teams)
* [Network and Location Data](#network-and-location-data)
<!--- cSpell:enable --->

## Keyboard Shortcuts

<https://support.microsoft.com/en-au/office/keyboard-shortcuts-for-microsoft-teams-2e8e2a70-e8d8-4a19-949b-4c36dd5292d2>

## Social Share to Teams

Info: <https://learn.microsoft.com/en-us/microsoftteams/platform/concepts/build-and-test/share-to-teams-from-web-apps> - also contains **proper** way to do it.

Rough example of method 1:

```html
<html>
 <body>
  <script async defer src="https://teams.microsoft.com/share/launcher.js"></script>

  <div
   class="teams-share-button"
   data-href="https://tlourey.github.io/"
   data-msg-text="Look MA, No pants!"
   data-icon-px-size="64"
   data-preview="true">
  </div>
 </body>
</html>
```

Method 2 allows a lot more control for dev

The manual hacky way:

| Parameters                | Description                           |
|------------------------|---------------------------------------|
| href  | the url to share|
| msgText | message text |
| Referrer           | the url that sent it                 |

Examples:

<https://teams.microsoft.com/share?href=https://adoption.microsoft.com/en-us/microsoft-lists/resources/&referrer=adoption.microsoft.com>

<https://teams.microsoft.com/share?href=https://example.com&referrer=example2.com>

<https://teams.microsoft.com/share?href=https%3A%2F%2Ftlourey.github.io%2F&msgText=Look%20MA%2C%20No%20pants!&referrer=127.0.0.1>

Using the above we should be able to create a bookmarklet

```javascript
javascript:(function()%7Bvar url %3D document.URL %3B%0A%0Awindow.location.href %3D "https%3A%2F%2Fteams.microsoft.com%2Fshare%3Fhref%3D"%0A                        %2B url %3B%7D)()%3B
```

[Share to Teams](javascript:(function()%7Bvar url %3D document.URL %3B%0A%0Awindow.location.href %3D "https%3A%2F%2Fteams.microsoft.com%2Fshare%3Fhref%3D"%0A                        %2B url %3B%7D)()%3B)\

If that doesn't work maybe this will

<a href="javascript:(function()%7Bvar url %3D document.URL %3B%0A%0Awindow.location.href %3D "https%3A%2F%2Fteams.microsoft.com%2Fshare%3Fhref%3D"%0A                        %2B url %3B%7D)()%3B">Share to Teams</a>

## Network and Location Data

<https://connectivity.office.com/> -  Microsoft 365 network connectivity test\

Also:
<https://learn.microsoft.com/en-us/microsoftteams/cqd-upload-tenant-building-data>\
[Call Quality Dashboard Tenant Data Upload](https://cqd.teams.microsoft.com/spd/#/TenantDataUpload)

<https://learn.microsoft.com/en-us/microsoftteams/location-based-routing-configure-network-settings> - while this is more for teams routing i've found it gives other parts of teams more context about issues.

Also see [Network Detail Upload in Microsoft 365 Tips](microsoft-365-tips.md#network-details-upload)
