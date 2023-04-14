# Custom PowerShell Functions: Grep-like Search Functions

In this guide, we will create a collection of grep-like search functions for your PowerShell environment. These functions will enable you to search for patterns in objects, JSON objects, and files.

## Create a PowerShell Profile (If you don't have one)

If you haven't already created a PowerShell profile, follow steps [here](https://github.com/Seppohto/OllieOver/blob/main/Creating%20a%20PowerShell%20Profile%20and%20Adding%20a%20HelloWorld%20Function.MD) to create it.

## Add the Search Functions to Your Profile

1. Open your PowerShell profile in a text editor (e.g., Notepad) by running the following command:
```powershell
notepad.exe $PROFILE
```
2. Add the search functions to your PowerShell profile:
```powershell
function SearchObject {
    param(
        [Parameter(ValueFromPipeline=$true)]
        [PSObject]$InputObject,

        [Parameter(Position=0)]
        [string]$Pattern
    )

    Process {
        $InputObject | Where-Object { $_ -match $Pattern }
    }
}
Set-Alias -Name GrepObject -Value SearchObject

function SearchJsonObjectsReturnObjects {
    param(
        [Parameter(ValueFromPipeline=$true)]
        [string]$InputObject,

        [Parameter(Position=0)]
        [string]$Pattern
    )

    Begin {
        $inputData = ""
    }

    Process {
        $inputData += $InputObject
    }

    End {
        $jsonObjects = $inputData | ConvertFrom-Json
        $jsonObjects | Where-Object { $_ -match $Pattern }
    }
}
Set-Alias -Name GrepJsonObjectsReturnObjects -Value SearchJsonObjectsReturnObjects

function SearchJsonObjectsReturnJson {
    param(
        [Parameter(ValueFromPipeline=$true)]
        [string]$InputObject,

        [Parameter(Position=0)]
        [string]$Pattern
    )

    Begin {
        $inputData = ""
    }

    Process {
        $inputData += $InputObject
    }

    End {
        $jsonObjects = $inputData | ConvertFrom-Json
        $filteredJsonObjects = $jsonObjects | Where-Object { $_ -match $Pattern }
        $filteredJsonObjects | ConvertTo-Json
    }
}
Set-Alias -Name GrepJsonObjectsReturnJson -Value SearchJsonObjectsReturnJson

function Search {
    param(
        [Parameter(ValueFromPipeline=$true)]
        [string[]]$InputObject,

        [Parameter(Position=0)]
        [string]$Pattern,

        [Parameter(Position=1)]
        [Alias("W")]
        [switch]$WordMatch
    )

    Process {
        $options = @{}

        if ($WordMatch) {
            $Pattern = "\b$Pattern\b"
        }

        $InputObject | Select-String -Pattern $Pattern @options
    }
}
Set-Alias -Name Grep -Value Search
```
3. Save the changes to the profile and close the text editor.

4. Restart your PowerShell session for the changes to take effect.

## Using the Search Functions

Now that you have the search functions in your PowerShell profile, you can use them as follows:

### Search for patterns in objects:
```powershell
Get-Process | GrepObject "edge"
```
In Azure with az cli I use it to find 'mytestvm' when I dont remember the names

```powershell
az vm list | GrepObject "test"
```

### Search for patterns in JSON objects and return objects:

When i query Azure it returns the results often as Json. Thats why I created next two functions. GrepJsonObjectsReturnObjects look prettier but in json form the result show more information and that's why i have GrepJsonObjectsReturnJson

```powershell
az vm list | GrepJsonObjectsReturnObjects "test"
```
Search for patterns in JSON objects and return JSON:
```powershell
az vm list | GrepJsonObjectsReturnJson "test"
```

#### you can use it for other jsondata too

```powershell
$jsonData | GrepJsonObjectsReturnObjects "username"
```
Search for patterns in JSON objects and return JSON:
```powershell
$jsonData | GrepJsonObjectsReturnJson "username"
```

### Search for patterns in files:
```powershell
Get-Content .\testfile.txt | Grep "specific"
```

or with azure to find all subs with specific string

```powershell
az account list | Grep "Test"
```
### Search for whole words in files:
```powershell
Get-Content .\testfile.txt | Grep "specific" -WordMatch
```
### Search for whole words in files using the `-W` alias:

```powershell
Get-Content .\testfile.txt | Grep "specific" -W
```
# That's it

These grep-like search functions provide a powerful way to search for patterns in various types of input, including objects, JSON objects, and files, and can be easily customized to suit your specific needs.

Maybe I'll develope this more if the need arise. I just wanted easier way than PowerShell native ways to search stuff. Since it uses PowerShell anyone could do better job just by using the native commands but this is good enough for me now. 