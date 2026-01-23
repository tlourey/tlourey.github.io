---
title: PowerShell Scripting Tips
description: TBA
published: false
categories:
    - Tech
type: pages
layout: pages
date: 2026-01-23T04:08:07.774Z
lastmod: 2026-01-23T05:08:46.295Z
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
* [Ispresent](#ispresent)
* [optionally pass switch to a cmdlet](#optionally-pass-switch-to-a-cmdlet)
* [Hash table vs array](#hash-table-vs-array)
* [Splatting](#splatting)
* [Importing WindowsPowerShell modules into PowerShel Core (6,7,etc)](#importing-windowspowershell-modules-into-powershel-core-67etc)
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

## Ispresent

if you have a parameter that is a switch you can sometimes do things like `ispresent`

```powershell
function Test-IsPresent {
    param(
        [switch]$MySwitch
    )

    Write-Host "Boolean value of \$MySwitch: $($MySwitch -as [bool])"
    Write-Host "Value of \$MySwitch.IsPresent: $($MySwitch.IsPresent)"

    if ($MySwitch.IsPresent) {
        Write-Host "The parameter -MySwitch was explicitly present in the command."
    } else {
        Write-Host "The parameter -MySwitch was absent from the command."
    }
}

```

## optionally pass switch to a cmdlet

```powershell
param(
 [Parameter(Mandatory = $false, ValueFromPipeline = $true, ValueFromPipelineByPropertyName = $true, Position = 3)]
 [switch]$optionwhenconnectingtothing

connect-tothing -servername bla -importantoption:$optionwhenconnectingtothing
```

## Hash table vs array

Array: <https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_arrays?view=powershell-7.4>

```powershell
# Array
$myarray = @(
  'value1',
  'value2',
  'value3'
)
#Blank array
$myarray = @()
```

Hashtable: <https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_hash_tables?view=powershell-7.4>

```powershell
$Hashtable = @{
  Path = "test.txt"
  Destination = "test2.txt"
  WhatIf = $true
}
$HashTable
```

## Splatting

Splatting: <https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_splatting?view=powershell-7.4>\
<https://learn.microsoft.com/en-us/previous-versions/technet-magazine/gg675931(v=msdn.10)?redirectedfrom=MSDN>

```powershell
$HashArguments = @{
  Path = "test.txt"
  Destination = "test2.txt"
  WhatIf = $true
}
Copy-Item @HashArguments
```

```PowerShell
$ArrayArguments = "test.txt", "test2.txt"
Copy-Item @ArrayArguments -WhatIf
```

Splatting a cmdlet (or at least putting it on multiple lines):

```PowerShell
MyCmdLet `
  -Parameter1 value `
  -Parameter2 value `
  -Parameter3 value
```

> [!NOTE] Weird Behavour
> Now and then, I don't see the splitting a cmdlet over multiple lines always work correctly. It may have some edgecases.

## Importing WindowsPowerShell modules into PowerShel Core (6,7,etc)

<https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/import-module?view=powershell-7.4>\
<https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_windows_powershell_compatibility?view=powershell-7.4>

```powershell
Import-Module LegacyModuleName -UseWindowsPowerShell
```

<!-- cSpell:ignore toolname -->
<!--
## toolname

### toolname Commands

### toolname Notes

### toolname References

<>
-->
