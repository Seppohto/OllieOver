# Hiding PowerShell Working Path or Customizing It

If you find the PowerShell prompt with the working path too long or bothersome, you can hide it or customize it. Here's how to do it:

## Create a PowerShell Profile (If you don't have one)

If you haven't already created a PowerShell profile, follow steps [here](https://github.com/Seppohto/OllieOver/blob/main/Creating%20a%20PowerShell%20Profile%20and%20Adding%20a%20HelloWorld%20Function.md) to create it.

## modify the profile file to hide the path or customize it

1. Open your PowerShell profile in a text editor (e.g., Notepad) by running the following command:
```powershell
notepad.exe $PROFILE
```
2. Add or modify the prompt function in the opened profile file. To hide the working path completely, you can use a minimal prompt function like this:

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
3. Save the changes
4. Restart the PowerShell terminal for the changes to take effect.

## Customize other stuff

To customize the displayed path, modify the prompt function in your PowerShell profile. For example, you can change the path color or add custom text:

```powershell
function prompt {
    $path = $(Get-Location).Path
    $customText = "My Custom Text: "
    $foregroundColor = "Cyan"

    Write-Host -NoNewline -ForegroundColor $foregroundColor $customText
    Write-Host -NoNewline -ForegroundColor $foregroundColor $path
    Write-Host -NoNewline -ForegroundColor $foregroundColor " > "

    return " "
}
```
This code sets the prompt to display the custom text "My Custom Text: ", followed by the current path in cyan, and then a "> " symbol. You can customize the $customText, $foregroundColor, and other elements as desired.

Now, your PowerShell prompt should display the customized path or hide it based on your preference. You can continue to modify the prompt function to further personalize your PowerShell experience.