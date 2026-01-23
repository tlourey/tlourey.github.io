---
title: PowerShell Scripting Tips
description: TBA
published: false
categories:
    - Tech
type: pages
layout: pages
date: 2026-01-23T04:08:07.774Z
lastmod: 2026-01-23T04:15:52.224Z
tags:
    - PowerShell
    - Tips
    - VSCode
isdraft: true
fmContentType: pages
mermaid: false
preview: ""
keywords:
    - PowerShell
    - Scripting
    - Tips
    - Tricks
---
<!--- cSpell:words -->
<!--- cSpell:ignore -->
<!--- cSpell:disable --->
* [String vs Array of strings in Parameters](#string-vs-array-of-strings-in-parameters)
* [Check if a parameter is populated or not aka Is Null](#check-if-a-parameter-is-populated-or-not-aka-is-null)
<!--- cSpell:enable --->

## String vs Array of strings in Parameters

```powershell
# this variable is a string
[string]$variable
# This means variable takes an array of strings
[string[]]$variable 
```

## Check if a parameter is populated or not aka Is Null

Best way to detect if a parameter is acturally populated or null is by:

```powershell
if ($testparameter) {
  do thing
}
```

This treats it like a bool. Its false if its acturally empty, true if it has anything in it. even a string.

I've often done it the way below but it sometimes has issues.

```powershell
if ($testparameter -eq $null) {
  do thing 
}

# OR 

if (($testparameter -eq $null) -or ($testparameter -eq "") ) {
  do thing
}
```

<!-- cSpell:ignore toolname -->
<!--
## toolname

### toolname Commands

### toolname Notes

### toolname References

<>
-->
