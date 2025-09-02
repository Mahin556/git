
## 🔹 What is Git Amend?

* `git commit --amend` lets you **modify your most recent commit**.
* You can:

  * Fix typos in the commit message
  * Add forgotten files
  * Remove files from the last commit

---

## 🔹 When to Use It

* You just committed but forgot something.
* You made a small mistake (typo, wrong file).
* You want to clean up the last commit **before pushing**.

⚠️ Avoid amending after pushing to a shared remote (it rewrites history).

---

## 🔹 Fix Last Commit Message

```bash
git commit --amend -m "New commit message"
```

✅ Updates only the commit message.

---

## 🔹 Add Files to the Last Commit

```bash
git add forgotten.txt
git commit --amend
```

✅ Adds the file(s) into the previous commit.

---

## 🔹 Remove Files from the Last Commit

```bash
git reset HEAD^ -- unwanted.txt
git commit --amend
```

✅ Removes the file from staging and rewrites the last commit.

---

## 🔹 Example Workflow

```bash
git log --oneline
07c5bc5 (HEAD -> master) Adding plines to reddme
```

Oops, typo! Let’s fix it:

```bash
git commit --amend -m "Added lines to README.md"
```

Now:

```bash
git log --oneline
eaa69ce (HEAD -> master) Added lines to README.md
```

👉 The old commit is replaced by the amended one.

---

## 🔹 Best Practices & Warnings

* Safe to use **before pushing**.
* Dangerous if used **after pushing**, since it rewrites commit history others may depend on.
* Use `git log` or `git status` to confirm your changes before pushing.

