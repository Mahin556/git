Set upstream tracking branch: To link your local main with the remote main.
```
git branch --set-upstream-to=origin/main main
```

Pull remote changes: `--rebase` keeps your commit history clean (your commits will be applied on top of the remote ones).
```
git pull --rebase origin main
```

Visualize Full History:
```
git log --oneline --graph --all --decorate
```

This downloads all new branches, commits, and tags from the remote (origin) into your local repo.
It does not change your working files or move HEAD; it just updates the remote-tracking references (like origin/main, origin/feat/contact-page).
```
git fetch origin
```

This creates a new local branch called feat/contact-page. It starts from the remote branch origin/feat/contact-page. The -b flag means “create a new branch.”
After running this, your local feat/contact-page will track the remote one.
```
git checkout -b feat/contact-page origin/feat/contact-page
```

Verbose output of git branch
```
git branch -v
git branch -vv
```
