
# Git Reset

**Change Platform:**
Shift focus to **GitHub** | **Bitbucket** | **GitLab**

---

## 🔹 What Does Git Reset Do?

The `git reset` command **moves your branch’s HEAD** to a different commit.
It can:

* Undo commits
* Unstage files
* Discard changes

⚠️ Unlike `git revert`, `git reset` can **rewrite history**, so use with care — especially in shared repositories.

---

## 🔹 Summary of Git Reset Commands and Options

| Command                      | Effect                                             |
| ---------------------------- | -------------------------------------------------- |
| `git reset --soft <commit>`  | Move HEAD to commit, keep changes **staged**       |
| `git reset --mixed <commit>` | Move HEAD to commit, **unstage** changes (default) |
| `git reset --hard <commit>`  | Move HEAD to commit, **discard all changes**       |
| `git reset <file>`           | Unstage a file                                     |
| `git log --oneline`          | Show commit history                                |

---

## 🔹 How to Find the Commit to Reset To

1. Run:

   ```bash
   git log --oneline
   ```

   Example:

   ```
   e56ba1f (HEAD -> master) Revert "Just a regular update..."
   52418f7 Just a regular update
   9a9add8 (origin/master) Added .gitignore
   81912ba Corrected spelling error
   ```
2. Copy the **first 7 characters** of the commit hash (e.g., `9a9add8`).

---

## 🔹 Git Reset Examples

### 1. `--soft` Reset

Moves HEAD, keeps all changes staged.

```bash
git reset --soft 9a9add8
```

✅ Use when you want to **squash commits** or rewrite history while keeping your work staged.

---

### 2. `--mixed` Reset (Default)

Moves HEAD, unstages changes, but keeps them in your files.

```bash
git reset --mixed 9a9add8
```

✅ Use when you want to “undo” commits but keep your code changes.

---

### 3. `--hard` Reset

Moves HEAD, deletes **all staged + working directory changes**.

```bash
git reset --hard 9a9add8
```

To forcefully push the reset HEAD to remote repo.
```
git push -f
```


⚠️ DANGEROUS — use only if you are sure you want to throw away changes.

---

## 🔹 Review Changes

After reset:

```bash
git status
git log --oneline
```

---

## 🔹 Tips & Best Practices

* Prefer `git revert` in shared repositories — it keeps history intact.
* Use `git reset` only for local history cleanup before pushing.
* Always check `git status` before committing again.
* For safety, create a backup branch:

  ```bash
  git branch backup-before-reset
  ```

---

## 🔹 Troubleshooting

* **If changes look wrong** → check with `git status`.
* **If you lost important work with `--hard`** → try `git reflog` to recover commits.
* **If remote already has your commits** → don’t use reset; use `revert` instead.



## 🔹 `git reset --soft HEAD~1`

* **Meaning:** Move `HEAD` and the current branch pointer **back by 1 commit**, but **keep everything staged**.
* ✅ Changes from that commit will appear in the **staging area (index)**, ready to recommit.
* ❌ No changes lost.

**Example:**

```bash
git reset --soft HEAD~1
```

* If your last commit was a mistake but you want to rewrite it, this puts all those changes back into staging.
* Then you can fix files and `git commit` again.

---

## 🔹 `git reset --hard <commit_hash>`

* **Meaning:** Move `HEAD` and branch pointer to the given commit, and **throw away all changes** (both staged + unstaged) after that commit.
* ✅ Cleans working directory & staging area to match exactly that commit.
* ⚠️ Destructive — your changes are lost (unless you can recover via `git reflog`).

**Example:**

```bash
git reset --hard a1b2c3d
```

* Your working tree now looks exactly like commit `a1b2c3d`.
* Everything after that commit disappears from history (unless in another branch or reflog).

---

## 📌 Summary:

| Command                     | Moves HEAD | Staging area                    | Working directory    |
| --------------------------- | ---------- | ------------------------------- | -------------------- |
| `git reset --soft HEAD~1`   | Yes        | Keeps changes staged            | Keeps changes        |
| `git reset --hard <commit>` | Yes        | Clears staging (matches commit) | Discards all changes |

