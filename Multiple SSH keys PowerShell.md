# Multiple SSH keys PowerShell

Here's how you can set up multiple SSH keys in Powershell:
If you're using Windows 11, SSH should be installed automatically. 

## Generate Multiple SSH Keys:

```
ssh-keygen -t rsa -b 4096 -C "your-email@example.com" -f C:\Users\YourUsername\.ssh\id_rsa_account1
```

## Add SSH Keys to the SSH Agent:

```powershell
Start-Service ssh-agent
```
then add keys
```powershell
ssh-add C:\Users\YourUsername\.ssh\id_rsa_account1
```

## Add SSH Keys to GitHub Accounts:
- Copy the public key to clipboard:
```powershell
Get-Content C:\Users\YourUsername\.ssh\id_rsa_account1.pub | Clip
```

- Go to GitHub -> Settings -> SSH and GPG keys.
- Click on "New SSH key" and paste the copied public key.
- Repeat for other accounts or projects as needed.

## Create an SSH Config File:
To manage multiple SSH keys, create or modify the SSH config file. Edit the C:\Users\YourUsername\.ssh\config file (or create it if it doesn't exist):
```powershell
notepad C:\Users\YourUsername\.ssh\config
```
asd
```powershell
# Account 1
Host github-account1
    HostName github.com
    User git
    IdentityFile C:/Users/YourUsername/.ssh/id_rsa_account1

# Account 2 (if applicable)
Host github-account2
    HostName github.com
    User git
    IdentityFile C:/Users/YourUsername/.ssh/id_rsa_account2
```

# All done!

Now you can use multeiple SSH-keys with Git.
