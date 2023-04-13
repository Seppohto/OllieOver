# Hiding PowerShell Working Path or Customizing It
If you find the PowerShell prompt with the working path too long or bothersome, you can hide it or customize it. Here's how to do it:

## Create a Profile
1. Open PowerShell.
2. Check if you have a PowerShell profile by running the following command:
```powershell
Test-Path $PROFILE
```

If the result is False, you don't have a profile yet, and you need to create one using the command:
```powershell
New-Item -ItemType File -Path $PROFILE -Force
```

## modify the profile file to hide the path or customize it
3. Open your PowerShell profile in a text editor (e.g., Notepad) by running the following command:
```powershell
notepad.exe $PROFILE
```
4. Add or modify the prompt function in the opened profile file. To hide the working path completely, you can use a minimal prompt function like this:

```powershell
function prompt {
    return "PS> "
}
```

Alternatively, you can customize the working path display by modifying the function. For example, to display only the current folder name, use the following code:
```powershell
function prompt {
    return (Split-Path -Leaf (Get-Location)) + "> "
}
```
5. Save the changes
6. Restart the PowerShell terminal for the changes to take effect.