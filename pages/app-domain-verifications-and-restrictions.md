---
title: App Domain Verifications and Restrictions
description: TBC
published: false
categories:
    - Tech
type: pages
layout: pages
date: 2024-12-12T18:04:19.415Z
lastmod: 2025-04-12T07:27:48.036Z
tags:
    - DNS
    - Security
    - References
isdraft: true
fmContentType: pages
mermaid: false
preview: ""
keywords:
    - DNS
    - Domain Verification
    - SaaS
---

<!--- cSpell:disable --->
* [Vendors](#vendors)
  * [Slack](#slack)
  * [monday.com](#mondaycom)
  * [Atlassian](#atlassian)
  * [Yahoo](#yahoo)
  * [Google](#google)
  * [Apple](#apple)
  * [Facebook](#facebook)
  * [Microsoft](#microsoft)
    * [Service 1 TBC](#service-1-tbc)
    * [Service 2 TBC](#service-2-tbc)
  * [Blackbaud](#blackbaud)
    * [Blackbaud SignIn](#blackbaud-signin)
  * [Docusign](#docusign)
  * [Paloalto Networks](#paloalto-networks)
  * [Adobe](#adobe)
    * [Adobe Sign](#adobe-sign)
    * [Adobe IDP](#adobe-idp)
  * [Cisco](#cisco)
    * [Webex](#webex)
    * [Cisco Ci](#cisco-ci)
  * [Dynatrace](#dynatrace)
  * [Sage](#sage)
  * [Amazon](#amazon)
    * [Amazon SES](#amazon-ses)
    * [AWS Service No 2](#aws-service-no-2)
  * [OneTrust](#onetrust)
  * [Twilio](#twilio)
  * [Zoom](#zoom)
  * [Tictok](#tictok)
  * [Stripe](#stripe)
  * [Docker](#docker)
  * [Canva](#canva)
  * [VMWare](#vmware)
  * [Fastly](#fastly)
    * [Fastly Domain Delegation](#fastly-domain-delegation)
    * [Fastly Verification](#fastly-verification)
* [Still to add](#still-to-add)
  * [Known](#known)
  * [Unknown](#unknown)
* [More Info](#more-info)
<!--- cSpell:enable --->

<!---
### Template

KB: <>

Record Name: TBA\
Record Type: TXT\
Record Value Format: `-verification=<random characters>`

Extra Instance Blocking Available: TBA
Extra Instance Blocking Info: <>
-->

## Vendors

### Slack

KB: <https://slack.com/intl/en-au/help/articles/5513043606547-Claim-and-verify-email-domains>

Record Name: @\
Record Type: TXT\
Record Value Format: `slack-domain-verification=<random characters>`

Extra Instance Blocking Available: Maybe (with Grid)
Extra Instance Blocking Info: <https://slack.com/intl/en-au/help/articles/115004234367-Manage-workspace-creation-requests-on-Enterprise-Grid>

### monday.com

KB: <https://support.monday.com/hc/en-us/articles/18705654232466-Claim-your-business-domain-on-monday-com>

Record Name: @\
Record Type: TXT\
Record Value Format: `-verification=<random characters>`

Extra Instance Blocking Available: YEs
Extra Instance Blocking Info: <https://support.monday.com/hc/en-us/articles/18705654232466-Claim-your-business-domain-on-monday-com#:~:text=At%20the%20bottom%20of%20the%20screen%2C%20you%20can%20choose%20if%20you%27d%20like%20to%20allow%20new%20accounts%20to%20be%20created%20with%20these%20domains%2C%20or%20if%20you%27d%20prefer%20to%20block%20new%20account%20creation%20with%20these%20domains%20altogether>

### Atlassian

KB: <>

Record Name: @\
Record Type: TXT\
Record Value Format: `atlassian-domain-verification=<random characters>`

Extra Instance Blocking Available: TBA
Extra Instance Blocking Info: <>

### Yahoo

KB: <>

Record Name: @\
Record Type: TXT\
Record Value Format: `yahoo-verification-key=<random characters>`

Extra Instance Blocking Available: TBA
Extra Instance Blocking Info: <>

### Google

KB: <https://support.google.com/a/answer/16018515?hl=en&visit_id=638800347432095314-2581519605&rd=1>

Record Name: @\
Record Type: TXT\
Record Value Format: `google-site-verification=<random characters>`

Extra Instance Blocking Available: TBA
Extra Instance Blocking Info: <>

### Apple

KB: <>

Record Name: @\
Record Type: TXT\
Record Value Format: `apple-domain-verification=<random characters>`

Extra Instance Blocking Available: TBA
Extra Instance Blocking Info: <>

### Facebook

KB: <https://developers.facebook.com/docs/sharing/domain-verification>

Record Name: @\
Record Type: TXT\
Record Value Format: `facebook-domain-verification=<random characters>`

Extra Instance Blocking Available: TBA
Extra Instance Blocking Info: <>

### Microsoft

<https://learn.microsoft.com/en-us/microsoft-365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider?view=o365-worldwide>

* [ ] Add in all the various microsoft ones

#### Service 1 TBC

TBC

#### Service 2 TBC

TBC

### Blackbaud

#### Blackbaud SignIn

KB: <>

Record Name: @\
Record Type: TXT\
Record Value Format: `<random characters>`

Extra Instance Blocking Available: TBA
Extra Instance Blocking Info: <>

### Docusign

KB: <>

Record Name: @\
Record Type: TXT\
Record Value Format: `docusign=<random characters>`

Extra Instance Blocking Available: TBA
Extra Instance Blocking Info: <>

### Paloalto Networks

KB: <>

Record Name: @\
Record Type: TXT\
Record Value Format: `paloaltonetworks-site-verification=<random characters>`

Extra Instance Blocking Available: TBA
Extra Instance Blocking Info: <>

### Adobe

#### Adobe Sign

KB: <>

Record Name: @\
Record Type: TXT\
Record Value Format: `adobe-sign-verification=<random characters>`

Extra Instance Blocking Available: TBA
Extra Instance Blocking Info: <>

#### Adobe IDP

KB: <>

Record Name: @\
Record Type: TXT\
Record Value Format: `adobe-idp-site-verification=<random characters>`

Extra Instance Blocking Available: TBA
Extra Instance Blocking Info: <>

### Cisco

#### Webex

KB: <>

Record Name: @\
Record Type: TXT\
Record Value Format: `webexdomainverification.\<random characters\>=<random characters>`

Extra Instance Blocking Available: TBA
Extra Instance Blocking Info: <>

#### Cisco Ci

KB: <>

Record Name: @\
Record Type: TXT\
Record Value Format: `cisco-ci-domain-verification=<random characters>`

Extra Instance Blocking Available: TBA
Extra Instance Blocking Info: <>

### Dynatrace

KB: <>

Record Name: @\
Record Type: TXT\
Record Value Format: `Dynatrace-site-verification=<random characters>`

Extra Instance Blocking Available: TBA
Extra Instance Blocking Info: <>

### Sage

KB: <>

Record Name: @\
Record Type: TXT\
Record Value Format: `intacct-esk=<random characters>`

Extra Instance Blocking Available: TBA
Extra Instance Blocking Info: <>

### Amazon

#### Amazon SES

KB: <>

Record Name: _amazonses.mydomainorsubdomain.tld\
Record Type: TXT\
Record Value Format: `<random characters>`

Extra Instance Blocking Available: TBA
Extra Instance Blocking Info: <>

#### AWS Service No 2

TBC

### OneTrust

KB: <>

Record Name: @\
Record Type: TXT\
Record Value Format: `onetrust-domain-verification=<random characters>`

Extra Instance Blocking Available: TBA
Extra Instance Blocking Info: <>

### Twilio

KB: <>

Record Name: _twillo\
Record Type: TXT\
Record Value Format: `twilio-domain-verification=<random characters>`

Extra Instance Blocking Available: TBA
Extra Instance Blocking Info: <>

### Zoom

KB: <>

Record Name: @\
Record Type: TXT\
Record Value Format: `Zoom=<random characters>` or `zoom-domain-verification=ZOOM_verify_<random characters>`

Extra Instance Blocking Available: TBA
Extra Instance Blocking Info: <>

### Tictok

KB: <>

Record Name: @\
Record Type: TXT\
Record Value Format: `tiktok-developers-site-verification=<random characters>`

Extra Instance Blocking Available: TBA
Extra Instance Blocking Info: <>

### Stripe

KB: <>

Record Name: @\
Record Type: TXT\
Record Value Format: `stripe-verification=<random characters>`

Extra Instance Blocking Available: TBA
Extra Instance Blocking Info: <>

### Docker

KB: <>

Record Name: @\
Record Type: TXT\
Record Value Format: `docker-verification=<GUID>`

Extra Instance Blocking Available: TBA
Extra Instance Blocking Info: <>

### Canva

KB: <>

Record Name: @\
Record Type: TXT\
Record Value Format: `canva-site-verification=<random characters>`

Extra Instance Blocking Available: TBA
Extra Instance Blocking Info: <>

### VMWare

KB: <>

Record Name: @\
Record Type: TXT\
Record Value Format: `vmware-cloud-verification-<GUID>`

> [!NOTE] One of these is not like most others...
> VMWare seem to use a `-` instead of an `=`

Extra Instance Blocking Available: TBA
Extra Instance Blocking Info: <>

### Fastly

#### Fastly Domain Delegation

KB: <>

Record Name: @\
Record Type: TXT\
Record Value Format: `fastly-domain-delegation-<random characters>`

> [!NOTE] One of these is not like most others...
> Fastly seem to use a `-` instead of an `=`

Extra Instance Blocking Available: TBA
Extra Instance Blocking Info: <>

#### Fastly Verification

Record Name: @\
Record Type: TXT\
Record Value Format: `FASTLY-VERIFY-XX-X-XX` (maybe a date format from the example I found)

> [!NOTE] One of these is not like most others...
> Fastly seem to use a `-` instead of an `=`

Extra Instance Blocking Available: TBA
Extra Instance Blocking Info: <>

## Still to add

### Known

* [ ] pardot
* [ ] mixpanel (uses GUID)
* [ ] salesforce
* [ ] liveramp
* [ ] Microsoft

### Unknown

* `SFMC-<random characters>-<random characters>`
* `cloudhealth=<GUID>`
* `remarkable-domain-verification=<GUID>`
* `hubspot-developer-verification=<random characters>`

## More Info

* <https://www.netspi.com/blog/technical-blog/network-pentesting/analyzing-dns-txt-records-to-fingerprint-service-providers/>
* <https://en.wikipedia.org/wiki/TXT_record>
* <https://en.wikipedia.org/wiki/Well-known_URI>
