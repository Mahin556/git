
# 🚀 Git Workflow – Complete Guide

## 🔹 The Three Areas of Git

1. **Working Directory** → Where you make and edit changes.
2. **Staging Area (Index)** → Where you prepare changes before committing.
3. **Repository (Local Repo)** → Where committed history is stored.

👉 Think of it like:
`[Working Directory] --git add--> [Staging Area] --git commit--> [Repository]`

---

## 🔹 Core Workflow Commands Overview

| Stage                   | Command                       | Purpose                                                       |
| ----------------------- | ----------------------------- | ------------------------------------------------------------- |
| **Check Status**        | `git status`                  | See which files are staged, unstaged, or untracked            |
| **Stage Changes**       | `git add <file>`              | Stage specific file                                           |
|                         | `git add .`                   | Stage all changes (new, modified, deleted)                    |
| **Commit Changes**      | `git commit -m "message"`     | Save staged changes to repository                             |
|                         | `git commit -a -m "message"`  | Stage & commit tracked files in one step (excludes new files) |
| **Push Changes**        | `git push`                    | Upload commits to remote (GitHub, GitLab, Bitbucket, etc.)    |
| **Undo / Fix Mistakes** | `git restore <file>`          | Undo changes in working directory                             |
|                         | `git restore --staged <file>` | Unstage a file                                                |
|                         | `git reset HEAD~`             | Undo last commit but keep changes in working directory        |
|                         | `git commit --amend`          | Change last commit message or add files to it                 |

---

## 🔹 Detailed Workflow

### 1. Working Directory

Where you **edit, create, or delete files**.
Git won’t track these changes until you stage them.

---

### 2. Staging Changes (`git add`)

Move changes into the **Staging Area**:

```bash
git add index.html      # Stage one file
git add .               # Stage all changes
```

---

### 3. Committing Changes (`git commit`)

Save staged changes into the **repository**:

```bash
git commit -m "Added new section to index.html"
```

Commit all modified & deleted files in one step:

```bash
git commit -a -m "Quick commit"
```

---

### 4. Pushing Changes (`git push`)

Send commits to the **remote repository**:

```bash
git push origin main
```

(Default branch may be `main` or `master`.)

---

### 5. Checking Status (`git status`)

View current state:

```bash
git status
```

* Shows staged, unstaged, and untracked files.

---

## 🔹 Undoing and Amending Changes

| Command                       | Use Case                                                 |
| ----------------------------- | -------------------------------------------------------- |
| `git restore <file>`          | Undo working directory changes before staging            |
| `git restore --staged <file>` | Unstage a file (keep changes in working directory)       |
| `git reset HEAD~`             | Undo the last commit (changes stay in working directory) |
| `git commit --amend`          | Edit the last commit message or add missing files        |

### Example – Unstage a file:

```bash
git restore --staged index.html
```

### Example – Fix last commit message:

```bash
git commit --amend -m "Corrected commit message"
```

---

## 🔹 Best Practices for Git Workflow

✅ Commit frequently with **clear, meaningful messages**.
✅ Use `git status` often to avoid surprises.
✅ Stage only what you want (`git add <file>` for precision).
✅ Use `git diff` to review changes before committing.
✅ Push regularly to **share your work and back it up**.

---

## 🔹 Workflows in Different Platforms

* **GitHub Flow** → Simple branching + pull requests (popular for teams).
* **GitLab Flow** → Adds environment-based deployment flows.
* **Bitbucket Flow** → Similar to GitHub but with additional CI/CD features.