---

👉 A quick trick to remember:

* **soft = safe** (keeps changes staged)
* **hard = harsh** (wipes everything to match commit)


Perfect 👍 You shared a detailed lecture transcript about **`git reset`**.
Let me now rewrite everything in **clear, structured English** (with examples), so you can fully understand how `git reset` works, especially compared to `git restore`.

---

# 🔹 Git Reset – Complete Guide

## 1. What is `git reset`?

* `git reset` moves the **HEAD** (your branch pointer) to another commit.
* Depending on the option (`--soft`, `--mixed`, `--hard`), it also affects the **staging area** and **working directory**.
* Use it when you want to:

  * Unstage files
  * Undo commits
  * Completely discard changes

---

## 2. Difference from `git restore`

* `git restore` → only affects **files** (working directory or staging area). It doesn’t move HEAD.
* `git reset` → moves the **HEAD pointer** to another commit and changes staging/working states.

---

## 3. Use Cases of `git reset`

### (A) Unstage files

If you added files to the staging area (`git add file.txt`) but want to unstage:

```bash
git reset file.txt
```

👉 Moves file back to working directory (unstaged).
👉 Content is unchanged, only staging is reset.

This is similar to:

```bash
git restore --staged file.txt
```

---

### (B) Undo the last commit (but keep changes)

```bash
git reset --soft HEAD~1
```

* Removes the last commit from history
* Keeps changes **staged** (ready to recommit)

📌 Example:

* Commit `C1 -> C2 -> C3`
* Run `git reset --soft HEAD~1`
* Now history is `C1 -> C2`
* Changes from `C3` are still in staging area

---

### (C) Undo last commit and unstage changes

```bash
git reset --mixed HEAD~1
```

(default if no option is given)

* Removes last commit
* Keeps changes in working directory
* Changes are **not staged**

📌 Example:

* Commit `C1 -> C2 -> C3`
* Run `git reset --mixed HEAD~1`
* History: `C1 -> C2`
* Changes from `C3` are now unstaged

---

### (D) Undo last commit and discard changes

```bash
git reset --hard HEAD~1
```

* Removes commit(s)
* Discards all related changes (both staging + working dir)
* ⚠️ Data is lost unless you recover via `git reflog`.

📌 Example:

* Commit `C1 -> C2 -> C3`
* Run `git reset --hard HEAD~1`
* History: `C1 -> C2`
* Changes from `C3` are completely gone

---

## 4. Reset to a specific commit

Instead of `HEAD~1`, you can give a commit hash:

```bash
# Soft reset (keep changes staged)
git reset --soft <commit-hash>

# Mixed reset (keep changes unstaged)
git reset --mixed <commit-hash>

# Hard reset (discard changes completely)
git reset --hard <commit-hash>
```

Example:

```bash
git reset --hard abc123
```

👉 Moves HEAD to commit `abc123` and discards everything after.

---

## 5. Summary of Options

| Command                  | Effect on Commit History    | Staging Area          | Working Directory                  |
| ------------------------ | --------------------------- | --------------------- | ---------------------------------- |
| `git reset --soft <id>`  | HEAD moves, commits removed | Changes remain staged | Unchanged (staged ready to commit) |
| `git reset --mixed <id>` | HEAD moves, commits removed | Changes unstaged      | Changes kept in working directory  |
| `git reset --hard <id>`  | HEAD moves, commits removed | Cleared               | Changes discarded completely       |

---

## 6. Golden Rules

* Use **soft** when you want to redo a commit but keep changes staged.
* Use **mixed** (default) when you want to unstage changes but keep them.
* Use **hard** only when you’re 100% sure — it **deletes changes**.
* If you delete commits by mistake → use `git reflog` to recover.

---

✅ In short:

* `restore` → reset files
* `reset` → reset commits (HEAD + staging + files depending on mode)

---

Would you like me to also draw a **diagram (visual timeline)** showing how HEAD, staging area, and working directory change for `soft`, `mixed`, and `hard` reset? That can make it super clear.
