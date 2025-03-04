---
title: Moving Microsoft Sentinel to another anything
date: 2025-01-18T05:41:37.512Z
categories: []
description: STOP. There will be tears and there isn't a great answer. Read this for bad ideas
published: false
preview: ""
isdraft: true
tags:
  - Azure
  - Sentinel
type: posts
fmContentType: posts
lastmod: 2025-03-04T11:35:15.650Z
---

[home](/) [up](./)
<!--- cSpell:disable --->
* [TL;DR](#tldr)
* [Intro](#intro)
<!--- cSpell:enable --->
## TL;DR

Azure says you can, but its only telling you about the Log Analytics Workspace. Moving Sentinel isn't supported. There isn't much stopping you.
If you just did this, move it back ***exactly*** where it was. Same subscription, same resource group, everything.
Wait a while, it may come back. You will still need to fix up somethings but thats what happened to me.

## Intro
