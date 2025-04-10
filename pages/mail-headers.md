---
title: Mail Headers
description: TBC
published: true
categories:
    - Tech
type: pages
layout: pages
date: 2025-03-17T23:34:50.024Z
lastmod: 2025-04-09T13:53:57.254Z
tags:
    - Email
    - Exchange
isdraft: true
fmContentType: pages
mermaid: false
preview: ""
---

<!--- cSpell:disable --->
* [Headers](#headers)
  * [From](#from)
    * [sender](#sender)
  * [Return Path](#return-path)
  * [Reply-To](#reply-to)
  * [To](#to)
  * [CC](#cc)
  * [BCC](#bcc)
  * [Content type](#content-type)
  * [Auth Headers](#auth-headers)
  * [Other Headers](#other-headers)
* [References](#references)
  * [Standards](#standards)
  * [Exchange Email Header References](#exchange-email-header-references)
* [Tools](#tools)
<!--- cSpell:enable --->

## Headers

<https://en.wikipedia.org/wiki/Email#Message_header>

### From

From: The email address, and, optionally, the name of the author(s). Some email clients are changeable through account settings.

#### sender

Sender: Address of the sender acting on behalf of the author listed in the From: field (secretary, list manager, etc.).

### Return Path

Return path The return path email, also known as the "bounce address" or "envelope sender," is an email header used during SMTP communication to specify where bounced emails should be directed.

It serves as the designated recipient for non-delivery reports or email bounce notifications, which include details about why an email failed to deliver. Importantly, the return path email can differ from the "From" or "Reply-To" addresses used in the message, allowing marketers to separate bounce handling from regular correspondence.****

<https://www.mailmodo.com/guides/return-path-email/>

### Reply-To

Should not be different to the from domain, but can be a different subdomain on the same TLD [REF](https://www.quora.com/Does-sending-emails-with-a-From-address-with-a-different-domain-from-the-Reply-To-address-hurt-ones-deliverability#:~:text=even%20if%20it%20is%20a%20different%20sub%2Ddomain%20should%20not%20be%20a%20problem.)

[Does sending emails with a From: address with a different domain from the Reply-To: address hurt one's deliverability?](https://www.quora.com/Does-sending-emails-with-a-From-address-with-a-different-domain-from-the-Reply-To-address-hurt-ones-deliverability)

### To

To: The email address(es), and optionally name(s) of the message's recipient(s). Indicates primary recipients (multiple allowed), for secondary recipients see Cc: and Bcc: below.

### CC

Cc: Carbon copy; Many email clients mark email in one's inbox differently depending on whether they are in the To: or Cc: list.

### BCC

Bcc: Blind carbon copy; addresses are usually only specified during SMTP delivery, and not usually listed in the message header.

### Content type

Usually a [MIME Type](https://en.wikipedia.org/wiki/MIME)

### Auth Headers

* Authentication-Results: after a server verifies authentication, it can save the results in this field for consumption by downstream agents.
* Received-SPF: stores results of SPF checks in more detail than Authentication-Results.
* DKIM-Signature: stores results of DomainKeys Identified Mail (DKIM) decryption to verify the message was not changed after it was sent.
* Auto-Submitted: is used to mark automatic-generated messages.
* VBR-Info: claims VBR whitelisting

### Other Headers

* Subject: A brief summary of the topic of the message. Certain abbreviations are commonly used in the subject, including "RE:" and "FW:".
* Precedence: commonly with values "bulk", "junk", or "list"; used to indicate automated "vacation" or "out of office" responses should not be returned for this mail, e.g. to prevent vacation notices from sent to all other subscribers of a mailing list. Sendmail uses this field to affect prioritization of queued email, with "Precedence: special-delivery" messages delivered sooner. With modern high-bandwidth networks, delivery priority is less of an issue than it was. Microsoft Exchange respects a fine-grained automatic response suppression mechanism, the X-Auto-Response-Suppress field.[46]
* Message-ID: Also an automatic-generated field to prevent multiple deliveries and for reference in In-Reply-To: (see below).
* In-Reply-To: Message-ID of the message this is a reply to. Used to link related messages together. This field only applies to reply messages.
* List-Unsubscribe: HTTP link to unsubscribe from a mailing list.
* References: Message-ID of the message this is a reply to, and the message-id of the message the previous reply was a reply to, etc.
* Archived-At: A direct link to the archived form of an individual email message.

## References

### Standards

[SMTP Standard in Misc References](misc-references.md#smtp)

### Exchange Email Header References

<https://learn.microsoft.com/en-us/defender-office-365/message-headers-eop-mdo>\
<https://learn.microsoft.com/en-us/exchange/header-firewall-exchange-2013-help>\
<https://learn.microsoft.com/en-us/exchange/anti-spam-stamps-exchange-2013-help>

## Tools

[Postmaster Tools in Misc Tools](misc-tools.md#postmaster)\
[Exchange Commands](exchange-commands.md)
