---
title: Mac OS Tips
description: Tips for Mac OS
published: true
categories:
    - Tech
type: pages
layout: pages
date: 2025-02-25T04:41:08.679Z
lastmod: 2025-04-24T00:28:54.816Z
tags:
    - MacOS
    - Tips
isdraft: true
fmContentType: pages
preview: ""
---

<!--- cSpell:disable --->
* [Mouse Scrolling](#mouse-scrolling)
* [Time doesn't update](#time-doesnt-update)
* [Property Lists](#property-lists)
* [Offical Guides](#offical-guides)
* [Other Tips](#other-tips)
<!--- cSpell:enable --->

## Mouse Scrolling

If external (non-apple) mouse scrolling is inverse on a mac laptop, change:

Preferences --> Mouse --> Natural scrolling: False

But this changes it for both track pad and mouse. To me it should be on for a track pad but not a mouse. If your external mouse has software, install it so that you can separately set scrolling direction/mode.

## Time doesn't update

Notice your time isn't automatically updating or seems super out? A reboot should fix it, but if not:

Quick Fix:

1. Go to Control Panel --> General --> Date and Time
2. Turn **off** set time and date automatically (if it was already off that is your problem, if not continue)
3. Turn it **on** again

Long term fix:
<https://www.reddit.com/r/applehelp/comments/1dccrep/comment/l7x2ih7/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button>

Caveats:

* Issue with MacOS Sonoma
* Should be fixed in 14.5 but I had it occur again on 14.7

## Property Lists

Not exactly like the windows registry but maybe sorta.

You can adjust properity lists via:

* `defaults` tool on MacOS. See [Edit property lists in Terminal on Mac](https://support.apple.com/en-au/guide/terminal/apda49a1bb2-577e-4721-8f25-ffc0836f6997/mac).
* `plutil` command on MacOS. See [plutil man page from xode](https://keith.github.io/xcode-man-pages/plutil.1.html) - I get the feeling `defaults` is better than `plutil`

Background:

> *"In the macOS, iOS, NeXTSTEP, and GNUstep programming frameworks, property list files are files that store serialized objects. Property list files use the filename extension .plist, and thus are often referred to as p-list files."*
>
> \- *<https://en.wikipedia.org/wiki/Property_list>*

> Preference and configuration files in macOS use property lists (plists) to specify the attributes, or properties, of an app or process. An example is the preferences plist for the Finder in the Library/Preferences/ folder of a user's home folder. The file is named com.apple.finder.plist. The default naming convention for a plist includes the distributor's reverse DNS name prepended to the app or process name, followed by a .plist extension.
>
> To edit property lists, use the defaults command-line tool. The defaults command is a powerful tool and, when you know the specific key and value in a property list you want to change, the defaults tool is very efficient.
>
> The defaults tool works directly with the macOS preferences subsystem and is used by many apps in macOS to manage preferences and other settings. It can be built into shell scripts and lets you access preferences in the multiple domains that exist on a given computer.
>
> \- *[Edit property lists in Terminal on Mac](https://support.apple.com/en-au/guide/terminal/apda49a1bb2-577e-4721-8f25-ffc0836f6997/mac)*

## Offical Guides

[MacOS User Guide](https://support.apple.com/en-au/guide/mac-help/welcome/mac)\
[iPhoneOS User Guide](https://support.apple.com/en-au/guide/iphone/welcome/ios)
[iPadOS User Guide](https://support.apple.com/en-us/guide/ipad/welcome/ipados)\
[Terminal User Guide](https://support.apple.com/en-au/guide/terminal/welcome/mac)

[Manuals, Specs and Downloads](https://support.apple.com/en-au/docs)

## Other Tips

<https://saurabhs.org/macos-tips>
