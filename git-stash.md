
# 🚀 Git Stash – Complete Guide

## 🔹 What is Git Stash?

`git stash` lets you **temporarily save your uncommitted changes** (staged + unstaged) and return to a clean working directory.

👉 Use it when you:

* Need to **switch branches quickly** without committing.
* Must **fix a bug** or do an urgent task.
* Want to **save work-in-progress** (WIP) safely without making messy commits.

---

## 🔹 Key Commands for Stashing

| Command                     | Purpose                                     |
| --------------------------- | ------------------------------------------- |
| `git stash`                 | Stash changes (tracked files only)          |
| `git stash -u`              | Stash changes **including untracked files** |
| `git stash push -m "msg"`   | Stash with a custom message                 |
| `git stash list`            | List all stashes                            |
| `git stash show`            | Show summary of latest stash                |
| `git stash show -p`         | Show full diff of latest stash              |
| `git stash apply`           | Apply latest stash (keeps it in the stack)  |
| `git stash apply stash@{n}` | Apply a specific stash                      |
| `git stash pop`             | Apply latest stash **and remove it**        |
| `git stash drop stash@{n}`  | Delete a specific stash                     |
| `git stash clear`           | Delete **all** stashes                      |
| `git stash branch <branch>` | Create new branch from a stash              |

---

## 🔹 Stash Basics

### 1. Stash Your Changes

```bash
git stash
```

✅ Saves **tracked** (staged + unstaged) files.
❌ Does **not** stash untracked files by default.

To include untracked files:

```bash
git stash -u
```

---

### 2. Stash with a Message

```bash
git stash push -m "WIP: homepage redesign"
```

---

### 3. List Your Stashes

```bash
git stash list
```

Example output:

```
stash@{0}: On main: WIP: homepage redesign
stash@{1}: WIP on main: Add new feature
```

---

### 4. Show What’s in a Stash

* Summary:

  ```bash
  git stash show
  ```
* Full diff:

  ```bash
  git stash show -p
  ```

---

## 🔹 Restoring Stashes

### 1. Apply the Latest Stash

```bash
git stash apply
```

✅ Keeps the stash in the stack.

---

### 2. Apply a Specific Stash

```bash
git stash apply stash@{1}
```

---

### 3. Pop the Stash (Apply + Remove)

```bash
git stash pop
```

---

### 4. Drop a Stash

```bash
git stash drop stash@{0}
```

---

### 5. Clear All Stashes

```bash
git stash clear
```

⚠️ Permanent! Cannot be undone.

---

### 6. Branch from a Stash

If your stashed work deserves its own branch:

```bash
git stash branch new-feature stash@{0}
```

---

## 🔹 Best Practices for Stashing

✅ Use **descriptive messages** (`git stash push -m "WIP: login form"`)
✅ Don’t rely on stashes as **long-term storage** → commit your work when possible
✅ Clean up old stashes with `git stash drop` or `git stash clear`
✅ Remember: stashes are **temporary helpers**, not replacements for commits

---

## 🔹 Troubleshooting

* Lost changes? → Run `git stash list` then `git stash apply stash@{n}`
* Conflicts on apply? → Resolve them like merge conflicts.
* Untracked files missing? → Use `git stash -u` next time.
* Cleared all stashes accidentally? → 😬 Sorry, `git stash clear` is permanent.

