---
title: KQL Queries
description: "KQL Queries to remember"
published: false
categories:
  - References
  - Language
type: pages
draft: true
tags: []
fmContentType: pages
---

[home](/) [up](./)
 <!--- cSpell:disable --->
* [KQL Functions](#kql-functions)
  * [count](#count)
  * [count\_distinct](#count_distinct)
  * [isnotempty](#isnotempty)
* [KQL Queries](#kql-queries)
  * [LAW Table Usage](#law-table-usage)
* [Misc References](#misc-references)
<!--- cSpell:enable --->
## KQL Functions

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

<https://learn.microsoft.com/en-au/kusto/query/count-distinct-aggregation-function?view=microsoft-fabric>
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

<https://learn.microsoft.com/en-us/kusto/query/isnotempty-function?view=azure-monitor>

## KQL Queries

### LAW Table Usage

```kql
union withsource=["$TableName"] *
| summarize Count=count() by TableName=["$TableName"]
| render barchart
```

## Misc References

Notes about KQL for Transformations: [Supported KQL features in Azure Monitor transformations](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/data-collection-transformations-kql)
