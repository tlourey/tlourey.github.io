---
title: Microsoft Teams Tips
description: Tips, tricks and shortcuts for MS Teams
published: false
categories:
    - Tech
type: pages
layout: pages
date: 2025-02-01T05:30:26.931Z
lastmod: 2025-04-04T06:38:44.864Z
tags:
    - Microsoft365
    - Teams
    - Tips
isdraft: truedele
fmContentType: pages
preview: ""
keywords:
    - Teams
---

<!--- cSpell:disable --->
* [Keyboard Shortcuts](#keyboard-shortcuts)
* [Slash Commands](#slash-commands)
* [Social Share to Teams](#social-share-to-teams)
* [Microsoft Places](#microsoft-places)
  * [Microsoft Places Setup](#microsoft-places-setup)
    * [Add Services to buildings](#add-services-to-buildings)
* [Network and Location Data](#network-and-location-data)
* [Misc KBs](#misc-kbs)
<!--- cSpell:enable --->

## Keyboard Shortcuts

**<https://support.microsoft.com/en-au/office/keyboard-shortcuts-for-microsoft-teams-2e8e2a70-e8d8-4a19-949b-4c36dd5292d2>**

|Area|Function|Desktop Shortcut|Webapp shortcut|
|-|-|-|-|
|Meetings & Calls|Temporarly unmute|<kbd>CTRL</kbd>+<kbd>Spacebar</kbd>|<kbd>CTRL</kbd>+<kbd>Spacebar</kbd>|
|Meetings & Calls|Ummute|<kbd>Win+Alt+K</kbd> or <br> <kbd>Ctrl+Shift+M</kbd>| <kbd>Win+Alt+K</kbd> or <br> <kbd>Ctrl+Shift+M</kbd> |
|Meetings & Calls|End audio or video call|<kbd>Ctrl+Shift+H</kbd>|<kbd>Ctrl+Shift+H</kbd>|
|Meetings & Calls|Decide a call|<kbd>CTRL+Shift+D</kbd>|<kbd>CTRL+Shift+D</kbd>|
|Meetings & Calls|Start a video call|<kbd>Alt+Shift+V</kbd>|<kbd>Alt+Shift+V</kbd>|
|Meetings & Calls|Start a audit call|<kbd>Alt+Shift+A</kbd>|<kbd>Alt+Shift+A</kbd>|
|Chat|Jump to last read/latest message|<kbd>Ctrl+J</kbd>|**<kbd>Alt+J</kbd>**|
|Chat|Reply to lastest/selected message|<kbd>Alt+Shift+R</kbd>|<kbd>Alt+R</kbd>|
|Chat|Search current channel|<kbd>Ctrl+F</kbd>|<kbd>Ctrl+F</kbd>|
|Chat|Pop Out Existsing Chnanel/Chat|<kbd>Ctrl+O</kbd>|**None**|
|Chat|Go to compose box|<kbd>Ctrl+R</kbd>|**<kbd>Ctrl+Shift+R</kbd>**|
|Chat|Mark as important|<kbd>Ctrl+Shift+I</kbd>|<kbd>Ctrl+Shift+I</kbd>|
|Chat|Expand compose box|<kbd>CTRL+Shif+X</kbd>|<kbd>CTRL+Shif+X</kbd>|
|Chat|Insert link|<kbd>CTRL+K</kbd>|<kbd>CTRL+K</kbd>|
|Chat|Paragraph style| <kbd>CTRL+Alt+P</kbd>| <kbd>CTRL+Alt+P</kbd> |
|Chat|Insert code blocks|<kbd>Ctrl+Shift+Alt+B</kbd>|<kbd>Ctrl+Shift+Alt+B</kbd>|
|Chat|Insert inline code|<kbd>Ctrl+Shift+Alt+C</kbd>|<kbd>Ctrl+Shift+Alt+C</kbd>|
|Chat|Insert code|<kbd>Ctrl+Alt+5</kbd>|<kbd>Ctrl+Alt+5</kbd>|
|Chat|Insert block quote|<kbd>Ctrl+Alt+4</kbd>|<kbd>Ctrl+Alt+4</kbd>|

## Slash Commands

<https://support.microsoft.com/en-au/office/use-commands-in-microsoft-teams-88f61508-284d-417f-a53d-9e082164050b>\
<https://www.fusionconnect.com/blog/slash-commands-in-microsoft-teams>

Common ones:

`/available`: Set your status to available.\
`/away`:Set your status to away.\
`/busy`:Set your status to busy.\
`/brb`:Set your status to be right back.\
`/dnd`:Set your status to do not disturb.\
`/offline`:Set your status to appear offline.\
`/reset`: Reset Presence Status

Others (Mostly from <https://www.fusionconnect.com/blog/slash-commands-in-microsoft-teams>):

`/apps`: Add an app.\
`/delete`: Delete the chat.\
`/hide`: Hide the chat.\
`/leavechat`: Leave the chat.\
`/leavemeeting`: Leave the meeting.\
`/meetnow`: Start or join a quick meeting.\
`/mute`: Mute the chat.\
`/unmute`: Unmute the chat.\
**`/window`: Open chat in a new window.**\
`/code`: Add a code block.\
`/loop`: Add a loop paragraph.\
`/record`: Record a video clip.\
`/settings`: Open settings.\
`/shortcuts`: Open keyboard shortcuts.\

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

## Microsoft Places

> [!CAUTION] TBA/TBC
> This section is still very TBA/TBC and under expansion.

> [!NOTE] Multiple Tools
> Microsoft Places stiches together a number of technology sets. This content may move between this page, an Exchange page and/or [Microsoft 365 Tips](microsoft-365-tips.md).
> While parts of this are more teams related it also uses Workspace Calendar

Microsoft Places App: <https://aka.ms/places>

<https://support.microsoft.com/en-au/office/first-things-to-know-about-bookable-desks-in-microsoft-teams-5d10c217-1205-48a1-a883-ff4533f4ae71>\
<https://support.microsoft.com/en-au/office/set-your-work-location-in-microsoft-teams-6c14a0f5-3cd6-427d-b1d2-aa0365aebf88>\
<https://support.microsoft.com/en-au/office/set-your-work-location-in-microsoft-teams-6c14a0f5-3cd6-427d-b1d2-aa0365aebf88>\
<https://support.microsoft.com/en-au/office/show-your-hybrid-work-location-availability-to-meet-work-hours-and-more-c861198d-f82e-41d7-88ec-c2e716be5ede>

> [!NOTE] Room and Workspace Mailboxes
> You should consider having Room and workspace mailboxes setup and working before doing MS Places
> See [Configure rooms and workspaces for Room Finder in Outlook](https://learn.microsoft.com/en-us/outlook/troubleshoot/calendaring/configure-room-finder-rooms-workspaces)

### Microsoft Places Setup

> [!WARNING] Still reading
> I'm still reading about this section so its still a bit of a work in progress.

> [!TIP] Set up Mailboxes first
> all of the below steps and info may be slightly easier if you have already started entering metadata using the `Set-Place` command from the Exchange PowerShell for your meeting rooms, etc.

<https://learn.microsoft.com/en-au/microsoftteams/rooms/bookable-desks>\
<https://learn.microsoft.com/en-au/powershell/module/teams/new-csteamsworklocationdetectionpolicy?view=teams-ps>\
<https://learn.microsoft.com/en-us/powershell/module/teams/grant-csteamsworklocationdetectionpolicy?view=teams-ps>\
<https://learn.microsoft.com/en-au/microsoft-365/places/configure-desk-booking?branch=main#configure-desk-pools>\
<https://learn.microsoft.com/en-au/microsoft-365/places/enabling-places-finder#understanding-the-differences-between-room-finder-and-places-finder>
<https://learn.microsoft.com/en-us/microsoft-365/places/get-started/quick-setup-buildings-floors>\
<https://gist.github.com/adthom/b703078806adeb71fe860929df0bd4c1>

> [!NOTE] Assumptions
> This section is assuming you are already using Meeting Room Calendars.

> [!IMPORTANT] Buildings and Floors
> When using the MicrosoftPlaces cmdlets, building and floor setups appear quickly in teams where as rooms, desks and workspaces may take 24 hours.
> *"New buildings, floors, and sections should be visible in Microsoft Places right away. However, any changes made to rooms, and workspaces may take up to 24 hours to update."*

1. Install/Import MicrosoftPlaces and MicrosoftTeams module
2. `connect-microsoftplaces`
3. `Initialize-Places`
4. Choose Option 1 to export a csv
5. Review and adjust the csv and adjust as per <https://learn.microsoft.com/en-us/microsoft-365/places/get-started/quick-setup-buildings-floors#step-2---review-and-revise-the-csv>
6. Upload the finalised CSV
7. `Set-PlacesSettings -PlacesFinderEnabled 'Default:true'`: Enable Places Finder. It can be limited to a specific group
8. Deploy MS Places app in outlook: <https://learn.microsoft.com/en-us/microsoft-365/admin/manage/teams-apps-work-on-outlook-and-m365?view=o365-worldwide>
9. Consider pre-installing in MS Teams by adjusting app setup policies: <https://learn.microsoft.com/en-us/microsoftteams/teams-app-setup-policies#add-apps-to-your-teams-client>
10. You need individual desks or desk pools (aka workspaces) setup. Indivudal desks needs teams premium.
11. **Other Steps TBC**
12. [Add Services to buildings](#add-services-to-buildings)
13. `Set-PlacesSettings -PlacesFinderEnabled 'Default:true'`
14. `Disconnect-MicrosoftPlaces`
15. `import-module MicrosoftTeams`
16. `Connect-MicrosoftTeams`
17. `New-CsTeamsWorkLocationDetectionPolicy -Identity wld-test-policy -EnableWorkLocationDetection $true` (These commands may need to be in a seperate set of steps)
18. `Grant-CsTeamsWorkLocationDetectionPolicy -PolicyName wld-test-policy -Identity testuser@test.onmicrosoft.com`: (you can set a policy to a group or Globally)
19. `Disconnect-MicrosoftTeams`

You can consider a manual setup: <https://learn.microsoft.com/en-us/microsoft-365/places/get-started/quick-setup-buildings-floors#alternative---manual-setup>

#### Add Services to buildings

> [!CAUTION] ResourceLinks always replaces
> The `Set-PlacesV3` `-ResourceLinks` Parameter always replaces the existsing values so you need to get current values and add to it when you want to amend. See [this section on Set-PlacesV3 Info page](https://learn.microsoft.com/en-us/microsoft-365/places/powershell/set-placev3#-resourcelinks).

Based off: <https://learn.microsoft.com/en-us/microsoft-365/places/services-in-places>

`Set-PlaceV3 -Identity <PlaceId> -ResourceLinks @{name="Tech Support"; Value="https://www.contoso.sharepoint.com/TechSupport"; type="URL"}`

Best way to setup multiples is:

1. Add the first: `Set-PlaceV3 -Identity <PlaceId> -ResourceLinks @{name="Tech Support"; Value="https://www.contoso.sharepoint.com/TechSupport"; type="URL"}`
2. Add exch extra using the snippet below

```powershell
$ResourceLinks = (Get-PlaceV3 <PlaceId>).ResourceLinks
$ResourceLinks.Add(@{name="TestLink";value="https://contoso.com/";type="Url"})
Set-PlaceV3 -Identity <PlaceId> -ResourceLinks $ResourceLinks
```

<https://learn.microsoft.com/en-us/microsoft-365/places/powershell/set-placev3#-resourcelinks>\
<https://learn.microsoft.com/en-us/microsoft-365/places/powershell/set-placev3>

## Network and Location Data

<https://connectivity.office.com/> -  Microsoft 365 network connectivity test\

Also:
<https://learn.microsoft.com/en-us/microsoftteams/cqd-upload-tenant-building-data>\
[Call Quality Dashboard Tenant Data Upload](https://cqd.teams.microsoft.com/spd/#/TenantDataUpload)

<https://learn.microsoft.com/en-us/microsoftteams/location-based-routing-configure-network-settings> - while this is more for teams routing i've found it gives other parts of teams more context about issues.

Also see [Network Detail Upload in Microsoft 365 Tips](microsoft-365-tips.md#network-details-upload)

## Misc KBs

<https://support.microsoft.com/en-au/office/join-a-meeting-without-an-account-in-microsoft-teams-c6efc38f-4e03-4e79-b28f-e65a4c039508>\
Markdown Support in Teams: <https://support.microsoft.com/en-au/office/use-markdown-formatting-in-microsoft-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772>
