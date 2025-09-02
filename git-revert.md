

# 🔄 Git Revert – Complete Guide

## 🔹 What is Git Revert?

`git revert` is used to **undo a commit safely** by creating a **new commit that reverses the changes** of a specific commit.

👉 Key difference:

* `git reset` changes history (dangerous in shared repos).
* `git revert` **preserves history** (safe for collaboration).

---

## 🔹 Common Git Revert Commands

| Command                     | Purpose                                   |
| --------------------------- | ----------------------------------------- |
| `git revert HEAD`           | Revert the latest commit                  |
| `git revert <commit_hash>`  | Revert a specific commit                  |
| `git revert HEAD~2`         | Revert a commit 2 steps back              |
| `git revert --no-edit HEAD` | Revert without editing commit message     |
| `git revert --continue`     | Continue revert after conflict resolution |
| `git revert --abort`        | Abort the revert if conflicts occur       |
| `git log --oneline`         | View commit history to find commit hash   |

---

## 🔹 Step 1 – Find the Commit to Revert

Use:

```bash
git log --oneline
```

Example output:

```
52418f7 (HEAD -> master) Just a regular update, definitely no accidents here...
9a9add8 Added .gitignore
81912ba Corrected spelling error
...
221ec6e First release of Hello World!
```

---

## 🔹 Step 2 – Run Git Revert

### Revert the latest commit

```bash
git revert HEAD --no-edit
```

Output:

```
[master e56ba1f] Revert "Just a regular update, definitely no accidents here..."
 1 file changed, 0 insertions(+), 0 deletions(-)
```

---

### Revert a specific commit

```bash
git revert 9a9add8
```

---

### Revert multiple commits

```bash
git revert HEAD~3..HEAD
```

👉 This reverts the last **3 commits**.

---

## 🔹 Step 3 – Review Changes

After revert, check history again:

```bash
git log --oneline
```

Example:

```
e56ba1f (HEAD -> master) Revert "Just a regular update..."
52418f7 Just a regular update, definitely no accidents here...
9a9add8 Added .gitignore
...
```

---

## 🔹 Handling Conflicts During Revert

If conflicts occur:

1. Resolve conflicts in files manually.
2. Mark resolved files:

   ```bash
   git add <file>
   ```
3. Continue revert:

   ```bash
   git revert --continue
   ```
4. Or abort if needed:

   ```bash
   git revert --abort
   ```

---

## 🔹 Tips & Best Practices

✅ Use `git revert` for **shared repositories** → safer than reset.
✅ Always check commit history with `git log --oneline`.
✅ Add `--no-edit` if you don’t want to open the commit message editor.
✅ Use `git revert --abort` if something goes wrong.
✅ For multiple commits, prefer `git revert <range>` instead of reverting one by one.

---

## 🔹 Quick Comparison – Revert vs Reset

| Command            | Effect                                   | Safe for Shared Repo? |
| ------------------ | ---------------------------------------- | --------------------- |
| `git reset --hard` | Removes commits permanently              | ❌ No                  |
| `git revert`       | Creates a new commit that undoes changes | ✅ Yes                 |


