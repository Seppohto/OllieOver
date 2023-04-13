# Custom PowerShell Function: FullPwd
The **FullPwd** function is a simple PowerShell function that displays the full working directory path without truncation. This guide will show you how to create and use the FullPwd function in your PowerShell environment.
## Create a PowerShell Profile (If you don't have one)
1. Open PowerShell.
2. Check if you have a PowerShell profile by running the following command:
```powershell
Test-Path $PROFILE
```
If the result is False, you don't have a profile yet, and you need to create one using the command:
```powershell
New-Item -ItemType File -Path $PROFILE -Force
```
## Add the FullPwd Function to Your Profile
3. Open your PowerShell profile in a text editor (e.g., Notepad) by running the following command:
```powershell
notepad.exe $PROFILE
```
4. Add the FullPwd function to your PowerShell profile:
```powershell
function FullPwd {
    $currentDirectory = Get-Location
    $currentDirectory.Path
}
```
5. Save the changes to the profile and close the text editor.
6. Restart your PowerShell session for the changes to take effect.

## Using the FullPwd Function
Now that you have the FullPwd function in your PowerShell profile, you can use it to display the full working directory path without truncation:

```powershell
FullPwd
```

This command will output the complete path of your current working directory, ensuring that you can view the entire directory path without any truncation, even when the default **pwd** command shortens the path with ellipses.