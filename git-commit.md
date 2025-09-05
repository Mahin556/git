

# 🔹 What is a Commit?

A **commit** in Git is like a **save point** in your project.

* It records a **snapshot of your files** at a specific point in time.
* Each commit includes a **message** that describes what changed.
* You can always **go back to a previous commit** if needed.

👉 Think of commits as the **checkpoints** in your project’s history.

---

## 🔹 Common Commit Commands

| Command                                 | Description                               |
| --------------------------------------- | ----------------------------------------- |
| `git commit -m "message"`               | Commit staged changes with a message      |
| `git commit -a -m "message"`            | Commit all tracked changes (skip staging) |
| `git log`                               | View commit history                       |
| `git commit --amend -m "message"`       | Edit the most recent commit message       |
| `git commit --allow-empty -m "message"` | Create an empty commit                    |
| `git commit --no-edit`                  | Use the previous commit message           |

---

## 🔹 Commit with a Message (`-m`)

Save staged changes:

```bash
git commit -m "First release of Hello World!"
```

Example output:

```
[master (root-commit) 221ec6e] First release of Hello World!
 3 files changed, 26 insertions(+)
 create mode 100644 README.md
 create mode 100644 bluestyle.css
 create mode 100644 index.html
```

✅ Always write a **clear, meaningful message** so others (and future you) understand what changed.

---

## 🔹 Commit All Changes Without Staging (`-a`)

You can skip `git add` for **modified and deleted files**:

```bash
git commit -a -m "Quick update to README"
```

⚠️ Notes:

* This only works for **tracked files** (already added before).
* **New/untracked files** still require `git add <file>` first.

Example of failure:

```bash
git commit -a -m "Try to commit new file"
```

Output:

```
Untracked files:
    index.html

nothing added to commit but untracked files present
```

---

## 🔹 Multi-line Commit Messages

If you just run:

```bash
git commit
```

Your editor opens.

Format:

```
Short summary (≤ 50 characters)

More detailed explanation if needed.
```

---

## 🔹 Commit Message Best Practices

* Keep the first line short (**≤ 50 characters**)
* Use the **imperative mood** (e.g., *“Fix bug”* not *“Fixed bug”*)
* Leave a blank line after the summary
* Explain **why** the change was made, not just **what** changed

---

## 🔹 Other Useful Commit Options

* Create an empty commit:

  ```bash
  git commit --allow-empty -m "Start project"
  ```
* Reuse previous message (no edit):

  ```bash
  git commit --no-edit
  ```
* Add changes to last commit (keep message):

  ```bash
  git commit --amend --no-edit
  ```

---

## 🔹 Troubleshooting Commit Mistakes

* **Forgot to stage a file?**

  ```bash
  git add <file>
  git commit --amend
  ```
* **Typo in commit message?**

  ```bash
  git commit --amend -m "Corrected message"
  ```
* **Committed wrong files?**

  ```bash
  git reset --soft HEAD~1
  ```

  (Undo last commit, keep changes staged)

---

## 🔹 Viewing Commit History

### Full history:

```bash
git log
```

Example:

```
commit 09f4acd3f8836b7f6fc44ad9e012f82faf861803 (HEAD -> master)
Author: John Doe
Date:   Fri Mar 26 09:35:54 2021 +0100

    Updated index.html with a new line
```

### Short history:

```bash
git log --oneline
```

```
09f4acd Updated index.html with a new line
221ec6e First release of Hello World!
```

### Show files changed per commit:

```bash
git log --stat
```

### Other
```
git commit -m "message" - Commit staged changes with a message
git commit -a -m "message" - Commit all tracked changes (skip staging) but not work with new/untracked file only work with modified/deleted file
git log #See commit history
git log --oneline #shorter view
git log --stat #see which files changed in each commit
git commit #add commit in message file or add multi-line commit
git commit --amend #to add files to your last commit.
git commit --amend --no-edit #Quickly add staged changes to last commit, keep message
git commit -a  ---> add + commit
git commit --allow-empty -m "Start project" #Create an empty commit
git commit --no-edit #Use previous commit message (no editor)
git commit --amend -m "Corrected message" #to fix typo in last commit message
```
---

⚡ **Pro Tip:** Think of commits like **game save points** 🎮 — you can checkpoint your work, revisit earlier states, and always know what changed.

