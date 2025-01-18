---
title: MS Sentinel, Syslog, CEF and Azure Monitor Agent
date: 2025-01-18T05:46:46.188Z
categories:
- Sentinel
- Monitoring
- Security
- Azure
description: "3 clowns, 2 of which are brothers, looking to stich you up with rubbish message, or complexity."
published: false
preview: ""
draft: true
tags: []
type: posts
fmContentType: posts
---

[home](/) [up](./)
<!--- cSpell:disable --->
* [Draft talking points - Delete before publishing](#draft-talking-points---delete-before-publishing)
* [TL;DR](#tldr)
* [Intro](#intro)
* [Syslog Noise](#syslog-noise)
* [Rsyslog conf modification](#rsyslog-conf-modification)
* [DCR](#dcr)
  * [Editing DCRs](#editing-dcrs)
* [How can I check?](#how-can-i-check)
* [Summary](#summary)
* [References](#references)
<!--- cSpell:enable --->
## Draft talking points - Delete before publishing

* Expensive Log Analytics Injection? Noisy syslog's?
* Situation specifics (Azure, tools that didn't allow facility changes, original goals of syslog server)
* Learn Syslog Facilities (I still haven't enough)
* Learn Azure Monitoring DCR Transformations
* Learn how your syslog tool process configurations, eg `/etc/rsyslog.d/*.conf`
* MS's Rsyslog configuration gets slightly better after AMA Version 1.28
* It still sends too much noise. What to see how much???
* Solutions are:
  * Modify the `/etc/rsyslog.d/10-azuremonitoragent-omfwd.conf` OR
  * Use DCR Transformation

## TL;DR

Content

## Intro

## Syslog Noise

Here is how I started to figure out my noise. `DeviceVendor` is part of the [CEF standard](../pages/misc-references.md#cef). So try this in your LAW and adjust your time period/limit per your logging load (Start small then increase either the limit or the time range to get an idea):

```kql
CommonSecurityLog
| summarize Count=count() by DeviceVendor
```

Where the device vendor is blank is syslog noise. Also note that those that know syslog facilities better than me may not have chosen the USER facility. I didn't have a choice given of my SIEM integrations.

Where is the noise coming from? I had to muck around with syslog configs to get an idea. But here are some examples I found:

* 2 separate ones for MS Defender for Endpoint in Azure
* Azure Monitor Agent
* I can't remember the 3rd

So we need to reduce the noise. I planned on taking one of the two approaches

## Rsyslog conf modification

Here is what `/etc/rsyslog.d/10-azuremonitoragent-omfwd.conf` looks like after 1.28:

```bash
# Azure Monitor Agent configuration: forward logs to azuremonitoragent

template(name="AMA_RSYSLOG_TraditionalForwardFormat" type="string" string="<%PRI%>%TIMESTAMP% %HOSTNAME% %syslogtag%%msg:::sp-if-no-1st-sp%%msg%")
# queue.workerThreads sets the maximum worker threads, it will scale back to 0 if there is no activity
# Forwarding all events through TCP port
*.* action(type="omfwd"
template="AMA_RSYSLOG_TraditionalForwardFormat"
queue.type="LinkedList"
queue.filename="omfwd-azuremonitoragent"
queue.maxFileSize="32m"
queue.maxDiskSpace="1g"
action.resumeRetryCount="-1"
action.resumeInterval="5"
action.reportSuspension="on"
action.reportSuspensionContinuation="on"
queue.size="25000"
queue.workerThreads="100"
queue.dequeueBatchSize="2048"
queue.saveonshutdown="on"
target="127.0.0.1" Port="28330" Protocol="tcp")
```

One option to consider is rewording the rsyslog file. One Idea I was considering stealing was back from when they used the Log Analytics Agent with syslog forwarding:

```bash
if $rawmsg contains "CEF:" or $rawmsg contains "ASA-" then @@127.0.0.1:25226
```

## DCR

They suggest modifying the DCR with something like this:

```json
          "dataFlows": [
                    {
                        "streams": [
                            "Microsoft-CommonSecurityLog"
                        ],
                        "destinations": [
                            "DataCollectionEvent"
                        ],
                        "transformKql": "  source\n    |  where ProcessName !contains \"CEF\"\n"
                    }
          ]
```

I did steal the above from a specific example scenario but from what I could see CEF doesn't use the ProcessName field. So instead i'm trying this:

```json
          "dataFlows": [
                    {
                        "streams": [
                            "Microsoft-CommonSecurityLog"
                        ],
                        "destinations": [
                            "DataCollectionEvent"
                        ],
                        "transformKql": "  source\n    |  where isnotempty(DeviceVendor)\n"
                    }
          ]
```

Note that not all KQL is supported in Transformations. Refer to [Supported KQL features in Azure Monitor transformations](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/data-collection-transformations-kql)

### Editing DCRs

"Cool Story Bro, but I really don't want to fuck around that much...". Me either so there is a cheat if its simple. Using the DCR's Export Template, click deploy and edit the template before you submit it, right over the top of the existing rule.

1. Go to Azure Monitor
2. Go to Settings --> Data Collection Rules
3. Select your Data Collection Rule that gets your syslog's/CEF messages
4. Go to Automation --> Export Template
5. Click Download to take a backup
6. Click Deploy at the top
7. Click Edit Template
8. Find the dataflow section
9. Add in your transformation in a new element. similar to the above example

## How can I check?

One thing I found is that its hide to see exactly. Here are some ways:

1. Metrics of the DCR - this one I found the best as you can see Logs coming in, log errors, transformation time.
2. Workbooks on usage of the LAW - esp if its Sentinel enabled.
3. Trying to mirror / watch / capture what the syslog server output.

## Summary

## References

<https://learn.microsoft.com/en-us/azure/sentinel/cef-syslog-ama-overview?tabs=single#data-ingestion-duplication-avoidance>\
<https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/data-collection-transformations-kql>\
[KQL Queries](../pages/kql-queries.md)\
[AMA DCR LAW](../pages/ama-dcr-law.md)\
[Misc References](../pages/misc-references.md#cef)
