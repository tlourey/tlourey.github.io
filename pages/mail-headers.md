---
title: Mail Headers
description: ""
published: false
categories:
    - Tech
type: pages
layout: pages
date: 2025-03-17T23:34:50.024Z
lastmod: 2025-03-17T23:41:54.694Z
tags:
    - Email
isdraft: true
fmContentType: pages
mermaid: false
preview: ""
---

<!--- cSpell:disable --->
* [Headers](#headers)
  * [From](#from)
  * [Return Path](#return-path)
  * [Reply-To](#reply-to)
  * [To](#to)
  * [CC](#cc)
  * [BCC](#bcc)
* [References](#references)
  * [Standards](#standards)
  * [Exchange Email Header References](#exchange-email-header-references)
* [Tools](#tools)
<!--- cSpell:enable --->

## Headers

### From

TBC

### Return Path

Return path The return path email, also known as the "bounce address" or "envelope sender," is an email header used during SMTP communication to specify where bounced emails should be directed.

It serves as the designated recipient for non-delivery reports or email bounce notifications, which include details about why an email failed to deliver. Importantly, the return path email can differ from the "From" or "Reply-To" addresses used in the message, allowing marketers to separate bounce handling from regular correspondence.****

<https://www.mailmodo.com/guides/return-path-email/>

### Reply-To

TBC

### To

TBC

### CC

TBC

### BCC

TBC

## References

### Standards

[SMTP Standard in Misc References](misc-references.md#smtp)

### Exchange Email Header References

<https://learn.microsoft.com/en-us/defender-office-365/message-headers-eop-mdo>\
<https://learn.microsoft.com/en-us/exchange/header-firewall-exchange-2013-help>
<https://learn.microsoft.com/en-us/exchange/anti-spam-stamps-exchange-2013-help>

## Tools
