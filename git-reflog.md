
# 📜 Git Reflog – Complete Guide

## 🔹 What is Git Reflog?

`git reflog` records updates to the **tip of branches and HEAD**.
It’s like an internal log of where Git pointers have been — including commits, resets, checkouts, merges, rebases, and more.

👉 Think of it as your **safety net**:

* Lets you recover commits you thought were “lost.”
* Helps undo mistakes like `git reset --hard`.
* Shows the true movement of HEAD, beyond what `git log` displays.

---

## 🔹 When to Use Git Reflog

* **Recover lost commits** (after reset, rebase, or accidental deletion).
* **Undo a reset or merge** by jumping back to a previous HEAD state.
* **See the history of branch movements** even when commits are no longer in `git log`.

---

## 🔹 Show the Reflog

List where HEAD has been:

```bash
git reflog
```

Example:

```
e56ba1f (HEAD -> master) HEAD@{0}: commit: Revert "Fix typo"
52418f7 HEAD@{1}: commit: Add footer section
9a9add8 (origin/master) HEAD@{2}: commit: Added .gitignore
81912ba HEAD@{3}: commit: Corrected spelling error
3fdaa5b HEAD@{4}: merge: Merge pull request #1
```

* `HEAD@{0}` = current position
* Higher numbers = older history

---

## 🔹 Recover Lost Commits

### Example: Undo a Hard Reset

Suppose you reset too far back:

```bash
git reset --hard HEAD~2
```

Use `git reflog` to find the commit:

```bash
git reflog
52418f7 HEAD@{1}: commit: Add footer section
```

Restore it:

```bash
git reset --hard HEAD@{1}
```

✅ Branch is back to the commit you wanted.

---

## 🔹 Clean Up the Reflog

Reflog entries are cleaned automatically, but you can expire or prune them:

```bash
# Expire entries older than 30 days
git reflog expire --expire=30.days refs/heads/main

# Run garbage collection to prune unreachable commits
git gc --prune=now
```

---

## 🔹 Tips & Best Practices

✅ Use `git reflog` whenever you think you “lost” work.
✅ Remember reflog entries are **local only** (not shared with remotes).
✅ Clean up occasionally if space is a concern (`git reflog expire`).

---

## 🔹 Troubleshooting

* **Reflog shows nothing?** → Check you’re in the right repo; also note remotes don’t store reflog.
* **Accidentally reset hard?** → Use `git reflog` to jump back to the right HEAD.
* **Lost stashes?** → They also appear in reflog (look for `stash@{}`).

---

## ⚠️ Warnings

* Reflog can overwrite states if used carelessly (e.g., hard resets).
* Expired reflog entries + garbage collection (`git gc`) = truly unrecoverable commits.

---

## 🔹 Quick Mental Model

* `git log` = project history (visible commits in current branch).
* `git reflog` = “local diary” of every move HEAD made (including resets, checkouts, rebases, stashes).

💡 If `git log` is like the **story**, then `git reflog` is the **behind-the-scenes journal**.

