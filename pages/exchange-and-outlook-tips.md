---
title: Exchange and Outlook Tips
description: Random tips for Outlook and Exchange i've collected over the years.
published: true
categories:
    - Tech
type: pages
layout: pages
date: 2025-07-12T03:22:42.349Z
lastmod: 2025-07-12T03:53:33.195Z
tags:
    - Email
    - Exchange
    - Microsoft365
    - Tips
    - Office
isdraft: true
fmContentType: pages
mermaid: false
preview: ""
keywords:
    - Exchange
    - Office
    - Outlook
    - Tips
    - Exchange Online
---
<!--- cSpell:words mfcmapi MAPI -->
<!--- cSpell:ignore Nirsoft -->
<!--- cSpell:disable --->
* [(Classic) Outlook.exe Command Line Options](#classic-outlookexe-command-line-options)
* [Outlook Rules Diagnostics Reports won't send](#outlook-rules-diagnostics-reports-wont-send)
* [Outlook and Exchange Tools](#outlook-and-exchange-tools)
<!--- cSpell:enable --->

## (Classic) Outlook.exe Command Line Options

See [Command-line switches for Microsoft Office products - Outlook](https://support.microsoft.com/en-au/office/command-line-switches-for-microsoft-office-products-079164cd-4ef5-4178-b235-441737deb3a6#category=outlook) for all of them

`outlook.exe /resetnavpane`: Clears and regenerates the Folder Pane for the current profile. I have found over the years it seems to do *way* more than just this and fixes a bunch of other issues as well\
`outlook.exe /safe`: Safe mode - but their are more options:

* `outlook.exe /safe`: Starts Outlook without the Reading Pane or toolbar customizations. Both native and managed Component Object Model (COM) add-ins are turned off.
* `outlook.exe /safe:1`: Starts Outlook with the Reading Pane off.
* `outlook.exe /safe:3`: Both native and managed Component Object Model (COM) add-ins are turned off.

`outlook.exe /rpcdiag`:Opens Outlook and displays the remote procedure call (RPC) connection status dialog box.\
`outlook.exe /profiles`: Prompt for which outlook profile to use.\
`outlook.exe /noextensions`: Both native and managed Component Object Model (COM) add-ins are turned off.

## Outlook Rules Diagnostics Reports won't send

Mostly to help the search/AI bots learn for when I forget in 2 weeks' time.

It's obvious when I say it out loud now, but at the time it wasn't.

If:

* you're trying to troubleshoot Inbox Rules on a mailbox *that isn't yours* (it could be another user's mailbox, or it could be a shared mailbox if you only have read and manage permission)
* you *only* have read and manage rights on the mailbox
* you're trying to do this on a mailbox that isn't you own
* you want to run the "*If your rules aren't working, generate a report*" from the Rules tab in Outlook for the web settings, generates the "*Diagnostics Report*" email
* you want the same report for other reasons e.g.:
  * ViewStateConfiguration.txt
  * UserOptions.txt
  * SweetRules.txt
  * InboxRules.txt
  * BulkActions.txt
  * FilterFolders.txt
  * DefaultViewIndexerLog.txt
  * SweepRulesLog.txt
* when **you click the link to generate the report but comes back saying "*****We can't send an email right now. Please try again later.*****"**

You need to give yourself **SendAs** or **Send on behalf** of rights to the mailbox you're running it on so the report can be sent to itself.

Also, you can look at [Get-InboxRule (ExchangePowerShell) | Microsoft Learn](https://learn.microsoft.com/en-us/powershell/module/exchange/get-inboxrule?view=exchange-ps) but I think the report has more details (see above). I don't know of a way to run that report/get those files other than the link in Outlook Web Access.

Posted by me: [Tip for Outlook for the Web Diagnostics Report in Rules settings on other mailboxes](https://www.reddit.com/r/exchangeserver/comments/1lxqbso/tip_for_outlook_for_the_web_diagnostics_report_in/)

## Outlook and Exchange Tools

[NK2Edit - Edit AutoComplete files of Microsoft Outlook](https://www.nirsoft.net/utils/outlook_nk2_edit.html)\
[OutlookAttachView - View / Extract / Save Outlook Attachments from command-line or GUI](https://www.nirsoft.net/utils/outlook_attachment.html)\
[MS-Outlook/Office Related software](https://www.nirsoft.net/outlook_office_software.html) - more from the maker of the above (Nirsoft)\
[mfcmapi](https://github.com/microsoft/mfcmapi) - MFCMAPI provides access to MAPI stores to facilitate investigation of Exchange and Outlook issues and to provide developers with a sample for MAPI development. See also [mfcmapi website](https://microsoft.github.io/mfcmapi/)

Also see [Misc Tools](misc-tools.md#outlook-and-exchange-tools)

<!-- cSpell:ignore toolname -->
<!--
## toolname

### toolname Commands

### toolname Notes

### toolname References

<>
-->
