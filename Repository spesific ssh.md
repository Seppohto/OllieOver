create a folder for repo
do
```powershell
git init
``` 
then go to that folder and run 
```powershell
git config --local -e 
```


add a line 
```powerwshell
[core]
    sshCommand = ssh -i ~/.ssh/id_rsa_metso
```