---
title: Language and Region Settings when not in USA
date: 2025-01-25T06:19:32.138Z
lastmod: 2025-01-28T14:36:25.043Z
categories:
    - Tech
description: Get your shit together
published: false
draft: true
type: posts
layout: posts
preview: ""
tags:
    - Microsoft 365
    - Language
    - Rant
fmContentType: posts
---

<!--- cSpell:disable --->
* [TL;DR](#tldr)
* [Intro](#intro)
* [en-us or bust](#en-us-or-bust)
* [Windows Language](#windows-language)
* [Summary](#summary)
<!--- cSpell:enable --->

<!--- cSpell:disable --->
<!---
Points: DELETE BEFORE PUBLISHING

* [ ] Declare Bias - ENAU, Austrlia, don't do much international
* [ ] Not everyone is EN-US
* [ ] Limited Display Language
* [ ] Timezones
* [ ] Regions
* [ ] Defaults
* [ ] Great examples
  * [ ] SharePoint Validation around timezones
  * [ ] Public URLs changing EN-US to EN-AU: SOMETIMES YES, SOMETIMES NO
    * [ ] Example, works for learn.microsoft.com, but not adoption.microsoft.com
  * [ ] OS Issues
    * [ ] EN-US keeps coming back and so does toolbar
* [ ] Multiple locations
* [ ] Not easy for end user
* [ ] Not easy for admin
--->
<!--- cSpell:enable --->

## TL;DR

## Intro

## en-us or bust

<https://learn.microsoft.com/en-us/powershell/scripting/overview?view=powershell-7.5> - Date is in US format\
<https://learn.microsoft.com/en-au/powershell/scripting/overview?view=powershell-7.5> - Date is in AU format - YAY

<https://adoption.microsoft.com/en-us/microsoft-lists/> - Of course this works\
<https://adoption.microsoft.com/en-gb/microsoft-lists/> - Jolly good, en-gb is working!
<https://adoption.microsoft.com/en-au/microsoft-lists/> - This gets a fancy 404, fuck you Australia\
<https://adoption.microsoft.com/en-nz/microsoft-lists/> - Sorry Sheep Shaggers, No Microsoft Lists adoption for you. 

## Windows Language

Why does it randomly keep adding en-us back? No idea. Maybe we need to set the default profile language to En au and also the home screen before you login. Lets use there copy profile settings buttons for language?

WHY DID IT INSTALL EN-GB???

How do we fix it?

PowerShell?
DSIM?
Some other random command? I but you don't have to do that with en-us...

## Summary
