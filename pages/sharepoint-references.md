---
title: SharePoint References
description: ""
published: false
categories:
    - Tech
type: pages
layout: pages
draft: true
tags:
    - SharePoint
    - References
fmContentType: pages
lastmod: 2025-01-26T03:50:05.913Z
---

<!--- cSpell:disable --->
* [Concepts](#concepts)
* [Validation Tips](#validation-tips)
* [SharePoint Formulas](#sharepoint-formulas)
  * [Common Formulas](#common-formulas)
* [Microsoft 365 Community Content](#microsoft-365-community-content)
<!--- cSpell:enable --->

## Concepts

* [SharePoint Lists Vs Library](https://sharepointmaven.com/lists-vs-libraries-in-sharepoint-online/)
* There is List/Library Validation and Column Validation
  * Column validation only works for new data entries [^1]
  * List/Library Validation ensures that the data was entered correctly with respect to other columns in the list or library. [^1]
  * A big limitation of the Column Validation I mentioned above is that you can not reference other columns. This is where the list/library validation comes into play. [^1]

[^1]: <https://sharepointmaven.com/how-to-do-column-validation-in-sharepoint/>

## Validation Tips

* If you're having trouble with the formulas try going into the library settings --> Advanced settings then select the column and enter the formula in the classic style interface.
* Today() and Now() seem to not always follow the timezone of the sharepoint site. Google for fixes. They are just semi-shitty workarounds like adding using created/modified dates or doing math to the today function.
  * <https://answers.microsoft.com/en-us/msoffice/forum/all/sharepoint-today-function-not-showing-correct-date/7d094e83-2a60-4d53-b06b-73c575008035> (expand to see app replies)

## SharePoint Formulas

[Examples of common formulas in lists](https://support.microsoft.com/en-us/office/examples-of-common-formulas-in-lists-d81f5f21-2b4e-45ce-b170-bf7ebf6988b3)\
<https://learn.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN>

### Common Formulas

`=[My Column Name] > TODAY()`: Column name must be greater than today's date.

## Microsoft 365 Community Content

[Site Builder/Owner: New Site Checklist](https://learn.microsoft.com/en-us/microsoft-365/community/new-site-checklist)
