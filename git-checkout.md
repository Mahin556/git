# 📝 Git Checkout – Complete Guide

## 🔹 What is `git checkout`?

`git checkout` is used to:

1. **Switch branches** (move `HEAD` to another branch).
2. **Restore files** in the working directory to a specific commit state.
3. **Create new branches** (with `-b`).
4. **Enter detached HEAD mode** (point `HEAD` directly to a commit, not a branch).

⚠️ Since Git **2.23 (2019)**, these tasks were split into **clearer commands**:

* `git switch` → branch operations
* `git restore` → file restore operations
  But `git checkout` still works and is widely used.

---

## 🔹 Usage Summary

### 1. Switch to an Existing Branch

```bash
git checkout branch-name
```

Moves `HEAD` to the given branch and updates your working directory.

---

### 2. Create and Switch to a New Branch

```bash
git checkout -b new-branch
```

Equivalent to:

```bash
git branch new-branch
git checkout new-branch
```

---

### 3. Restore a File to Last Commit

```bash
git checkout -- file.txt
```

Replaces your working copy of `file.txt` with the version from the last commit.
⚠️ This discards local changes to that file!
```
git checkout file.txt
```
Discard changes in files that are in working tree but do not descard the staged files.

---

### 4. Restore a File to a Specific Commit

```bash
git checkout <commit-hash> -- file.txt
```

Replaces the file with its state at that commit, without changing the branch.

---

### 5. Checkout a Commit (Detached HEAD)

```bash
git checkout <commit-hash>
```

HEAD points to a commit, **not a branch** → detached HEAD mode.

* You can explore history, build, or test.
* If you make commits, they won’t belong to any branch unless you create one:

```bash
git checkout -b new-branch
```

---

### 6. Checkout a Remote Branch

```bash
git checkout -t origin/feature
```

or shorter:

```bash
git checkout feature
```

(if Git can guess the remote branch).

---

### 7. Go Back to Previous Branch

```bash
git checkout -
```

Switches back to the branch you were on last (like `cd -` in Linux).

---

## 🔹 Key Options

| Option                 | Purpose                                |
| ---------------------- | -------------------------------------- |
| `-b <branch>`          | Create and switch to a new branch      |
| `-B <branch>`          | Create and switch, overwrite if exists |
| `-- file.txt`          | Restore file from commit or branch     |
| `<commit> -- file.txt` | Restore file from specific commit      |
| `<commit>`             | Checkout commit (detached HEAD)        |
| `-t <remote/branch>`   | Create and track a remote branch       |
| `-f`                   | Force checkout (discard local changes) |

---

## 🔹 Examples

### Switch Branch

```bash
git checkout main
```

### Create New Branch

```bash
git checkout -b hotfix
```

### Restore File

```bash
git checkout -- config.json
```

### Checkout Old Commit

```bash
git checkout a1b2c3d
```

### Create Branch from Old Commit

```bash
git checkout -b experiment a1b2c3d
```

---

## 🔹 Detached HEAD Explained

When you do:

```bash
git checkout <commit-hash>
```

You’re not on a branch anymore → `HEAD` is **detached**.

* You can make commits, but they’ll be “dangling” until you attach them to a branch:

```bash
git checkout -b new-branch
```

---

## 🔹 Git Checkout vs Git Switch & Git Restore

| Task            | Old Way (`git checkout`)   | New Way                      |
| --------------- | -------------------------- | ---------------------------- |
| Switch branch   | `git checkout main`        | `git switch main`            |
| Create branch   | `git checkout -b dev`      | `git switch -c dev`          |
| Restore file    | `git checkout -- file.txt` | `git restore file.txt`       |
| Checkout commit | `git checkout abc123`      | `git switch --detach abc123` |

✅ Use `git switch` and `git restore` if your Git is new enough.
✅ Use `git checkout` for compatibility with older versions.

---

## 🔹 Best Practices

* Prefer `git switch` and `git restore` for clarity (Git 2.23+).
* Be cautious with `git checkout -- file.txt` → it **destroys local changes**.
* If you’re in detached HEAD mode and want to keep your commits → create a branch.

---

⚡ In short:

* **Branches?** → `git checkout branch` or better `git switch`.
* **Files?** → `git checkout -- file` or better `git restore`.
* **Commits?** → `git checkout <commit>` (detached HEAD).

