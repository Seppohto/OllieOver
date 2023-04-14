# My Ultimate Git Function for PowerShell: GitGud
GitGud is a simple yet powerful PowerShell function that streamlines your Git workflow by executing the commands **git add .**, **git commit**, **git pull**, and **git push** all in one go. This guide will walk you through the process of creating and using the GitGud function in your PowerShell environment.

## Why these commands?

3. **'git add .'**: This command stages all changes in the working directory, including new files, modified files, and deleted files. Staging changes is the first step in preparing a commit. By automatically including this command in the function, you ensure that all changes are staged before committing.

2. **'git commit'**: This command creates a new commit containing the staged changes. A commit is a snapshot of your project's history, allowing you to track changes over time. The optional -m flag lets you include a commit message that describes the changes made. By integrating this command into the function, you can easily create a new commit for your changes.

3. **'git pull'**: This command fetches changes from the remote repository and merges them into your local branch. By performing a pull before pushing your changes, you ensure that your local branch is up-to-date with the remote repository. This helps prevent conflicts and ensures a smooth collaboration experience.

4. **'git push'**: This command pushes your local commits to the remote repository, making them available to other collaborators. By including this command in the function, you can ensure that your changes are shared with others as soon as they are committed.

By combining these Git commands into a single PowerShell function called 'gitgud', you can streamline your Git workflow and save time. Instead of running each command individually, you can execute the entire sequence of commands with just one function call. This simplifies the process of committing and sharing changes, making it more efficient and user-friendly.

## Create a PowerShell Profile (If you don't have one)

If you haven't already created a PowerShell profile, follow steps [here](https://github.com/Seppohto/OllieOver/blob/main/Creating%20a%20PowerShell%20Profile%20and%20Adding%20a%20HelloWorld%20Function.MD) to create it.

## Add the GitGud Function to Your Profile

1. Open your PowerShell profile in a text editor (e.g., Notepad) by running the following command:
```powershell
notepad.exe $PROFILE
```
2. Add the GitGud function to your PowerShell profile:
```powershell
function gitgud {
    param(
        [Parameter(Position=0)]
        [string]$commitMessage
    )
    
    git add .
    if ($?) {
        if ($commitMessage) {
            git commit -m "$commitMessage"
        } else {
            git commit
        }
    }
    git pull
    if ($?) {
        git push
    }
}
```
3. Save the changes to the profile and close the text editor.
4. Restart your PowerShell session for the changes to take effect.

## Using the GitGud Function

Now that you have the GitGud function in your PowerShell profile, you can use it in the following ways:

- To perform **git add .**, **git commit**, **git pull**, and **git push** with a commit message:
```powershell
gitgud 'Your commit message'
```
- To perform **git add .**, **git commit** (without a commit message), **git pull**, and **git push**:
```powershell
gitgud
```
GitGud simplifies your Git workflow and helps you save time by combining these common Git commands into a single function. With GitGud, you can now manage your code commits and pushes more efficiently in PowerShell.
