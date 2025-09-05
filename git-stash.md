Got it ✅ — you want me to merge both versions (your first **clean reference** and the second **structured guide**) into **one complete, polished Git Stash guide**.
Here’s the combined result (concise, organized, and copy-ready for docs, README, or learning material):

---

# 🚀 Git Stash – Complete Guide

## 🔹 What is Git Stash?

`git stash` temporarily saves your **uncommitted changes** (staged + unstaged) so you can return to a clean working directory.
Think of it as putting your work-in-progress (WIP) onto a stack — you can restore it later.

**Why use it?**

* Switch branches quickly without committing WIP.
* Handle urgent bug fixes without losing work.
* Keep unfinished changes safe without making messy commits.

---

## 🔹 Key Commands (Cheat Sheet)

| Command                     | Purpose                                                     |
| --------------------------- | ----------------------------------------------------------- |
| `git stash`                 | Stash tracked changes (shorthand for `push`)                |
| `git stash -u`              | Stash including **untracked** files (`--include-untracked`) |
| `git stash -a`              | Stash including **untracked + ignored** files (`--all`)     |
| `git stash push -m "msg"`   | Stash with a custom message (recommended)                   |
| `git stash list`            | List all stashes                                            |
| `git stash show`            | Show summary of latest stash                                |
| `git stash show -p`         | Show full diff of latest stash                              |
| `git stash apply`           | Apply latest stash (keeps it in the stack)                  |
| `git stash apply stash@{n}` | Apply a specific stash                                      |
| `git stash pop`             | Apply latest stash **and remove** it                        |
| `git stash drop stash@{n}`  | Delete a specific stash                                     |
| `git stash clear`           | Delete **all** stashes (⚠️ irreversible)                    |
| `git stash branch <branch>` | Create new branch from a stash                              |
| `git stash --keep-index`    | Stash only unstaged changes, keep staged ones intact        |
| `git stash apply --index`   | Restore stash + staged/index state                          |

---

## 🔹 Stash Basics & Examples

### 1. Stash your changes

```bash
git stash
# Saves tracked files (staged + unstaged), not untracked by default
```

Include untracked files:

```bash
git stash -u
```

### 2. Stash with a message

```bash
git stash push -m "WIP: homepage redesign"
```

### 3. List stashes

```bash
git stash list
# stash@{0}: On main: WIP: homepage redesign
# stash@{1}: WIP on feature: Add widget
```

### 4. Show stash details

```bash
git stash show              # summary
git stash show -p stash@{1} # full diff
```

---

## 🔹 Restoring Stashes

* **Apply latest stash (keep in list):**

  ```bash
  git stash apply
  ```

* **Apply specific stash:**

  ```bash
  git stash apply stash@{1}
  ```

* **Pop (apply + remove):**

  ```bash
  git stash pop
  ```

* **Drop stash:**

  ```bash
  git stash drop stash@{0}
  ```

* **Clear all stashes (⚠️ permanent):**

  ```bash
  git stash clear
  ```

* **Branch from a stash:**

  ```bash
  git stash branch new-feature stash@{0}
  ```

---

## What gets stashed?

* By default: **tracked files** (both staged and unstaged) and index state.
* To include **untracked files**: `git stash -u` (or `--include-untracked`).
* To include **untracked + ignored**: `git stash -a` (or `--all`).

---

## Advanced / handy options

* `git stash --keep-index` — stash only the unstaged changes; keep index/staged files (useful for testing pre-commit state).
* `git stash apply --index` — attempt to restore the index state (staged files) when applying a stash.
* Prefer `git stash push -m "msg"` (modern explicit form) instead of older `git stash save`.

---

## Best practices

* Use descriptive messages: `git stash push -m "WIP: add login form validation"`.
* Don’t treat stashes as long-term storage — commit or branch your work when ready.
* Clean up old stashes regularly (`git stash list` → `git stash drop`).
* If stash grows complex, consider `git stash branch` to make it a proper branch.

---

## Troubleshooting

* **Stash didn’t apply cleanly** → conflicts: resolve them like a normal merge (edit files, `git add`, finish).
* **Untracked files missing after apply** → you didn’t stash untracked files; next time use `-u`.
* **Accidentally dropped/cleared stashes** → usually hard to recover. Check `git reflog` for clues, but treat `git stash clear` as irreversible.
* **Want to add a forgotten file to last commit** → `git add <file>` then `git commit --amend`.

---

## 🔹 Quick Mental Model

```
Working Directory → (git add) → Staging Area → (git commit) → Repository history
        |
        ↓
     git stash
```

`git stash` saves your working directory (+ optional index) onto a stack so you can return later without losing progress.

