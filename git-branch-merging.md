
## **1. Branch Creation**

* **Create a new branch:**

```bash
git branch <branch-name>
```

Example:

```bash
git branch hello-world-images
```

* **Create and switch to a new branch (shortcut with `-b`):**

```bash
git checkout -b <branch-name>
```

Example:

```bash
git checkout -b emergency-fix
```

* **Rename a branch:**

```bash
git branch -m <old-name> <new-name>
```

Example:

```bash
git branch -m old-name new-name
```

---

## **2. Listing Branches**

* **List all branches in the repository:**

```bash
git branch
```

* Shows the current branch with a `*`:

```
  hello-world-images
* master
```

---

## **3. Switching Between Branches**

* **Switch to an existing branch:**

```bash
git checkout <branch-name>
```

Example:

```bash
git checkout hello-world-images
```

* **Alternative (modern Git) command:**

```bash
git switch <branch-name>
```

---

## **4. Working in a Branch**

* **Check the status of files in the branch:**

```bash
git status
```

* **Stage files for commit (all changes):**

```bash
git add --all
```

* **Stage specific files:**

```bash
git add <file-name>
```

Example:

```bash
git add index.html
```

* **Commit staged changes with a message:**

```bash
git commit -m "Your commit message"
```

Example:

```bash
git commit -m "Added image to Hello World"
```

---

## **5. Merging Branches**

* **Merge a branch(specified branch history-commits) into the current branch:**

```bash
git merge <branch-name>
```

Example:

```bash
git merge emergency-fix
```

---

## **6. Deleting Branches**

* **Delete a branch that is already merged:**

```bash
git branch -d <branch-name>
```

Example:

```bash
git branch -d hello-world-images
```

* **Force delete an unmerged branch:**

```bash
git branch -D <branch-name>
```

---

## **7. Other Useful Commands**

* **Check which branch you are currently on:**

```bash
git status
```

* **List all files in the current branch directory:**

```bash
ls
```

* **Check staged and unstaged changes:**

```bash
git status
```

---

### **Best Practices for Branching**

1. Use descriptive branch names: `feature/login-page` or `bugfix/header-crash`.
2. Keep each branch focused on a single purpose.
3. Regularly merge changes from `main` to stay updated.
4. Delete branches after merging to keep the repository clean.

Got it 👍
Here’s a **well-structured, polished guide on Git Branch Merging**, with **all commands clearly listed and explained** in the right order.

---

# 🚀 Git Branch Merging – Complete Guide

## 🔹 What is Merging in Git?

Merging in Git means **combining the changes from one branch into another**.
It’s how you bring different lines of development together after working separately on features or bug fixes.

---

## 🔹 Common Git Merge Options

| Command                       | Description                                             |
| ----------------------------- | ------------------------------------------------------- |
| `git merge <branch>`          | Merge a branch into your current branch                 |
| `git merge --no-ff <branch>`  | Always create a merge commit (preserves branch history) |
| `git merge --squash <branch>` | Squash all commits into one before merging              |
| `git merge --abort`           | Abort a merge in progress                               |

---

## 🔹 Steps for Merging Branches

1. **Switch to the branch you want to merge into** (usually `main` or `master`):

   ```bash
   git checkout master
   ```

2. **Merge another branch into it**:

   ```bash
   git merge emergency-fix
   ```

   If no conflicts exist and the branch is a direct continuation, Git performs a **fast-forward merge**.

---

## 🔹 Best Practices Before Merging

✅ Always **commit or stash** your changes before starting a merge.
✅ Regularly **merge from `main` into your feature branch** to reduce conflicts.
✅ Read and resolve conflicts carefully.
✅ Write **clear and descriptive merge commit messages**.

---

## 🔹 Practical Merge Examples

### 1. Abort a Merge

If something goes wrong:

```bash
git merge --abort
```

### 2. Check Merge Status

```bash
git status
```

### 3. Resolve a Conflict and Continue

```bash
# Edit conflicted files manually
git add <file>
git commit
```

### 4. Delete a Merged Branch

```bash
git branch -d emergency-fix
```

---

## 🔹 Types of Merges

### ✅ Fast-Forward Merge

Happens when the target branch has no new commits.

```bash
git merge feature-branch
```

### ✅ Non-Fast-Forward Merge (History Preserved)

Forces a merge commit:

```bash
git merge --no-ff feature-branch
```

### ✅ Squash Merge (Clean History)

Combines all commits into a single one:

```bash
git merge --squash feature-branch
git commit -m "Merged feature-branch as a single commit"
```
---

## 🔹 Merge Conflicts

A **merge conflict** happens when two branches edit the same part of a file differently.

Conflict markers look like this inside files:

```txt
<<<<<<< HEAD
<p>This line is from master</p>
=======
<p>This line is from feature branch</p>
>>>>>>> feature-branch
```

---

## 🔹 Resolving Merge Conflicts

1. **Open the conflicted file(s)**
2. Manually choose or combine changes
3. Remove conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`)
4. Stage and commit the resolution

### Example

```bash
git add index.html
git commit -m "Resolved merge conflict in index.html"
```

---

## 🔹 Full Example with Conflict

```bash
# Switch to master
git checkout master

# Merge feature branch
git merge hello-world-images
# ❌ Conflict occurs in index.html

# Check status
git status

# Open and edit index.html to fix conflicts
# Then stage changes
git add index.html

# Commit after resolving
git commit -m "Merged hello-world-images after resolving conflicts"

# Delete merged branch
git branch -d hello-world-images
```

---

## 🔹 Troubleshooting & Tips

* Cancel merge if needed → `git merge --abort`
* Always check conflicts with → `git status`
* Ask teammates if unsure about conflict resolution
* Keep commits small and meaningful for easier merges




