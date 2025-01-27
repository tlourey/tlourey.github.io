---
title: KQL Queries
description: KQL Queries to remember
published: true
categories:
    - Tech
type: pages
layout: pages
draft: true
tags:
    - Language
    - References
    - Azure Sentinel
    - Azure Log Analytics
fmContenttype: pages
date: 2025-01-18T16:51:00
lastmod: 2025-01-27T15:40:11.394Z
---


 <!--- cSpell:disable --->
* [KQL Language](#kql-language)
  * [Overview](#overview)
  * [count](#count)
  * [count\_distinct](#count_distinct)
  * [isnotempty](#isnotempty)
  * [project](#project)
* [KQL Queries](#kql-queries)
  * [LAW Table Usage](#law-table-usage)
  * [Get Watch List](#get-watch-list)
* [Misc References](#misc-references)
<!--- cSpell:enable --->

## KQL Language

### Overview

[Kusto](https://learn.microsoft.com/en-us/kusto/?view=azure-monitor)\
[KQL](https://learn.microsoft.com/en-us/kusto/query/?view=azure-monitor)\
[KQL Quick Reference](https://learn.microsoft.com/en-us/kusto/query/kql-quick-reference?view=azure-monitor)\
[KQL Learning Resources](https://learn.microsoft.com/en-us/kusto/query/kql-learning-resources?view=azure-monitor)\
[Learn Common Operators](https://learn.microsoft.com/en-us/kusto/query/tutorials/learn-common-operators?view=azure-monitor)\
[SQL to KQL Cheat Sheet](https://learn.microsoft.com/en-us/kusto/query/sql-cheat-sheet?view=azure-monitor)\
[KQL Regex](https://learn.microsoft.com/en-us/kusto/query/regex?view=azure-monitor)\
[KQL Timezones](https://learn.microsoft.com/en-us/kusto/query/timezone?view=azure-monitor)

### count

```kql
StormEvents
| summarize Count=count() by State
```

```kql
CommonSecurityLog
| summarize Count=count() by DeviceVendor
```

<https://learn.microsoft.com/en-au/kusto/query/count-aggregation-function?view=microsoft-fabric>

### count_distinct

```kql
StormEvents
| summarize UniqueEvents=count_distinct(EventType) by State
| top 5 by UniqueEvents
```

<https://learn.microsoft.com/en-au/kusto/query/count-distinct-aggregation-function?view=azure-monitor>
<!--- cSpell:disable --->
### isnotempty
<!--- cSpell:enable --->
```kql
StormEvents
| where isnotempty(BeginLat) and isnotempty(BeginLon)
```

```kql
CommonSecurityLog
| where isnotempty(DeviceVendor)
```

<https://learn.microsoft.com/en-au/kusto/query/isnotempty-function?view=azure-monitor>

### project

Allows limiting of columns

```kql
StormEvents
| project State
```

<https://learn.microsoft.com/en-au/kusto/query/project-operator?view=azure-monitor>

Other project related operators:

* [project-away-operator](https://learn.microsoft.com/en-au/kusto/query/project-away-operator?view=azure-monitor)
* [project-keep-operator](https://learn.microsoft.com/en-au/kusto/query/project-keep-operator?view=azure-monitor)
* [project-rename-operator](https://learn.microsoft.com/en-au/kusto/query/project-rename-operator?view=azure-monitor)
* [project-reorder-operator](https://learn.microsoft.com/en-au/kusto/query/project-reorder-operator?view=azure-monitor)

## KQL Queries

### LAW Table Usage

```kql
union withsource=["$TableName"] *
| summarize Count=count() by TableName=["$TableName"]
| render barchart
```

### Get Watch List

```kql
_GetWatchlist('NetworkAddresses')
| extend IPSubnet = ["IP Subnet"]
| extend RangeName = ["Range Name"]
| project IPSubnet,RangeName
```

## Misc References

Notes about KQL for Transformations: [Supported KQL features in Azure Monitor transformations](https://learn.microsoft.com/en-au/azure/azure-monitor/essentials/data-collection-transformations-kql)\
<https://github.com/rod-trent/MustLearnKQL>\
<https://github.com/reprise99/Sentinel-Queries>\
<https://github.com/reprise99/awesome-kql-sentinel>\
<https://github.com/Bert-JanP/Hunting-Queries-Detection-Rules>\
<https://www.kqlsearch.com/>
