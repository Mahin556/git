

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

Here’s a **well-organized and clear English explanation** of the transcript, summarizing the concept, demonstration, and best practices for Git merge vs. rebase:

---

### 1. Introduction

* **Git rebase** is often considered confusing, but it’s a powerful tool for keeping your branch history **clean and linear**.
* The video explains:

  * The difference between **Git merge** and **Git rebase**.
  * When to use each.

---

### 2. The Problem with Merge

* Scenario:

  * You have a **master branch**.
  * You create a **feature branch** from master.
  * Meanwhile, someone else makes commits on master.
* **Solution most people use:** `git merge master` in the feature branch.
* **Issue with merge:**

  * Each merge creates a **new merge commit** if fast-forward is not possible.
  * Over time, multiple merges create **useless commits** that clutter your history.

Example:

```
Master: A --- B --- C
Feature:    D --- E
After merge:
Feature:    D --- E --- M (merge commit)
```

* Here, `M` is just a merge commit with no new changes, making the history messy.

---

### 3. How Rebase Solves the Problem

* **Git rebase** reapplies your feature branch commits **on top of master** instead of merging master into your branch.
* **Effect:**

  * Linear and clean history.
  * Master branch commits remain unchanged.
  * Feature branch commits get **new commit hashes**, but their changes remain the same.
* **Important caution:**

  * Do **not rebase branches shared with others**, because rebasing rewrites history, which can break your teammates’ work.

Example after rebase:

```
Master:  A --- B --- C
Feature:            D' --- E'
```

* Now, `D'` and `E'` are the same changes as `D` and `E`, but reapplied on top of master.

---

### 4. Demonstration (Step by Step)

1. **Setup:**

   * Create a new repository.
   * Add a `home` file, commit a header and footer on master.

2. **Feature branch:**

   * Create a feature branch.
   * Add changes to an `about` page (phone number, email, address).

3. **Simulate master changes:**

   * Make more commits on master (login form, photos).

4. **Merging master into feature branch:**

   * Creates multiple merge commits.
   * History becomes messy.

5. **Rebase feature onto master:**

   * Checkout feature branch.
   * Run `git rebase master`.
   * Resolve conflicts manually if any (`git status`, open files, choose changes, `git add`, `git rebase --continue`).
   * Result: clean, linear history with feature commits applied on top of master.

---

### 5. Key Points to Remember

* **Merge:**

  * Keeps history but may create many unnecessary merge commits.
  * Best for **shared branches** or when preserving the original branch structure.

* **Rebase:**

  * Linear, clean history.
  * Commits are reapplied on top of master.
  * **Do not use on shared branches**.
  * Useful for **local feature branches** before merging back to master.

* **Conflict handling during rebase:**

  1. Check status: `git status`.
  2. Open files with conflicts.
  3. Decide which changes to keep.
  4. `git add <file>` and `git rebase --continue`.

---

### 6. Visualization of History

**Before rebase (using merge repeatedly):**

```
Master:  A --- B --- C --- F --- G
Feature: D --- E --- M1 --- M2
```

* M1, M2 are merge commits.

**After rebase:**

```
Master:  A --- B --- C --- F --- G
Feature:                   D' --- E'
```

* Feature branch commits D and E are now **on top of master**.
* History is **linear and clean**, no unnecessary merge commits.

---

### 7. Summary

* **Rebase** = "move your branch on top of master", keeping history clean.
* **Merge** = "integrate master into your branch", may create merge commits.
* Use **rebase** for local branches, **merge** for shared branches.
* Always resolve conflicts carefully during rebase.

---

If you want, I can also **draw a simple visual diagram comparing merge vs rebase** with commit trees and conflicts, which makes it **super easy to understand at a glance**.

Do you want me to do that?

