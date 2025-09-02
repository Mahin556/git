### 🔹 `git reset [file]`

* **Purpose:** Unstages a file (removes it from staging/index) but **keeps changes** in your working directory.
* **Use case:** You accidentally added a file with `git add`, but don’t want it in the next commit.
* ✅ Changes still exist in the working directory.
* Example:

  ```bash
  git add file.txt       # staged
  git reset file.txt     # unstaged, but file.txt still modified
  ```

---

### 🔹 `git diff`

* **Purpose:** Shows differences between the **working directory** and the **staging area**.
* ✅ What you changed but have **not yet staged**.
* Example:

  ```bash
  git diff
  ```

  → shows modifications still pending `git add`.

---

### 🔹 `git diff --staged` (or `--cached`)

* **Purpose:** Shows differences between the **staging area** and the **last commit**.
* ✅ What is staged, but **not yet committed**.
* Example:

  ```bash
  git diff --staged
  ```

  → shows what will go into the next commit if you run `git commit`.

---

📌 **Quick mental map:**

* **Working dir ↔ Staging area** → `git diff`
* **Staging area ↔ Last commit** → `git diff --staged`
* **Remove from staging, keep changes** → `git reset [file]`

