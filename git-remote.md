
# **Git Remote Commands & Setting GitHub Remote via SSH**

---

## **1. List Remote Repositories**

* **Show all remote names**

```bash
git remote
```

> Example output:

```
origin
upstream
```

* **Show remote names and URLs**

```bash
git remote -v
```

> Example output:

```
origin   https://github.com/user/repo.git (fetch)
origin   https://github.com/user/repo.git (push)
```

---

## **2. Add a Remote Repository**

* **Add a new remote**

```bash
git remote add <name> <url>
```

> Example:

```bash
git remote add origin https://github.com/user/repo.git
```

---

## **3. Remove a Remote Repository**

* **Remove a remote**

```bash
git remote remove <name>
```

> Example:

```bash
git remote remove origin
```

* **Alternative syntax**

```bash
git remote rm <name>
```

---

## **4. Rename a Remote**

```bash
git remote rename <old-name> <new-name>
```

> Example:

```bash
git remote rename origin upstream
```

---

## **5. Show Detailed Information About a Remote**

```bash
git remote show <name>
```

> Example:

```bash
git remote show origin
```

**Output includes:**

* Remote URL
* Branches tracked
* Fetch/push info
* Local/remote differences

---

## **6. Tips**

* After adding a remote, you can fetch or push using its name:

```bash
git fetch origin
git push origin main
```

* Use `git remote -v` to confirm remote URLs before pushing or pulling.

---

## **7. Set GitHub Remote Using SSH**

### **Step 1: Test SSH Connection**

```bash
ssh -T git@github.com
```

> Output example:

```
Hi your-username! You've successfully authenticated, but GitHub does not provide shell access.
```

* If your GitHub username appears, the SSH connection is successful.

---

### **Step 2: Get Repository SSH URL**

* On GitHub: go to your repository → **Code → SSH** → copy the SSH URL

> Example: `git@github.com:your-username/your-repo.git`

---

### **Step 3: Add or Update Remote**

* **Add remote (first time)**

```bash
git remote add origin git@github.com:your-username/your-repo.git
```

* **Update existing remote to use SSH**

```bash
git remote set-url origin git@github.com:your-username/your-repo.git
```

---

### **Step 4: Push/Pull Using SSH**

```bash
git push -u origin main
git pull origin main
```

Excellent 👌 you’re now touching the **advanced side of Git remotes**. Let’s go **deep down into Git remotes** so that you fully understand not just the commands, but also the real-world use cases and workflows.

---

### 🌍 What is a Remote?

* A **remote** is basically a **bookmark (alias)** that points to another Git repository URL.
* Instead of typing the full URL every time, you use its **name** (e.g., `origin`, `upstream`, `backup`).
* Remotes allow collaboration:

  * **Pull / Fetch** = get changes from remote
  * **Push** = send your local commits to remote
  * **Track branches** = keep your local branches in sync with remote branches

---

### 🏗️ Common Remote Names

* `origin` → Default name for the repository you cloned or initialized with.
* `upstream` → Often used for the original repo you forked from.
* `backup` → Could be used for a mirror on another service.
* `deploy` → Sometimes used to push to a deployment server.

---

### ⚙️ Core Remote Operations

#### 1. **Add a Remote**

```bash
git remote add upstream https://github.com/other/repo.git
```

* Adds a new remote named `upstream` pointing to another repo.

---

#### 2. **Remove a Remote**

```bash
git remote remove upstream
```

* Deletes the reference, doesn’t delete the repo itself.

---

#### 3. **Rename a Remote**

```bash
git remote rename origin main-origin
```

* Useful if you need clarity or restructuring in project setup.

---

#### 4. **List Remotes**

```bash
git remote -v
```

* Shows all remotes with fetch/push URLs.

Example:

```
origin   https://github.com/you/repo.git (fetch)
origin   https://github.com/you/repo.git (push)
upstream https://github.com/other/repo.git (fetch)
upstream https://github.com/other/repo.git (push)
```

---

#### 5. **Inspect a Remote**

```bash
git remote show upstream
```

* Shows:

  * Remote URL
  * Tracked branches
  * Push/fetch URLs
  * Whether branches are up to date

---

#### 6. **Fetch from Remote**

```bash
git fetch upstream
```

* Downloads commits and branches from remote without merging them.
* Your local branches remain unchanged.

---

#### 7. **Pull from Remote**

```bash
git pull upstream main
```

* Combines `fetch` + `merge`.
* Downloads and merges changes from `upstream/main` into your current branch.

---

#### 8. **Push to Remote**

```bash
git push origin feature-branch
```

* Uploads your local branch commits to the remote branch.

---

#### 9. **Track a Remote Branch**

```bash
git checkout -b new-feature upstream/new-feature
```

* Creates a local branch `new-feature` that tracks `upstream/new-feature`.
* Any `git pull` while on that branch will automatically pull from upstream.

---

### 🧑‍🤝‍🧑 Real-World Workflow with Multiple Remotes

* **Fork scenario (common in open source):**

  * `origin` → your fork
  * `upstream` → main project repo
* Workflow:

  1. Clone your fork → `origin`
  2. Add main repo → `git remote add upstream URL`
  3. Sync fork:

     ```bash
     git fetch upstream
     git checkout main
     git merge upstream/main
     git push origin main
     ```
  4. Work on a branch and push to your fork (`origin`).
  5. Open a pull request to `upstream`.

---

### 🛠️ Advanced Use Cases

#### **1. Push to multiple remotes at once**

```bash
git remote set-url --add --push origin https://github.com/you/repo.git
git remote set-url --add --push origin https://gitlab.com/you/repo.git
```

* Now `git push origin` pushes to both GitHub and GitLab.

---

#### **2. Read-only remote (for fetching only)**

```bash
git remote set-url --push upstream no_push
```

* Prevents accidental pushes to the `upstream` repo.

---

#### **3. Mirror a Repository**

```bash
git clone --mirror https://github.com/you/repo.git
cd repo.git
git push --mirror https://gitlab.com/you/repo.git
```

* Useful for **backups** or migration.

---

#### **4. Replace Remote URL**

* Switching HTTPS to SSH:

```bash
git remote set-url origin git@github.com:you/repo.git
```

---

### ⚡ Troubleshooting & Best Practices

* **Error: remote not found** → check with `git remote -v`.
* **Error: non-fast-forward push** → run `git pull --rebase origin main` before pushing.
* **Access denied / auth error** → update your credentials or SSH key.
* **Best Practices**:

  * Always name remotes clearly (`origin`, `upstream`, `backup`).
  * Don’t keep unused remotes (clean with `git remote remove`).
  * Use `git remote show <name>` to debug sync issues.
  * Keep forks in sync with `upstream`.

---

✅ **Big Picture:**
Remotes are the **bridge** between your local Git and collaborative/shared repos. Mastering multiple remotes means you can **fork, mirror, backup, and deploy** projects seamlessly.

---

Do you want me to make a **step-by-step exercise repo** (like I did for branching) where you’ll practice:

* adding/removing/renaming remotes,
* syncing fork with upstream,
* pushing to multiple remotes,
* and mirroring a repo?

