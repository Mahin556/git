
# 🔹 Git Staging Environment

### What is the Staging Environment?

The **staging environment** (or **staging area**) is like a **waiting room for your changes**.
When you edit files in your repository, Git doesn’t immediately commit them. Instead, you **stage** the files you want to include in your next commit.

👉 This gives you control over what goes into your project history.

---

## 🔹 Common Staging Commands

| Command                         | Description                                      |
| ------------------------------- | ------------------------------------------------ |
| `git add <file>`                | Stage a specific file                            |
| `git add --all` OR `git add -A` | Stage all changes (new, modified, deleted files) |
| `git status`                    | Show which files are staged/unstaged             |
| `git restore --staged <file>`   | Unstage a file                                   |
| `git reset HEAD <file>`         | (Alternative) Unstage a file                     |

---

## 🔹 Stage a File

To add a file to the staging area:

```bash
git add index.html
```

Now `index.html` is staged.
Check the status:

```bash
git status
```

Example output:

```
On branch master

No commits yet

Changes to be committed:
  (use "git restore --staged ..." to unstage)
    new file: index.html
```

---

## 🔹 Stage Multiple Files

To stage **all changes at once**:

```bash
git add --all
```

or

```bash
git add -A
```

---

## 🔹 Check Staged Files

See what’s ready to be committed:

```bash
git status
```

Example:

```
On branch master

No commits yet

Changes to be committed:
  (use "git restore --staged ..." to unstage)
    new file:   README.md
    new file:   bluestyle.css
    new file:   index.html
```

---

## 🔹 Unstage a File

If you staged a file by mistake:

```bash
git restore --staged index.html
```

Now `index.html` is no longer staged.
(You can also use `git reset HEAD index.html`.)

---

* **`git add -A` (or `--all`)**

  * Stages **everything**: new files, modified files, and deleted files across the **entire working tree**.
  * Works no matter where you run it (top-level or subdirectory).
  * Since Git v2, this is the **default behavior** of `git add`.

---

* **`git add -u` (or `--update`)**

  * Stages **only modified and deleted files**.
  * Does **not** stage new/untracked files.
  * Work like -A or --all but only for update and deleted files.

---

* **`git add .`**

  * Stages new, modified, and deleted files — **but only from the current directory downward**.
  * If run at the repo root → behaves like `git add -A`.
  * If run inside a subdirectory → ignores changes outside that directory.

---

* **`git add *`**

  * Uses the **shell’s wildcard expansion**, not Git’s logic.
  * Adds visible files in the current directory (no hidden files like `.gitignore` or `.env`).
  * Does not handle deleted files correctly.
  * Can produce **unexpected results**, so it’s generally **not recommended**.


