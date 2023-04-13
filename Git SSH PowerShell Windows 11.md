# Setting Up Git SSH in Powershell
If you're using Windows 11, SSH should be installed automatically. Here's how you can set up Git SSH in Powershell:

## Check if key exists
```
Get-ChildItem -Path ~/.ssh/id_rsa.pub
```
## Generate a key
```
ssh-keygen.exe
```
You can click enter multiple times to accept the default settings, or choose a passphrase and other options.

## Copy the key

```
Get-Content -Path ~/.ssh/id_rsa.pub | Clip
```
## Add the key to GitHub
1. Go to GitHub and open settings
2. Navigate to SSH and GPG keys
3. Click "New SSH key" and paste the key there
4. Save it

# All done!
Now you can use SSH with Git.

## Quick Git Push Command
If you want to push changes quickly, use the following command in Bash:


```
git add . ; if ($?) { git commit } ; git pull ; if ($?) { git push }
```
This command will add all the files, commit changes, pull from the remote repository, and push the changes to the remote repository.