

## 🔹 1. Change the **most recent commit message**

If it’s the **last commit**, run:

```bash
git commit --amend -m "New commit message"
```

👉 This updates the message of the latest commit.
⚠️ If you already pushed it, you’ll need:

```bash
git push origin branch-name --force
```

---

## 🔹 2. Change an **older commit message**

Use **interactive rebase**:

```bash
git rebase -i HEAD~N
```

(where `N` = how many commits back you want to edit, e.g. `HEAD~5` for the last 5 commits).

You’ll see something like:

```
pick a1b2c3 First commit
pick d4e5f6 Add login page
pick g7h8i9 Fix bug in routes
```

* Change `pick` to `reword` (or `r`) for the commit whose message you want to edit:

```
pick a1b2c3 First commit
reword d4e5f6 Add login page
pick g7h8i9 Fix bug in routes
```

* Save & close.
* Git will open an editor to let you change that commit message.

Finally:

```bash
git rebase --continue
```

If you already pushed the old commit, force push:

```bash
git push origin branch-name --force
```

---

## 🔹 3. Change a commit message by hash (without rebase)

If you know the commit **hash**:

```bash
git rebase -i <commit-hash>^
```

(use `^` to include the commit before it).
Then mark that commit as `reword`.

---

⚠️ **Important:** If the commit has been pushed and shared with others, rewriting history can cause conflicts for collaborators. In that case, it’s better to create a new commit that corrects things instead of rewriting history.

