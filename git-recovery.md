

# 🛠️ Git Recovery – Complete Guide

## 🔹 What is Git Recovery?

Git recovery is the process of **getting back lost commits, branches, or files**.

Even after mistakes like `git reset --hard` or deleting a branch, Git often keeps a hidden record (via **reflog** and object database).

👉 This means you can **undo mistakes and recover lost work** in most cases.

---

## 🔹 When to Use Git Recovery

Use Git recovery when you:

* ❌ Accidentally deleted a branch or file
* ❌ Ran `git reset --hard` and lost commits
* ❌ Overwrote changes you still need
* ❌ Want to undo a bad commit or restore an old version

---

## 🔹 Recover Lost Commits with `git reflog`

Reflog tracks movements of **HEAD**. You can use it to locate and recover commits.

```bash
git reflog
```

Example:

```
e56ba1f (HEAD -> master) HEAD@{0}: commit: Revert "Fix bug"
52418f7 HEAD@{1}: commit: Add footer section
9a9add8 (origin/master) HEAD@{2}: commit: Added .gitignore
81912ba HEAD@{3}: commit: Corrected spelling error
```

👉 Copy the commit hash you want to recover.

---

## 🔹 Restore a Deleted Branch

If you deleted a branch but its commits still exist in reflog:

```bash
git checkout -b branch-name <commit-hash>
```

✅ This recreates the branch at the commit you specify.

---

## 🔹 Recover a Deleted or Changed File

If you accidentally removed or modified a file:

```bash
git restore filename.txt
```

* Restores the file from the **last committed state**.
* To restore from a specific commit:

```bash
git restore --source=<commit-hash> filename.txt
```

---

## 🔹 Recover from a Hard Reset

If you reset and lost commits:

1. View reflog:

   ```bash
   git reflog
   ```
2. Find the commit before the reset (e.g., `HEAD@{2}`).
3. Restore:

   ```bash
   git reset --hard HEAD@{2}
   ```

✅ Branch returns to the state it was at that point.

---

## 🔹 Tips & Best Practices

* ✅ **Commit regularly** so recovery is easier.
* ✅ Use `git reflog` first when you think something is “lost.”
* ✅ Use `git restore` to bring back deleted/modified files.
* ✅ Don’t panic — most “lost” work can be recovered until Git runs garbage collection.

---

## ⚠️ Warnings

* **Reflog is local only** → you can’t recover remote history from your local reflog.
* Once reflog entries expire (default 90 days for commits, 30 days for unreachable commits) and `git gc` runs, commits may be permanently lost.

---

👉 Git recovery is basically about **finding the commit (via reflog/log)** and **resetting or checking out from it**.
