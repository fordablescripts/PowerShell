---
external help file: Get-Packages.xml
Module Name: FordableScripts
online version: 1.0.0
schema: 2.0.0
---

# Get-Packages

```powershell
Function Get-Packages {
    <#
    .SYNOPSIS
    Provides a list of installed packages for Debian-based systems
    .DESCRIPTION
    This function runs the Debian package manager (dpkg) and converts the output to a powershell object.
    .LINK
    https://github.com/fordablescripts/PowerShell/blob/main/Help/Get-Packages.md
    .EXAMPLE
    Get-Installed | Where-Object {$_.Name -like "fire*"} | Select-Object -Property Name, Version | Format-List
    #>
        ((dpkg -l).split("ii")).Trimstart() | 
        Select-Object -Skip 6 | 
        ForEach-Object {$_ -replace '\s{2,}', ', '} | 
        ConvertFrom-Csv -Header Name, Version, Architecture, Description | 
        Select-Object -Property Name, Version, Architecture, Description
}
```


## SYNOPSIS
Provides a list of installed packages for Debian-based systems

## SYNTAX

```
Get-Packages
```

## DESCRIPTION
This function runs the Debian package manager (dpkg) and converts the output into a PowerShell object.

## EXAMPLES

### Example 1
```powershell
PS C:\>Get-Packages | Where-Object {$_.Name -like "fire*"} | Select-Object -Property Name, Version | Format-List
```

Showcases the ability to filter through the data and change formatting as a PowerShell Object.

## PARAMETERS

## INPUTS

### None
## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS
