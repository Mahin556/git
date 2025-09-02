
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

