To compare 2 branches: to update remote-tracking branches, you need to type `git fetch` first and then:
```
git diff <local branch> <remote>/<remote branch>
git diff origin/main #compare current with remote
git diff main origin/main #compare main with remote
```
Compare 2 commits
```
git diff <hash_commit1> <hash_commit2>
```

List all branchs(local,remote)
```
git branch -a
```
git fetch
```
git fetch
git fetch <remote> <branch>
git fetch upstream main
```

Merge the changes: we can merge the current branch `main` with remote branch `origin/main`.
```
git merge origin/master
```
git pull: pull is a combination of `fetch` and `merge`. It is used to pull all changes from a remote repository into the branch you are working on.
```
git pull
```
git push
```
git push origin
```

To see logs of remote
```
git log origin/master
```

This will first fetch the changes from your default remote (origin). This will be created automatically when you clone a repository. You can also be explicit: `git fetch origin master`.

I usually do `git diff <remote>/<remote branch> <local branch>` to see what my push will do to remote repo.

The even shorter `git diff origin` is sufficient if you just compare with your upstream branch.

