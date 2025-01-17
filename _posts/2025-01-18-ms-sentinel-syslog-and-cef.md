---
title: MS Sentinel, Syslog, CEF and Azure Monitor Agent
date: 2025-01-18T05:46:46.188Z
modifieddate: 2025-01-19T14:19:38.794Z
categories:
    - Sentinel
    - Monitoring
    - Security
    - Azure
description: 4 clowns, 2 of which are brothers, looking to stich you up with rubbish messages, complexity, just to be tools.
published: false
preview: ""
draft: true
tags: []
type: posts
layout: posts
fmContentType: posts
---



<!--
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
-->

## TL;DR

Getting CEF Messages into Azure Sentinel is a pain.\
You can easily send far more than you wanted and then you're paying for ingestion / storage you didn't mean to.\
There are some queries to determine how big the problem is.\
We try to filter out the noise getting stored by implementing a simple Azure Monitor Data Collection Rule Transformation.\
We try to filter out the noise getting sent in the first place by modifying the rsyslog ruleset to reduce what gets sent to the Azure Monitoring Agent.\
We cover some methods to monitor / test if they work.
The concept could be adapted to other situations.

## Intro

TBC

<!--- cSpell:disable --->
* [TL;DR](#tldr)
* [Intro](#intro)
* [Scenario](#scenario)
* [Syslog Noise](#syslog-noise)
* [DCR Transformation](#dcr-transformation)
  * [Editing DCRs](#editing-dcrs)
  * [How can I check the DCR Transformation?](#how-can-i-check-the-dcr-transformation)
  * [Is this really a fix?](#is-this-really-a-fix)
* [Rsyslog conf modification](#rsyslog-conf-modification)
  * [How can I check the new Rsyslog config working?](#how-can-i-check-the-new-rsyslog-config-working)
* [Summary](#summary)
* [References](#references)
<!--- cSpell:enable --->

## Scenario

TBC

## Syslog Noise

Here is how I started to determine the level of noise. `DeviceVendor` is part of the [CEF standard](../pages/misc-references.md#cef). So try this in your KQL Query in your Log Analytics Workspace and adjust your time period/limit per your logging load (Start small then increase either the limit or the time range to get an idea):

```kql
CommonSecurityLog
| summarize Count=count() by DeviceVendor
```

Where the device vendor is blank is syslog noise. Also note that those that know syslog facilities better than me may not have chosen the USER facility. I didn't have a choice given of my SIEM integrations.

Where is the noise coming from? I had to muck around with syslog configs to get an idea. But here are some examples I found:

* 2 separate ones for MS Defender for Endpoint in Azure
* Azure Monitor Agent
* I can't remember the 3rd

So we need to reduce the noise. There are two approaches I came to. DCR Transformation & Rsyslog config modification.

## DCR Transformation

MS suggest modifying the DCR with something like this:

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

Creating and Editing DCR's normally requires you to hard code JSON and submit via the API.

"Cool Story Bro, but I really don't want to fuck around that much...". Me either so there is a cheat if your Transformation is simple. Using the Export Template feature of the Azure Portal on the DCR, click deploy and edit the template before you submit it, right over the top of the existing rule.

1. Go to Azure Monitor
2. Go to Settings --> Data Collection Rules
3. Select your Data Collection Rule that gets your syslog's/CEF messages
4. Go to Automation --> Export Template
5. Click Download to take a backup
6. Click Deploy at the top
7. Click Edit Template
8. Find the dataflow section
9. Add in your transformation in a new element. similar to the above example

### How can I check the DCR Transformation?

One thing I found is that its hide to see exactly. Here are some ways:

1. Metrics of the DCR - this one I found the best as you can see Logs coming in, log errors, transformation time.
2. Workbooks on usage of the LAW - esp if its Sentinel enabled.
3. Trying to mirror / watch / capture what the syslog server output.
4. Try the noisy KQL query from above again

### Is this really a fix?

Technically yes, but I understand what you mean. Your still sending a lot of data in the first place, then filtering it out. Depending on the scale, thats money somewhere.

The goal was to also use this as a single (or HA) syslog server for all needs instead of running multiples.

In my situation I got there by setting the CEF Connection via AMA for Sentinel, in which you must choose a SYSLOG facility to bring in and a level. One of my input devices I could change the facility and one I couldn't. So I may be stuck with User/Log_User Facility. But we could get 'creative' with the RSyslog config file as mentioned above. Thats the next step to try.

## Rsyslog conf modification

If you setup log forwarding via:

1. The Azure Monitoring Agent and a DCR
2. Setup the Sentinel CEF Connector and run Forwarder_AMA_installer.py

on your syslog server and you're running Azure Monitoring Agent v1.28 or newer, you will end up with `/etc/rsyslog.d/10-azuremonitoragent-omfwd.conf` being created. It looks like:

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

> [!NOTE] Azure Monitoring Agent before 1.28
> Before 1.28 you will end up with 2 files in `/etc/rsyslog.d/`. This is because AMA uses a Unix Socket to get the syslog's, where after 1.28 its back to like it was in the Log Analytics Agent (something running on a port)

One option to consider is adjusting the rsyslog file. One Idea I was considering stealing was back from when they used the Log Analytics Agent with syslog forwarding:

```bash
if $rawmsg contains "CEF:" or $rawmsg contains "ASA-" then @@127.0.0.1:25226
```

So how does this merging look? Here is my attempt but note i'm not an rsyslog expert.

```bash
# Azure Monitor Agent configuration: forward logs to azuremonitoragent

template(name="AMA_RSYSLOG_TraditionalForwardFormat" type="string" string="<%PRI%>%TIMESTAMP% %HOSTNAME% %syslogtag%%msg:::sp-if-no-1st-sp%%msg%")
# queue.workerThreads sets the maximum worker threads, it will scale back to 0 if there is no activity
# Forwarding all events through TCP port
if $rawmsg contains "CEF:" or $rawmsg contains "ASA-" then {
  action(type="omfwd"
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
}
```

Things you may need to consider with the above script.

* The Azure support tools may not work correctly.
* Forwarder_AMA_installer.py may revert it back
* Sentinel_AMA_troubleshoot.py may not work

### How can I check the new Rsyslog config working?

Using the same Azure Metrics I used for the DCR, I should have seen a drop, but I didn't see a noticeable one. Esp given what I was seeing before the DCR Transformation. The metric of log rows dropped is still high. As such I may need to disable the translate to see how good/bad the rsyslog changes are.

## Summary

* Use DCR KQL Transforms to reduce noise being imported
* Consider adjusting rsyslog.d conf for azure monitoring Agent
* Learn facilities, syslog and the log files and how they work and more importantly, interact

## References

<https://learn.microsoft.com/en-us/azure/sentinel/cef-syslog-ama-overview?tabs=single#data-ingestion-duplication-avoidance>\
<https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/data-collection-transformations-kql>\
<https://www.rsyslog.com/storing-messages-from-a-remote-system-into-a-specific-file/>\
<https://www.rsyslog.com/normalizing-cisco-asa-messages/>\
<https://www.rsyslog.com/doc/configuration/index.html>\
<https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/6/html/deployment_guide/s1-basic_configuration_of_rsyslog#s2-Filters>\
[KQL Queries](../pages/kql-queries.md)\
[AMA DCR LAW](../pages/ama-dcr-law.md)\
[Misc References](../pages/misc-references.md#cef)
