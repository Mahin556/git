
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


