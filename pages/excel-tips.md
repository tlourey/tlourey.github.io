---
title: Excel Tips
description: Random things to remember with Excel
published: false
categories:
    - Tech
type: pages
layout: pages
date: 2025-04-09T08:13:44.845Z
lastmod: 2025-04-09T08:54:39.168Z
tags:
    - Office
isdraft: true
fmContentType: pages
mermaid: false
preview: ""
---

<!--- cSpell:disable --->
* [Formulas](#formulas)
  * [Subtotal instead of sum](#subtotal-instead-of-sum)
  * [Xlookup instead of just Vlookup](#xlookup-instead-of-just-vlookup)
  * [Rounding](#rounding)
  * [Search Cell for Text](#search-cell-for-text)
  * [Timestamp and Timezone conversions](#timestamp-and-timezone-conversions)
* [Formatting](#formatting)
  * [Custom Formatting](#custom-formatting)
* [Pivots](#pivots)
* [OfficeScript instead of Macros](#officescript-instead-of-macros)
* [Misc Office Links](#misc-office-links)
<!--- cSpell:enable --->

## Formulas

### Subtotal instead of sum

### Xlookup instead of just Vlookup

### Rounding

### Search Cell for Text

`=ISNUMBER(SEARCH("substringtosearchfor",A2))`: search another cell for text and return a true or false

### Timestamp and Timezone conversions

Convert ISO 8601 format timestamp: `=(DATEVALUE(MID(A2,1,10))+TIMEVALUE(MID(A2,12,8)))`[^1]\
Also add some time (10 hours to convert to AEST): `=(DATEVALUE(MID(A2,1,10))+TIMEVALUE(MID(A2,12,8)))+TIME(10,0,0)`

> [!TIP] Custom Formatting
> Don't forget the [Custom Formatting](#custom-formatting)

[^1]: <https://stackoverflow.com/questions/4896116/parsing-an-iso8601-date-time-including-timezone-in-excel>

## Formatting

### Custom Formatting

`d/mm/yyyy h:mm`: date and time with 24h time\
`d/mm/yyyy h:mm AM/PM`: Date and time with 12h time **(Non-Standard)**

## Pivots

## OfficeScript instead of Macros

## Misc Office Links
