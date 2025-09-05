Got it 👍
The video you shared is explaining **`git restore`** in simple terms. I’ll summarize everything in English clearly for you:

---

## 🔹 What is `git restore`?

`git restore` is used to **undo changes** in your working directory or staging area.
It helps you:

* Discard unwanted changes
* Unstage files from staging area
* Restore files from specific commits

---

## 🔹 Common Use Cases

### 1. Discard changes in a file

```bash
git restore <file>
```

👉 Removes changes from working directory (file goes back to last commit).

---

### 2. Unstage a staged file

If a file is already staged (`git add` was used), you need:

```bash
git restore --staged <file>
```

👉 Moves file out of staging area, but keeps your changes in working directory.

---

### 3. Discard everything (restore repo to last commit)

```bash
git restore --staged . --worktree .
```

or simply:

```bash
git restore .
```

👉 Cleans all changes (both staged & unstaged) and resets to `HEAD`.

---

### 4. Restore from a specific commit

```bash
git restore --source=<commit_id> <file>
```

👉 Replaces the file content with the version from that commit (but doesn’t change branch).

Example:

```bash
git restore --source=abc123 movies.txt
```

---

### 5. Restore all files to a commit

```bash
git restore --source=<commit_id> .
```

---

### 6. Restore and keep history (make a commit for restore)

If you want to record the restore in history:

1. Run `git restore ...`
2. Then commit:

   ```bash
   git commit -m "Restored files to previous state"
   ```

---

## 🔹 Key Flags

* `--staged` → Unstage files
* `--worktree` → Discard changes in working directory
* `--source=<commit>` → Restore from a specific commit (default = `HEAD`)
* `.` (dot) → Apply to all files

---

## 🔹 Difference from `git checkout`

* Before Git 2.23, people used `git checkout` for this.
* Now `git restore` is clearer:

  * `git checkout` → for **switching branches**
  * `git restore` → for **undoing file changes**

---

✅ In short:

* **Made mistake before commit?** → `git restore` is your best friend.
* **Staged wrong file?** → `git restore --staged file.txt`
* **Want old version from commit?** → `git restore --source=commit_id file.txt`

---

Do you want me to also compare **`git restore` vs `git reset`** with examples? That’s a common confusion.
