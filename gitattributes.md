
### 🌍 What `.gitattributes` Really Does

* `.gitattributes` lives in your repo (just like `.gitignore`) and **defines how Git should treat certain files**.
* It affects:

  * Line endings (`CRLF` vs `LF`) across Windows/Linux/macOS
  * Whether a file is **text** or **binary**
  * How Git **merges** files
  * How Git shows **diffs**
  * Which files to **ignore in archives**
  * Git **LFS (Large File Storage)** tracking
* Since it’s version-controlled, **all contributors follow the same rules**.

---

### ⚙️ Core Use Cases with Examples

#### 1. **Handle Line Endings (CRLF vs LF)**

* Problem: Different OSes use different line endings (`Windows = CRLF`, `Linux/macOS = LF`).
* Fix with `.gitattributes`:

  ```gitattributes
  * text=auto             # auto-normalize line endings
  *.sh text eol=lf        # enforce LF for shell scripts
  *.bat text eol=crlf     # enforce CRLF for Windows batch scripts
  ```

---

#### 2. **Mark Files as Binary**

* Stops Git from treating them as text (no diffs, no line-ending changes).

  ```gitattributes
  *.png binary
  *.jpg binary
  *.zip binary
  *.exe binary
  ```

---

#### 3. **Git LFS (Large File Storage)**

* Stores large files in LFS instead of bloating Git history.

  ```gitattributes
  *.psd filter=lfs diff=lfs merge=lfs -text
  *.mp4 filter=lfs diff=lfs merge=lfs -text
  *.csv filter=lfs diff=lfs merge=lfs -text
  ```

---

#### 4. **Custom Diff Tools**

* Useful for files like Markdown, Jupyter Notebooks, or JSON.

  ```gitattributes
  *.md diff=markdown
  *.ipynb diff=ipynb
  *.json diff=json
  ```

* Then configure `.git/config` or `~/.gitconfig` with custom diff drivers.

---

#### 5. **Custom Merge Drivers**

* Prevent merge conflicts for tricky files like `package-lock.json` or `requirements.lock`.

  ```gitattributes
  package-lock.json merge=union
  *.lock merge=ours
  ```

---

#### 6. **Exclude Files from Archives**

* When you run `git archive`, exclude docs or configs.

  ```gitattributes
  docs/* export-ignore
  *.md export-ignore
  ```

---

#### 7. **Language/Tool Specific Settings**

* For C++ projects:

  ```gitattributes
  *.cpp text eol=lf
  *.h   text eol=lf
  ```
* For Web projects:

  ```gitattributes
  *.js   text eol=lf
  *.css  text eol=lf
  *.html text eol=lf
  ```

---

### 🔍 Inspecting Attributes

Check what rules apply to a file:

```bash
git check-attr --all README.md
```

---

### ⚡ Advanced Tips

* `.gitattributes` in **subfolders** only affects that folder (local rules).
* If you change `.gitattributes`, you might need to re-checkout/re-add files to apply the changes:

  ```bash
  git rm --cached -r .
  git reset --hard
  ```
* Combine with `.gitignore`:

  * `.gitignore` = which files Git should **not track**
  * `.gitattributes` = how Git should **treat tracked files**

---

✅ **Big Picture:**
Think of `.gitattributes` as the **rulebook for file handling in Git**. It solves hidden problems like inconsistent line endings, binary merges, large file handling, and keeps your repo **collaborator-proof** across platforms.

