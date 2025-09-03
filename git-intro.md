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

### Tagging
#### What is a Tag?
- A tag in Git is like a label or bookmark for a specific commit.  
- Tags are commonly used to mark important points in your project history, like releases, milestones, or hotfixes.

#### Tagging Best Practices
- Use tags to mark releases, major milestones, or stable points.
- Prefer annotated tags (-a -m) for anything public or shared.
- Create tags after passing tests or before releasing code.

#### Type of tags
- lightweight tag:-  just a name for a commit
- annotated tag:- stores tagname, author, the date, and a message, Recommended for releases and sharing with others
  
```
git tag <tagname> - Create a lightweight tag
git tag -a <tagname> -m "message" - Create an annotated tag
git tag -a <tagname> -m "message" <commit-hash> - Tag a specific commit
git tag - List tags
git show <tagname> - Show tag + commit details
git push origin v1.0
git push --tags
git tag -d v1.0 #Delete a tag locally
git push origin --delete tag v1.0 #Delete a tag from remote
git push --tags #Push all tags at once

#Move a tag to a different commit and update the remote:
git tag -f v1.0 <new-commit-hash>
git push --force origin v1.0
```

### Stash
#### What is stash?


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
git reset [file] # unstaged, but file.txt still modified(keeps changes in your working directory)
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

git show <commit_sha> #show the changes in commit
git reset --soft HEAD~1 # to undo the last commit and keep your changes staged when accidentally committed the wrong files.
git reset --hard <commit_sha> #to revert back to the previous commit

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
git config --global color.ui auto #set automatic command line coloring for Git for easy reviewing
git config --global core.editor "code --wait"
git config --global core.autocrlf
git config --global -e #open file .gitconfig for config

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

```
