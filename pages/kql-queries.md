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

* [KQL Functions](#kql-functions)
  * [count](#count)
  * [count\_distinct](#count_distinct)

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
