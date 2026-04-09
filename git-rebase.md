

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

---

## Git Rebase – Complete Notes

### What is Git Rebase?

**Rebasing** is the process of changing the **parent commit** of a branch. Instead of a branch branching off from an old commit, rebasing makes it look like the branch was created from the **latest commit** of another branch (like `main`).

> In simple terms: Rebase **rewrites history** by changing the base (parent) of your branch.

---

### Visual Explanation (From the Demo)

**Initial Setup:**
- First commit: `hello.txt` with "Hello World"
- Created a `feature` branch from the first commit
- Made **3 commits** on the `feature` branch
- Switched to `main` branch and added **1 new commit** (different file)

**Before Rebase:**
```
main:     A (first) --- B (new file)
feature:  A (first) --- C --- D --- E (3 commits)
```
- `feature` branch is still pointing to commit `A` as its parent

**After Rebase (`git rebase main` while on `feature`):**
```
main:     A --- B
feature:  A --- B --- C' --- D' --- E'
```
- Now `feature` branch looks like it was created from commit `B` (latest main)
- The 3 commits are **rewritten** with new commit IDs

---

### Command Used

```bash
# First, switch to the branch you want to rebase
git switch feature

# Then rebase it onto the main branch
git rebase main
```

---

### Key Things to Understand

| Concept | Explanation |
|---------|-------------|
| **Parent pointer changes** | The branch's base commit changes to the latest commit of the target branch |
| **History is rewritten** | Commit IDs change (new SHA hashes are generated) |
| **Linear history** | Results in a cleaner, linear project history |
| **No merge commit created** | Unlike `git merge`, rebase doesn't create an extra commit |

---

### When to Use Rebase

#### ✅ Good Use Cases:
1. **Working alone** on a feature branch – rebase keeps history clean
2. **You need latest configuration/changes** from `main` into your feature branch
3. **Before pushing** a feature branch to keep history linear
4. **Updating your branch** without creating merge commits

#### ❌ When NOT to Use Rebase:
> **Avoid rebasing on shared/public branches** (branches that other developers are using)

- If a team is working together, rebase causes confusion
- Other developers won't understand where branches are coming from
- Rewriting shared history can cause serious problems for others

---

### Conflicts During Rebase

- Conflicts can **still happen** if you modify the **same file** in both branches
- The process is similar to merge conflicts but uses:
  ```bash
  git rebase --continue   # After resolving conflicts
  git rebase --abort      # To cancel the rebase
  git rebase --skip       # To skip a problematic commit
  ```

> The video mentions conflicts will be covered in the next video.

---

### Rebase vs Merge – Quick Comparison

| Feature | Rebase | Merge |
|---------|--------|-------|
| History | Linear, clean | Preserves actual branch structure |
| Merge commit | No | Yes |
| Commit IDs | Changed (rewritten) | Same as original |
| Best for | Private branches | Shared/public branches |
| Complexity | Higher (rewrites history) | Lower |

---

### Important Warnings

1. **Never rebase branches that others are working on** – It rewrites history and causes chaos for your team

2. **Commit IDs change** – After rebase, your commits get **new IDs**. Take screenshots or note old IDs to see the difference

3. **Looks like magic but isn't** – Git makes it appear that your branch started from the latest commit, but internally it's reapplying your changes

4. **Useful for configuration updates** – If another developer adds config changes to `main`, you can rebase to include them in your feature branch

---

### Summary

> **Git Rebase** changes the base (parent) of your branch to another branch's latest commit. It creates a **clean, linear history** but **rewrites commit IDs**. Use it when working **alone** or to **update your branch** with latest changes. **Avoid rebasing on shared branches** – that's when you should use `git merge` instead.