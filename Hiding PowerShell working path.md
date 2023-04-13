# Hiding PowerShell working path or customizing it

I wanted to remove the path from the pompt. Sometimes the path is just so long that it makes bothers me. So i found out how to do it.

## Create a Profile

1. Open PowerShell.
2.  Check if you have a PowerShell profile by running the following command:
```
Test-Path $PROFILE
```

If the result is False, you don't have a profile yet, and you need to create one using the command:
```
New-Item -ItemType File -Path $PROFILE -Force
```

## modify the profile file to hide the path or customize it

3. Open your PowerShell profile in a text editor (e.g., Notepad) by running the following command:
```
notepad.exe $PROFILE
```
4. Add or modify the prompt function in the opened profile file. To hide the working path completely, you can use a minimal prompt function like this:

```
function prompt {
    return "PS> "
}
```

Or, you can customize the working path display by modifying the function. For example, to display only the current folder name, use the following code:
```
function prompt {
    return (Split-Path -Leaf (Get-Location)) + "> "
}
```
5. Save the changes
6. Restart the PowerShell terminal for the changes to take effect.