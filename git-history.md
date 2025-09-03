
## **1. View Commit History**

* **Full commit history**

```bash
git log
```

* **Short summary of commits (one line each)**

```bash
git log --oneline
```

* **Filter commits by author**

```bash
git log --author="Alice"
```

* **Show recent commits (e.g., last 2 weeks)**

```bash
git log --since="2 weeks ago"
```

* **Show files changed per commit**

```bash
git log --stat
```

* **Show branch history as a graph**

```bash
git log --graph --oneline
```

---

## **2. View Details of a Specific Commit**

* **Show all info for a specific commit**

```bash
git show <commit_hash>
```

> Example: `git show 09f4acd`

---

## **3. Compare Changes**

* **See unstaged changes (working directory vs last commit)**

```bash
git diff
```

* **See staged changes (staging area vs last commit)**

```bash
git diff --staged
```

* **Compare two specific commits**

```bash
git diff <commit1> <commit2>
```

> Example: `git diff 1234567 89abcde`

---

## **Tips / Best Practices**

* Make frequent, meaningful commits.
* Write clear commit messages.
* Use `git diff` before committing to review changes.
* Use `git log --oneline` for a quick overview.
* Press `q` to exit `git log` or `git diff` view.


```bash
git log --follow [file]
```

does 👇

---

## 🔹 Purpose

The `--follow` option makes Git **show the history of a file across renames/moves**.
By default, `git log` only shows commits for the file in its current path.
If the file was renamed, its history before the rename won’t appear unless you use `--follow`.

---

## 🔹 Syntax

```bash
git log --follow <file>
```

---

## 🔹 Example

Suppose you had:

1. `about.html` (original file)
2. Later renamed to `about-us.html`

Now, running:

```bash
git log about-us.html
```

👉 Will show commits **only after the rename**.

But running:

```bash
git log --follow about-us.html
```

👉 Will show the **entire history**, including when it was called `about.html`.

---

## 🔹 Useful Options with `--follow`

* Show patch details (diffs):

  ```bash
  git log --follow -p <file>
  ```
* Show history in one line:

  ```bash
  git log --follow --oneline <file>
  ```
* Limit the number of commits:

  ```bash
  git log --follow -n 5 <file>
  ```

---

✅ **Use Case**: Perfect when tracking the full evolution of a file, especially in projects where files are frequently renamed or reorganized.


