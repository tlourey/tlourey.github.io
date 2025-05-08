---
title: Excel Tips
description: Random things to remember with Excel
published: true
categories:
    - Tech
type: pages
layout: pages
date: 2025-04-09T08:13:44.845Z
lastmod: 2025-04-27T13:34:38.448Z
tags:
    - Office
    - Tips
    - References
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

**<https://support.microsoft.com/en-au/office/Formulas-and-functions-294d9486-b332-48ed-b489-abe7d0f9eda9>**

<https://support.microsoft.com/en-au/office/excel-functions-by-category-5f91f4e9-7b42-46d2-9bd1-63f26a86c0eb>\
<https://support.microsoft.com/en-au/office/excel-functions-alphabetical-b3944572-255d-4efb-bb96-c6d90033e188>\
<https://support.microsoft.com/en-au/office/logical-functions-reference-e093c192-278b-43f6-8c3a-b6ce299931f5>\
<https://support.microsoft.com/en-au/office/lookup-and-reference-functions-reference-8aa21a3a-b56a-4055-8257-3ec89df2b23e>\
<https://support.microsoft.com/en-au/office/date-and-time-functions-reference-fd1b5961-c1ae-4677-be58-074152f97b81>\
<https://support.microsoft.com/en-au/office/text-functions-reference-cccd86ad-547d-4ea9-a065-7bb697c2a56e>\
<https://support.microsoft.com/en-au/office/statistical-functions-reference-624dac86-a375-4435-bc25-76d659719ffd>\
<https://support.microsoft.com/en-au/office/math-and-trigonometry-functions-reference-ee158fd6-33be-42c9-9ae5-d635c3ae8c16>

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
|---|---|---|
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

[ROUNDUP](https://support.microsoft.com/en-au/office/roundup-function-f8bc9b23-e795-47db-8703-db171d0c42a7): `=ROUNDUP(number, num_digits)`\
[ROUNDDOWN](https://support.microsoft.com/en-au/office/rounddown-function-2ec94c73-241f-4b01-8c6f-17e6d7968f53): `=ROUNDDOWN(number, num_digits)`\
[ROUND](https://support.microsoft.com/en-au/office/round-function-c018c5d8-40fb-4053-90b1-b3e7f61a213c): `=ROUND(number, num_digits)`

|Formula|Description|Result|
|---|---|---|
|=ROUND(2.15, 1)|Rounds 2.15 to one decimal place|2.2|
|=ROUND(2.149, 1)|Rounds 2.149 to one decimal place|2.1|
|=ROUND(-1.475, 2)|Rounds -1.475 to two decimal places|-1.48|
|=ROUND(21.5, -1)|Rounds 21.5 to one decimal place to the left of the decimal point|20|
|=ROUND(626.3,-3)|Rounds 626.3 to the nearest multiple of 1000|1000|
|=ROUND(1.98,-1)|Rounds 1.98 to the nearest multiple of 10|0|
|=ROUND(-50.55,-2)|Rounds -50.55 to the nearest multiple of 100|-100|

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
