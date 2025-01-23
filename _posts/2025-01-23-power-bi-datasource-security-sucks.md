---
title: Power BI datasource security sucks
date: 2025-01-23T07:48:04.684Z
modifieddate: 2025-01-23T07:51:54.214Z
categories: []
description: ""
published: false
draft: true
type: posts
layout: posts
preview: ""
tags: []
fmContentType: posts
---


 <!--- cSpell:disable --->
* [TL;DR](#tldr)
* [Intro](#intro)
* [Summary](#summary)
 <!--- cSpell:enable --->
## TL;DR

* Power BI Datasource security sucks
* [Web.Contents](https://learn.microsoft.com/en-us/powerquery-m/web-contents) has an API Key section, but it only applies if the API Key is part of the URL/URI
* If you use a header to authenticate, it has to be hard coded.
* The other only option is to make a custom connector, which is too hard and overkill for something like this.

## Intro

## Summary
