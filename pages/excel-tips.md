---
title: Excel Tips
description: Random things to remember with Excel
published: false
categories:
    - Tech
type: pages
layout: pages
date: 2025-04-09T08:13:44.845Z
lastmod: 2025-04-09T14:09:22.758Z
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
  * [Date Stuff](#date-stuff)
* [Formatting](#formatting)
  * [Custom Formatting](#custom-formatting)
* [Pivots](#pivots)
* [OfficeScript instead of Macros](#officescript-instead-of-macros)
* [Misc Office Links](#misc-office-links)
<!--- cSpell:enable --->

## Formulas

### Subtotal instead of sum

<https://support.microsoft.com/en-au/office/subtotal-function-7b027003-f060-4ade-9040-e478765b9939>

* Represents a partial sum or total of a specific group or section within a larger set of data.
* Used when you want to calculate a total for a portion of the data, before calculating the overall total.
* Example: "The subtotal of the first three items is $100".
* In Excel, the SUBTOTAL function can be used to calculate subtotals, even when rows are hidden, making it useful for filtered data.

Example: `=SUBTOTAL(9,C1,C2:C3)`: Sums the ranges

`=SUBTOTAL(function_num,ref1,[ref2],...)`

The SUBTOTAL function syntax has the following arguments:

* Function_num: Required. The number 1-11 or 101-111 that specifies the function to use for the subtotal. 1-11 includes manually-hidden rows, while 101-111 excludes them; filtered-out cells are always excluded.

|Function_num\ (includes hidden rows)| Function_num\ (ignores hidden rows) | Function|
|-|-|-|
|1|101|AVERAGE|
|2|102|COUNT|
|3|103|COUNTA|
|4|104|MAX|
|5|105|MIN|
|6|106|PRODUCT|
|7|107|STDEV|
|8|108|STDEVP|
|9|109|SUM|
|10|110|VAR|
|11|111|VARP|

* Ref1     Required. The first named range or reference for which you want the subtotal.
* Ref2,...     Optional. Named ranges or references 2 to 254 for which you want the subtotal.

### Xlookup instead of just Vlookup

* [ ] Xlookup

### Rounding

* [ ] Rounding

### Search Cell for Text

`=ISNUMBER(SEARCH("substringtosearchfor",A2))`: search another cell for text and return a true or false

### Timestamp and Timezone conversions

Convert ISO 8601 format timestamp: `=(DATEVALUE(MID(A2,1,10))+TIMEVALUE(MID(A2,12,8)))`[^1]\
Also add some time (10 hours to convert to AEST): `=(DATEVALUE(MID(A2,1,10))+TIMEVALUE(MID(A2,12,8)))+TIME(10,0,0)`

> [!TIP] Custom Formatting
> Don't forget the [Custom Formatting](#custom-formatting)

[^1]: <https://stackoverflow.com/questions/4896116/parsing-an-iso8601-date-time-including-timezone-in-excel>

### Date Stuff

`=DATEDIF` - older formula

* [ ] More Date Stuff

## Formatting

### Custom Formatting

`d/mm/yyyy h:mm`: date and time with 24h time\
`d/mm/yyyy h:mm AM/PM`: Date and time with 12h time **(Non-Standard)**

## Pivots

* [ ] Add PivotTable Stuff

## OfficeScript instead of Macros

* [ ] Add OfficeScript

## Misc Office Links
