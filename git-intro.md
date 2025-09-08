### What is Version control?
```
version control in a process of tracking and managing all tha changes in source code.
```

what is git?
```
- Tracker --> track the changes in the files
- Git is open-source distributed version control system (DVCS) which track and manage the changes in code base.
- We can use Git privately as well as publically.
- Git was developed by Linus Torvalds in 2005 for Linux kernel development. 
```

what is github?
```
GitHub, a hosting service(remote server,which is public) for Git repositories, allows you to access and download projects from any computer. Here’s what you can do with GitHub:
  Store Repositories: GitHub hosts your repositories.
  Collaborate: Work with other developers from any location.
  Version Control: Manage collaborative workflows using Git and GitHub.
```

### Files
```
.git
.gitignore

```


### Init
```
git init
git init .
git init ./demo/
```


```
git --version
git -v
git clone <repo>
git status - See what is staged
git status -s
git restore <file>
git restore --staged <file> - Unstage a file == git reset HEAD <file_name>
git reset [file] # unstaged, but file.txt still modified(keeps changes in your working directory)
git rm --cached <file>


git show <commit_sha> #show the changes in commit
git reset --soft HEAD~1 # to undo the last commit and keep your changes staged when accidentally committed the wrong files.
git reset --hard <commit_sha> #to revert back to the previous commit



git diff #Shows differences between the working directory and the staging area
git diff --staged (or --cached) #Shows differences between the staging area and the last commit.

git blame <file_path>  #show what changed in file, who changed and when

git revert <commit_sha> #to revert the changes of specifc commit and commit that revert

git remote add [alias] [url]   # Add a Git URL as an alias
git fetch [alias]              # Fetch all branches from that remote
git merge [alias]/[branch]     # Merge a remote branch into current branch
git push [alias] [branch]      # Push local commits to remote branch
git pull                       # Fetch + merge changes from remote
git rm [file]                         # Delete file and stage removal
git mv [old-path] [new-path]          # Move/rename file and stage move
git log --stat -M                     # Show commit logs with renamed/moved paths

git push --all

git clean -f    # to remove all untracked file from the dir

```
