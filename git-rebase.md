

# 🔄 Git Rebase – Complete Guide

## 🔹 What is Git Rebase?

`git rebase` moves or combines a sequence of commits onto a new base commit.
It’s often used to keep a **clean, linear project history** by avoiding unnecessary merge commits.

👉 Benefits:

* Clean, readable commit history.
* Reapply changes on top of the latest base branch.
* Combine multiple commits into one.
* Edit, reorder, or fix commits before sharing.

---

## 🔹 When to Use Rebase

* Keep your feature branch up to date with `main`/`master`.
* Clean up your commits before opening a pull request.
* Squash related commits together (e.g., fix + feature).
* Reorder commits for logical history.

⚠️ **Avoid rebasing commits already pushed to a shared branch** — it rewrites history and may cause conflicts for others.

---

## 🔹 Basic Rebase

Move your feature branch on top of the latest `main`:

```bash
git checkout feature-branch
git rebase main
```

This reapplies your branch’s commits **on top of** `main`, as if you had started from the latest main branch.

---

## 🔹 Interactive Rebase (`-i`)

Use interactive rebase to **edit, reorder, squash, or reword commits**.

Example: rebase the last 3 commits

```bash
git rebase -i HEAD~3
```

This opens an editor with a list like:

```
pick a1b2c3 Add feature
pick d4e5f6 Fix bug
pick g7h8i9 Update docs
```

You can change actions:

* `pick` → keep commit as-is.
* `squash` → combine with previous commit.
* `edit` → stop and let you amend the commit.
* `reword` → change only the commit message.
* `drop` → remove commit.

After saving, Git applies your edits and continues.

---

## 🔹 Rebase Workflow: Continue, Abort, Skip

During rebase, conflicts may occur. Use these commands:

* **Continue after resolving conflicts:**

  ```bash
  git add fixed_file.txt
  git rebase --continue
  ```

* **Abort rebase (go back to original state):**

  ```bash
  git rebase --abort
  ```

* **Skip a problematic commit:**

  ```bash
  git rebase --skip
  ```

---

## 🔹 Review After Rebase

After rebasing:

* Run `git log --oneline` to verify commit order/history.
* Run tests/build to confirm everything still works.

---

## 🔹 Best Practices

✅ Use `git pull --rebase` to keep feature branches updated without merge commits.
✅ Use interactive rebase (`-i`) before pushing your branch for review.
✅ Squash minor “fix typo” or “WIP” commits into meaningful commits.
❌ Don’t rebase **shared commits** (already pushed to remote master/main).
✅ Always double-check history with `git log --oneline`.

---

## 🔹 Troubleshooting

* **Conflicts during rebase** → resolve, then `git rebase --continue`.
* **Commit can’t be fixed** → `git rebase --skip`.
* **Want to cancel** → `git rebase --abort`.

---

## 🔹 Quick Mental Model

Without rebase:

```
main:    A---B---C
feature:      \---D---E
```

With rebase (`git rebase main`):

```
main:    A---B---C
feature:              D'---E'
```

(feature commits reapplied onto latest main)

