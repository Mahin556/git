
## **1. Branch Creation**

* **Create a new branch:**

```bash
git branch <branch-name>
```

Example:

```bash
git branch hello-world-images
```

* **Create and switch to a new branch (shortcut with `-b`):**

```bash
git checkout -b <branch-name>
```

Example:

```bash
git checkout -b emergency-fix
```

* **Rename a branch:**

```bash
git branch -m <old-name> <new-name>
```

Example:

```bash
git branch -m old-name new-name
```

---

## **2. Listing Branches**

* **List all branches in the repository:**

```bash
git branch
```

* Shows the current branch with a `*`:

```
  hello-world-images
* master
```

---

## **3. Switching Between Branches**

* **Switch to an existing branch:**

```bash
git checkout <branch-name>
```

Example:

```bash
git checkout hello-world-images
```

* **Alternative (modern Git) command:**

```bash
git switch <branch-name>
```

---

## **4. Working in a Branch**

* **Check the status of files in the branch:**

```bash
git status
```

* **Stage files for commit (all changes):**

```bash
git add --all
```

* **Stage specific files:**

```bash
git add <file-name>
```

Example:

```bash
git add index.html
```

* **Commit staged changes with a message:**

```bash
git commit -m "Your commit message"
```

Example:

```bash
git commit -m "Added image to Hello World"
```

---

## **5. Merging Branches**

* **Merge a branch into the current branch:**

```bash
git merge <branch-name>
```

Example:

```bash
git merge emergency-fix
```

---

## **6. Deleting Branches**

* **Delete a branch that is already merged:**

```bash
git branch -d <branch-name>
```

Example:

```bash
git branch -d hello-world-images
```

* **Force delete an unmerged branch:**

```bash
git branch -D <branch-name>
```

---

## **7. Other Useful Commands**

* **Check which branch you are currently on:**

```bash
git status
```

* **List all files in the current branch directory:**

```bash
ls
```

* **Check staged and unstaged changes:**

```bash
git status
```

---

### **Best Practices for Branching**

1. Use descriptive branch names: `feature/login-page` or `bugfix/header-crash`.
2. Keep each branch focused on a single purpose.
3. Regularly merge changes from `main` to stay updated.
4. Delete branches after merging to keep the repository clean.

