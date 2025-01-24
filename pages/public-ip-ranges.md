---
title: Public IP Ranges
description: Public IP Ranges to note and their references
categories:
    - References
    - Networks
type: pages
layout: pages
published: true
date: 2024-12-31T11:34:00
lastmod: 2025-01-24T07:58:23.315Z
---


<!--- cSpell:disable --->
* [Azure](#azure)
  * [Microsoft Sentinel](#microsoft-sentinel)
* [Amazon](#amazon)
* [Apple](#apple)
* [Google](#google)
* [Cloudflare](#cloudflare)
* [Omnissa](#omnissa)
* [Salesforce](#salesforce)
* [Misc Providers](#misc-providers)
* [Misc Sources](#misc-sources)
<!--- cSpell:enable --->

## Azure

* <https://www.microsoft.com/en-us/download/details.aspx?id=56519>
* <https://download.microsoft.com/download/7/1/D/71D86715-5596-4529-9B13-DA13A5DE5B63/ServiceTags_Public_20241021.json>

### Microsoft Sentinel

[IP allowlisting for the Microsoft Sentinel TAXII client](https://learn.microsoft.com/en-us/azure/sentinel/connect-threat-intelligence-taxii#ip-allowlisting-for-the-microsoft-sentinel-taxii-client)

## Amazon

* <https://docs.aws.amazon.com/vpc/latest/userguide/aws-ip-ranges.html>
* <https://ip-ranges.amazonaws.com/ip-ranges.json>
* <https://ip-ranges.amazonaws.com/geo-ip-feed.csv>

## Apple

* <https://support.apple.com/en-au/101555>

## Google

* <https://support.google.com/a/answer/10026322?hl=en>
* <https://www.gstatic.com/ipranges/goog.json>
* <https://www.gstatic.com/ipranges/cloud.json>

## Cloudflare

* <https://www.cloudflare.com/en-au/ips/>
* <https://www.cloudflare.com/ips-v4>
* <https://www.cloudflare.com/ips-v6>

## Omnissa

* [Omnissa Workspace ONE IP ranges for SaaS data centers (2960995)](https://kb.omnissa.com/s/article/2960995) - usually contains most accurate info but the below may need to be referred to:
* [Omnissa Best Practices Update - Workspace ONE UEM SaaS IP ranges - update and recommendation for customers to transition to DNS based allow lists (91317)](https://kb.omnissa.com/s/article/91317)
* [Omnissa Best Practices Update - Workspace ONE UEM SaaS IP ranges - updated recommendation for customers to transition to DNS based allow lists by January 15th, 2024 (95271)](https://kb.omnissa.com/s/article/95271)
* [Introducing IP Limited CDN capabilities in Managed Hosting SaaS Workspace ONE Environments (76872)](https://kb.omnissa.com/s/article/76872)
* [Omnissa Workspace ONE Assist IP ranges for SaaS Data centers (82567)](https://kb.omnissa.com/s/article/82567)

## Salesforce

* <https://ip-ranges.salesforce.com/ip-ranges.json>\
* <https://help.tableau.com/current/online/en-us/to_keep_data_fresh.htm#new-ip-addresses-after-hyperforce-migration>\
* <https://my.slack.com/help/urls>

## Misc Providers

* [Oracle Cloud](https://docs.oracle.com/iaas/tools/public_ip_ranges.json)
* [Linode](https://geoip.linode.com/)
* [DigitalOcean (DO)](https://digitalocean.com/geo/google.csv)

## Misc Sources

* <https://github.com/femueller/cloud-ip-ranges> which has a bot auto updating ranges regularly covering:
  * Akamai
  * Github
  * Fastly
  * Zscaler
  * Apple
  * Google
  * Cloudflare
  * AWS
  * Microsoft
  * Linode
  * Oracle
