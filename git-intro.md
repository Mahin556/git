### What is Version control?
```
version control in a process of tracking and managing all tha changes in source code.
```

what is git?
```
Git is open-source distributed version control system (DVCS) which track and manage the changes in code base.
We can use Git privately as well as publically.
Git was developed by Linus Torvalds in 2005 for Linux kernel development. 
```

what is github?
```
GitHub, a hosting service for Git repositories, allows you to access and download projects from any computer. Here’s what you can do with GitHub:
Store Repositories: GitHub hosts your repositories.
Collaborate: Work with other developers from any location.
Version Control: Manage collaborative workflows using Git and GitHub.
```

### Files
```
.git
.gitignore

```


```
git --version
git -v
git clone <repo>
git add <file> - Stage a file
git add .
git add *
git add --all or git add -A - Stage all changes
git status - See what is staged
git status -s
git restore <file>
git restore --staged <file> - Unstage a file == git reset HEAD <file_name>
git rm --cached <file>
git commit -m "message" - Commit staged changes with a message
git commit -a -m "message" - Commit all tracked changes (skip staging) but not work with new/untracked file only work with modified/deleted file
git log #See commit history
git log --oneline #shorter view
git log --stat #see which files changed in each commit
git commit #add commit in message file or add multi-line commit
git commit --amend #to add files to your last commit.
git commit --amend --no-edit #Quickly add staged changes to last commit, keep message
git commit -a  ---> add + commit
git commit --allow-empty -m "Start project" #Create an empty commit
git commit --no-edit #Use previous commit message (no editor)
git commit --amend -m "Corrected message" #to fix typo in last commit message
git reset --soft HEAD~1 # to undo the last commit and keep your changes staged when accidentally committed the wrong files.
git config credential.helper "cache --timeout=3600"
git config --list
git config --local --list
git config user.name
git config --local user.name
git config --global --list 
git config --system --list 
git config --system user.name
git config --system user.name "Your Name"
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global --unset code.editor
git config --global init.defaultBranch main
```
