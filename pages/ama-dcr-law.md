---
title: Azure Monitoring Agent Data Collection Rules for Log Analytics Workspace
description:
published: false
categories:
- References
- Azure
- Monitoring
type: pages
---

* [Overview](#overview)
* [AMA - Azure Monitoring Agent](#ama---azure-monitoring-agent)
* [DCR - Data Collection Rule](#dcr---data-collection-rule)
  * [Transformation](#transformation)
* [DCE - Data Collection Endpoint](#dce---data-collection-endpoint)
* [LAW - Log Analytics Workspace](#law---log-analytics-workspace)

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
  * Most common transformation is to reduce the amount of data being imported after it has been colelcted
* Must be in same region as the Log Analytics Workspace it is sending things to

### Transformation

TBC - Most common transformation is: [Data ingestion duplication avoidance](https://learn.microsoft.com/en-us/azure/sentinel/cef-syslog-ama-overview?tabs=single#data-ingestion-duplication-avoidance)

* free if not adding data
* Easist way to modify
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

## DCE - Data Collection Endpoint

TBC

## LAW - Log Analytics Workspace

TBC