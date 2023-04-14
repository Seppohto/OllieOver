# Our Ultimate Git Function for Bash: GitGud
GitGud is a simple yet powerful Bash function that streamlines your Git workflow by executing the commands git add ., git commit, git pull, and git push all in one go. This guide will walk you through the process of creating and using the GitGud function in your Bash environment.

## Add the GitGud Function to Your Bash Profile
1. Open your Bash profile (.bashrc or .bash_profile) in a text editor (e.g., nano, vim) by running one of the following commands:
```bash
vim ~/.bashrc
```

or

```bash
vim ~/.bash_profile
```
2. Add the GitGud function to your Bash profile:
```bash
gitgud() {
    commit_message="$1"

    git add .
    if [ $? -eq 0 ]; then
        if [ -n "$commit_message" ]; then
            git commit -m "$commit_message"
        else
            git commit
        fi
    fi
    git pull
    if [ $? -eq 0 ]; then
        git push
    fi
}
```
3. Save the changes to the profile and close the text editor.
4. Restart your terminal session or source your Bash profile for the changes to take effect:
```bash
source ~/.bashrc
```
or

```bash
source ~/.bash_profile
```
## Using the GitGud Function
Now that you have the GitGud function in your Bash profile, you can use it in the following ways:

- To perform git add ., git commit, git pull, and git push with a commit message:
```bash
gitgud "Your commit message"
```
- To perform git add ., git commit (without a commit message), git pull, and git push:
```bash
gitgud
```

GitGud simplifies your Git workflow and helps you save time by combining these common Git commands into a single function. With GitGud, you can now manage your code commits and pushes more efficiently in Bash.
