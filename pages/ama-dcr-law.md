---
title: Azure Monitoring Data Collection Rules for Log Analytics Workspace
description: Ripe and ready for TLAs and FLTLAs
published: true
categories:
    - References
    - Azure
    - Monitoring
type: pages
draft: true
lastmod: 2025-01-19T07:14:02.656Z
date: 2025-01-15T01:07:00
---

[home](/) [up](./)
<!--- cSpell:disable --->
* [Overview](#overview)
* [AMA - Azure Monitoring Agent](#ama---azure-monitoring-agent)
* [DCR - Data Collection Rule](#dcr---data-collection-rule)
  * [Transformation](#transformation)
* [DCE - Data Collection Endpoint](#dce---data-collection-endpoint)
* [LAW - Log Analytics Workspace](#law---log-analytics-workspace)
* [Streams and Data Sources](#streams-and-data-sources)
* [Misc References](#misc-references)
<!--- cSpell:enable --->
## Overview

DCR --> AMA --> DCE --> LAW

## AMA - Azure Monitoring Agent

* Installed when you create an Azure VM
* Can be updated / controlled via Azure Portal for in VM Extensions

## DCR - Data Collection Rule

* Applies via Azure Monitor (portal, PS, API, etc)
* Defines the VMs (or services/resources) the DCR applies to
* Defines the things it collections
* Defines the destination for those things
* Can define transformations of those things to the destination.
  * Most common transformation is to reduce the amount of data being imported after it has been collected
* Must be in same region as the Log Analytics Workspace it is sending things to

### Transformation

TBC - Most common transformation is: [Data ingestion duplication avoidance](https://learn.microsoft.com/en-us/azure/sentinel/cef-syslog-ama-overview?tabs=single#data-ingestion-duplication-avoidance)

* free if not adding data
* Easiest way to modify
  1. Make in portal
  2. Deploy
  3. Go to export template
  4. download a copy
  5. Find the dataflow section
  6. add in your transformation in a new element. eg

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
```

This didn't work for me... So, I tried this:

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
```

> [!TIP] Microsoft-CommonSecurityLog
> My Microsoft-CommonSecurityLog was underlined yellow and saying it wasn't valid. It still accepted it and it still worked. This may have been an issue since I moved my sentinel-enabled LAW around. I also noted that when typing it in I had to add a space that before the <!--- cSpell:disable --->`transformkql`<!--- cSpell:enable ---> came up in the drop down so I knew what I was doing was 'somewhat' valid.

Notes about KQL for Transformations: [Supported KQL features in Azure Monitor transformations](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/data-collection-transformations-kql)

## DCE - Data Collection Endpoint

Apparently not needed unless using Azure Private Link. I think can be used if you have some machines that can't see the internet without private link but not sure.

## LAW - Log Analytics Workspace

TBC

## Streams and Data Sources

From [Structure of a data collection rule (DCR) in Azure Monitor](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/data-collection-rule-structure)

[Input-streams](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/data-collection-rule-structure#input-streams):

* If this is a standard data type such as a Windows event, then the stream will be in the form Microsoft-\<TableName\>. If it's a custom type, then it will be in the form Custom-\<TableName\>
* [Valid Source Types](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/data-collection-rule-structure#valid-data-source-types) - there are more
* [Full list of 240 possible streams values (Oct 20, 2022)](https://github.com/Azure/azure-rest-api-specs/issues/21200#:~:text=Full%20list%20of%20240%20possible%20streams%20values)

[Azure Monitor data sources and data collection methods](https://learn.microsoft.com/en-us/azure/azure-monitor/data-sources)

## Misc References

<https://learn.microsoft.com/en-us/azure/azure-monitor/agents/troubleshooter-ama-windows?tabs=WindowsPowerShell#linux-troubleshooter>\
<https://learn.microsoft.com/en-us/azure/azure-monitor/agents/troubleshooter-ama-linux?tabs=redhat%2CGenerateLogs>
