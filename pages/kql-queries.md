---
title: KQL Queries
description: KQL Queries to remember
published: true
categories:
    - Tech
type: pages
layout: pages
isdraft: true
tags:
    - Azure_Log_Analytics
    - Azure_Sentinel
    - Language
    - References
    - Security
    - Commands
date: 2025-01-18T16:51:00
lastmod: 2025-03-19T10:25:01.108Z
fmContentType: pages
---

 <!--- cSpell: ignore Kusto --->
 <!--- cSpell:disable --->
* [KQL Language](#kql-language)
  * [Overview](#overview)
  * [Tabular operators](#tabular-operators)
    * [summarize operator](#summarize-operator)
    * [distinct operator](#distinct-operator)
    * [project operator](#project-operator)
    * [count operator](#count-operator)
  * [aggregation function](#aggregation-function)
    * [count aggregation function](#count-aggregation-function)
    * [count\_distinct aggregation function](#count_distinct-aggregation-function)
  * [Scalar functions](#scalar-functions)
    * [isnotempty scalar functions](#isnotempty-scalar-functions)
* [KQL Queries](#kql-queries)
  * [LAW Table Usage](#law-table-usage)
  * [Get Watch List](#get-watch-list)
* [Manage KQL Queries](#manage-kql-queries)
  * [Query Packs](#query-packs)
  * [Export and Import Saved Queries](#export-and-import-saved-queries)
* [Accessing KQL](#accessing-kql)
* [Misc KQL References and Resources](#misc-kql-references-and-resources)
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

[Syntax conventions for reference documentation](https://learn.microsoft.com/en-au/kusto/query/syntax-conventions?view=azure-monitor) - brings the menu to the right place for browsing\
[Best practices for Kusto Query Language queries](https://learn.microsoft.com/en-au/kusto/query/best-practices?view=azure-monitor)

### Tabular operators

#### summarize operator

```kql
StormEvents
| summarize by EventType
```

<https://learn.microsoft.com/en-au/kusto/query/summarize-operator?view=azure-monitor>

#### distinct operator

```kql
StormEvents
| distinct EventType
```

<https://learn.microsoft.com/en-au/kusto/query/distinct-operator?view=azure-monitor>

#### project operator

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

#### count operator

```kql
StormEvents | count
```

<https://learn.microsoft.com/en-au/kusto/query/count-operator?view=azure-monitor>

### aggregation function

#### count aggregation function

```kql
StormEvents
| summarize Count=count() by State
```

```kql
CommonSecurityLog
| summarize Count=count() by DeviceVendor
```

<https://learn.microsoft.com/en-au/kusto/query/count-aggregation-function?view=azure-monitor>

#### count_distinct aggregation function

```kql
StormEvents
| summarize UniqueEvents=count_distinct(EventType) by State
| top 5 by UniqueEvents
```

<https://learn.microsoft.com/en-au/kusto/query/count-distinct-aggregation-function?view=azure-monitor>
<!--- cSpell:disable --->
### Scalar functions

#### isnotempty scalar functions
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

## Manage KQL Queries

### Query Packs

* [ ] Add info about Query Packs

### Export and Import Saved Queries

<https://techcommunity.microsoft.com/discussions/microsoftsentinel/export-and-import-saved-queries-and-functions-from-one-sentinel-workspace-to-ano/1910930>

## Accessing KQL

* [Kusto.Explorer](https://learn.microsoft.com/en-au/kusto/tools/kusto-explorer)
  * [Installing Kusto.Explorer](https://aka.ms/ke)
* [](https://learn.microsoft.com/en-au/kusto/tools/kusto-cli?view=microsoft-fabric)
* [Az.Operational Insights PowerShell Module](https://learn.microsoft.com/en-us/powershell/module/az.operationalinsights/) - namely:
  * [Invoke-AzOperationalInsightsQuery](https://learn.microsoft.com/en-us/powershell/module/az.operationalinsights/invoke-azoperationalinsightsquery)
  * [Get-AzOperationalInsightsSavedSearch](https://learn.microsoft.com/en-us/powershell/module/az.operationalinsights/get-azoperationalinsightssavedsearch)
  * [New-AzOperationalInsightsSavedSearch](https://learn.microsoft.com/en-us/powershell/module/az.operationalinsights/new-azoperationalinsightssavedsearch)
* [Azure PowerShell](https://learn.microsoft.com/en-au/powershell/azure/) - see [Access methods Azure VM Tips](azure-vm-tips.md#access-methods)
* **[Log Analytics Workspaces in Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.OperationalInsights%2Fworkspaces)** - where I do most of my stuff
* [Log Analytics REST API Reference](https://learn.microsoft.com/en-us/rest/api/loganalytics/?view=rest-loganalytics-2025-02-01)
* [Azure Data Explorer](https://dataexplorer.azure.com/) - Web based client (there is also a downloadable client)
* [Advanced Hunting in Microsoft Defender Portal](https://security.microsoft.com/v2/advanced-hunting)

[Using KQL in PowerShell](https://learningbydoing.cloud/blog/query-log-analytics-with-kql-from-powershell/#query-log-analytics-from-powershell)

## Misc KQL References and Resources

* Notes about KQL for Transformations: [Supported KQL features in Azure Monitor transformations](https://learn.microsoft.com/en-au/azure/azure-monitor/essentials/data-collection-transformations-kql)
* **<https://github.com/rod-trent/MustLearnKQL>** - Highly Recommended
* <https://github.com/reprise99/Sentinel-Queries> - Highly Recommended
* <https://github.com/reprise99/awesome-kql-sentinel>
* <https://github.com/Bert-JanP/Hunting-Queries-Detection-Rules>
**<https://www.kqlsearch.com/>**
