
# 🚀 Git Best Practices

## 🔹 1. Commit Often

* Make **small, frequent commits** to capture progress.
* Easier to track changes, debug issues, and roll back.

**Example**

```bash
git add .
git commit -m "Add user authentication logic"
```

---

## 🔹 2. Write Clear Commit Messages

* Explain **why** a change was made, not just what changed.
* Use the **imperative mood**: “Fix bug” instead of “Fixed bug”.
* Be specific and meaningful.

**Good Example**

```bash
git commit -m "Fix bug in user login validation"
```

✅ Clear messages help teammates and your future self understand history.

---

## 🔹 3. Use Branches

* Keep `main` (or `master`) stable.
* Create branches for **features, fixes, and experiments**.
* Use **clear names**: `feature/login-form`, `bugfix/user-auth`.

**Example**

```bash
git checkout -b feature/login-form
```

---

## 🔹 4. Pull Before You Push

* Always update your local branch before pushing.
* Prevents **conflicts and rejected pushes**.

**Example**

```bash
git pull origin main
git push origin main
```

---

## 🔹 5. Review Changes Before Committing

* Catch mistakes early by checking what you’re about to commit.

**Example**

```bash
git status     # See staged/unstaged changes
git diff       # See actual changes in files
```

---

## 🔹 6. Keep Repositories Small

* Don’t add large binaries, videos, or unnecessary dependencies.
* Use **Git LFS** (Large File Storage) for big files.

**Why?**

* Faster cloning, easier collaboration, fewer repo issues.

---

## 🔹 7. Use `.gitignore`

* Prevents unnecessary files (build artifacts, logs, secrets) from being tracked.

**Example `.gitignore`**

```gitignore
node_modules/
*.log
.env
```

👉 If a file is already tracked, remove it with:

```bash
git rm --cached <file>
```

---

## 🔹 8. Tag Releases

* Mark important versions (e.g., `v1.0`) for easy reference and rollback.

**Example**

```bash
git tag v1.0
git push origin v1.0
```

---

### 9. IGNORING PATTERNS

Prevent unintentional staging/committing of files.

```
git config --global core.excludesfile [file]   # Set global ignore file
```

📌 Usually, you also create a .gitignore file inside your repo to ignore project-specific files:

** Example .gitignore **
```
node_modules/
*.log
.env
```
---

# ✅ Summary of Good Git Habits

* 📌 Commit often, with clear messages.
* 🌱 Use branches for isolation.
* 🔄 Pull before you push.
* 👀 Review with `git status` & `git diff`.
* 🧹 Keep repos clean & small.
* 🚫 Ignore unwanted files with `.gitignore`.
* 🏷 Tag releases for milestones.

