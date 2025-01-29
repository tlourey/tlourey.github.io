---
title: Power BI datasource security sucks
date: 2025-01-23T07:48:04.684Z
categories:
    - Tech
description: ""
published: false
draft: true
type: posts
layout: posts
preview: ""
tags:
    - Power BI
    - Security
fmContentType: posts
lastmod: 2025-01-29T07:43:16.553Z
---

<!--- cSpell:disable --->
* [TL;DR](#tldr)
* [Intro](#intro)
* [Scenario](#scenario)
* [Workspace restrictions](#workspace-restrictions)
* [File restrictions](#file-restrictions)
* [Changing credentials](#changing-credentials)
* [Summary](#summary)
<!--- cSpell:enable --->

## TL;DR

* Power BI Datasource security sucks
* [Web.Contents](https://learn.microsoft.com/en-us/powerquery-m/web-contents) has an API Key section, but it only applies if the API Key is part of the URL/URI
* If you use a header to authenticate, it has to be hard coded, which is shit.
* The other only option is to make a custom connector, which is too hard and overkill for something like this.
* This post covers some bad more options when this is your only choice.
* Vote for this to be fixed.

## Intro

* [ ] Intro

## Scenario

* [ ] Scenario

## Workspace restrictions

Whatever workspace you push it to, limit who has access.
Share reports individually out of the workspace
Don't allow others to re-share the report
Don't allow others to access the underlying datasource when sharing

## File restrictions

If you make a .pbix or .pbit with the credential in it, tell people to keep them VERY secure.
Send them around in a password protected zip file.

## Changing credentials

* Do it regularly
* Do it before you release the report
  * Note that anyone who access to the workspace can download a copy of the .pbit/.pbix with the credentials in it, so consider the workspace restrictions above.
* Set them to expire more often.

## Summary

Vote for it to be better: <https://ideas.fabric.microsoft.com/ideas/idea/?ideaid=2468fe9d-498f-ec11-826d-501ac50aa35e>

Other give me other ideas...
