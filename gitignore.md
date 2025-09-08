
### **What is `.gitignore`?**

* A file that tells Git **which files/folders to ignore** (not track).
* Prevents clutter from logs, build artifacts, temp files, OS/editor files, or sensitive files.
* The `.gitignore` file itself **is tracked**, so teammates share the same ignore rules.

---

### **When to Use**

* Keep **sensitive or unnecessary files** out of the repo.
* Avoid clutter in Git history.
* Ignore auto-generated files from build tools, IDEs, or OS.

---

### **How to Create**

* At repo root:

  ```bash
  touch .gitignore
  ```

---

### **Key Rules & Patterns**

* **Ignore folders:**

  ```
  temp/
  ```
* **Wildcards:**

  * `*` = any characters → `*.log` ignores all `.log` files
  * `?` = single character → `file?.txt` → matches `file1.txt`, `fileA.txt`
  * `[abc]` = set → `file[abc].txt` → matches `filea.txt`, `fileb.txt`
  * `[!abc]` = negate set → `file[!abc].txt` → excludes `a,b,c`
* **Negation:**

  * `*.log` = ignore all logs
  * `!important.log` = but keep this one
* **Comments:** start with `#`

---

### **Special Uses**

* **Local ignore (per-user):** `.git/info/exclude` (not shared).
* **Global ignore (all repos):**

  ```bash
  git config --global core.excludesfile ~/.gitignore_global
  ```

---

### **Stop Tracking Already Tracked Files**

If a file is already in Git history, `.gitignore` won’t affect it until you remove it:

```bash
git rm --cached filename.txt
```

---

### **Tips & Troubleshooting**

* Case-sensitive → check spelling.
* Use `git status` to verify ignored files.
* `.gitignore` only works on **untracked files**.

---

### **Common Patterns**

| Pattern          | Meaning                                                  |
| ---------------- | -------------------------------------------------------- |
| `*.log`          | Ignore all `.log` files                                  |
| `temp/`          | Ignore `temp` folder and everything inside               |
| `/config.json`   | Ignore `config.json` only in root                        |
| `**/logs/`       | Ignore any `logs` folder anywhere in repo                |
| `!important.log` | Do not ignore this specific file even if pattern says so |

---

👉 In short: **`.gitignore` = cleaner repos, safer collaboration, less clutter**.
