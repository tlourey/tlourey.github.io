---
title: Mac OS Tips
description: Tips for Mac OS
published: false
categories:
    - Tech
type: pages
layout: pages
date: 2025-02-25T04:41:08.679Z
lastmod: 2025-02-26T23:37:07.412Z
tags:
    - MacOS
    - Tips
draft: true
fmContentType: pages
preview: ""
---

<!--- cSpell:disable --->
* [Mouse Scrolling](#mouse-scrolling)
* [Time doesn't update](#time-doesnt-update)
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
