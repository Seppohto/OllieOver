# Custom PowerShell Function: FullPwd

The **FullPwd** function is a simple PowerShell function that displays the full working directory path without truncation. This guide will show you how to create and use the FullPwd function in your PowerShell environment.

## Create a PowerShell Profile (If you don't have one)

If you haven't already created a PowerShell profile, follow steps [here](https://github.com/Seppohto/OllieOver/blob/main/Creating%20a%20PowerShell%20Profile%20and%20Adding%20a%20HelloWorld%20Function.MD) to create it.

## Add the FullPwd Function to Your Profile

1. Open your PowerShell profile in a text editor (e.g., Notepad) by running the following command:
```powershell
notepad.exe $PROFILE
```
2. Add the FullPwd function to your PowerShell profile:
```powershell
function FullPwd {
    $currentDirectory = Get-Location
    $currentDirectory.Path
}
```
3. Save the changes to the profile and close the text editor.
4. Restart your PowerShell session for the changes to take effect.

## Using the FullPwd Function

Now that you have the FullPwd function in your PowerShell profile, you can use it to display the full working directory path without truncation:

```powershell
FullPwd
```

This command will output the complete path of your current working directory, ensuring that you can view the entire directory path without any truncation, even when the default **pwd** command shortens the path with ellipses.