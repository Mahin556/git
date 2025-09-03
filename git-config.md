
# ⚙️ Git Configuration Guide

Once Git is installed, the **first step** is to configure your Git settings.
This setup ensures Git can correctly identify you and behave the way you prefer.

---

## 🔹 Where Git Stores Configurations

Git uses a tool called `git config` to manage settings. These can be defined at **three levels**:

1. **System Level** – `[path]/etc/gitconfig`

   * Applies to all users and all repositories on the system.
   * Use `--system` flag.
   * Requires administrator/root privileges.

   ```bash
   git config --system <key> <value>
   ```

2. **Global Level** – `~/.gitconfig` or `~/.config/git/config`

   * Applies only to the current user across all repositories.
   * Use `--global` flag.

   ```bash
   git config --global <key> <value>
   ```

3. **Local Level** – `.git/config` (inside each repository)

   * Applies only to that specific repository.
   * Default if no flag is used.

   ```bash
   git config --local <key> <value>
   ```

👉 **Precedence:** Local > Global > System
(If the same key exists in multiple places, the last one read overrides the others.)

---

## 🔹 Viewing Configuration

To see all settings and where they come from:

```bash
git config --list --show-origin
```

Example output (trimmed):

```
file:C:/Program Files/Git/etc/gitconfig core.autocrlf=true
file:C:/Users/User/.gitconfig user.name=Tutorialspoint
file:C:/Users/User/.gitconfig user.email=test@tutorialspoint.com
```

To check a single setting:

```bash
git config user.name
git config user.email
```

To see which file sets a value:

```bash
git config --show-origin user.name
```

---

## 🔹 Setting Up Your Identity

Git associates each commit with a **name** and **email**.

Set them globally:

```bash
git config --global user.name "Your Name"
git config --global user.email your_email@example.com
```

Set them for one repository only:

```bash
git config user.name "Project Specific Name"
git config user.email project_email@example.com
```

---

## 🔹 Configure Default Editor

When Git requires a message (e.g., commit, merge), it opens a text editor.
Set your preferred editor:

* **Visual Studio Code**

  ```bash
  git config --global core.editor "code --wait"
  ```

* **Vim**

  ```bash
  git config --global core.editor "vim"
  ```

* **Nano**

  ```bash
  git config --global core.editor "nano"
  ```

* **Windows Notepad**

  ```bash
  git config --global core.editor "notepad"
  ```

⚠️ On Windows, sometimes you must give the full path:

```bash
git config --global core.editor "H:/Microsoft VS Code/bin/code --wait"
```

---

## 🔹 Configure Colors

To make Git output easier to read:

```bash
git config --global color.ui true
git config --global color.status auto
git config --global color.branch auto
```

---

## 🔹 Default Branch Name

By default, Git creates the first branch as `master`.
You can change it to `main` (or any name you prefer):

```bash
git config --global init.defaultBranch main
```

---

## 🔹 Example: Listing Current Settings

```bash
git config --list
```

Output:

```
user.name=Tutorialspoint
user.email=test@tutorialspoint.com
core.editor=code --wait
color.ui=true
init.defaultBranch=main
```
---
### Changing or Unsetting Config Values
Again run `git config` to overwrite the values or using --unset flag to unset the value.
```
git config --global --unset code.editor
```


---



### **User Information** 👤
* `user.email`: **mahinraza556@gmail.com**
* `user.name`: **MahinRaza** and **Mahin55** (The latter entry seems to override the former, depending on the scope of the config file. A user can have different names/emails for global and local repos).

***

### **Core Configuration** ⚙️
* `core.repositoryformatversion`: **0**
* `core.filemode`: **false** (Git will not track changes to file permissions).
* `core.bare`: **false**
* `core.logallrefupdates`: **true**
* `core.symlinks`: **false** (Symbolic links are not created or stored as such).
* `core.ignorecase`: **true** (Git will ignore file case differences, which is common on Windows and macOS).
* `core.autocrlf`: **true** (Handles automatic conversion of line endings, common on Windows).
* `core.fscache`: **true** (Improves performance by caching file system data).

***

### **Remote and Branch Information** 🌳
* `remote.origin.url`: **[https://github.com/Mahin556/demo-git.git](https://github.com/Mahin556/demo-git.git)** (The URL for the remote named 'origin').
* `remote.origin.fetch`: **+refs/heads/*:refs/remotes/origin/*** (Specifies which branches to fetch from the remote).
* `branch.main.remote`: **origin** (Specifies the remote for the 'main' branch).
* `branch.main.merge`: **refs/heads/main** (Specifies the branch on the remote that 'main' should merge from).
* `branch.demo.vscode-merge-base`: **origin/main** (A configuration specific to Visual Studio Code for merging).

***

### **HTTP and Credential Settings** 🔒
* `http.sslbackend`: **schannel** (Specifies the SSL/TLS library to use, in this case, the Windows-native one).
* `credential.helper`: **manager** (A credential manager is used to store login information).
* `credential.https://dev.azure.com.usehttppath`: **true** (Allows the credential helper to use the full URL path, useful for specific hosts like Azure DevOps).

***

### **Filter and Diff Settings** 🔍
* `filter.lfs.clean`: **git-lfs clean -- %f** (Command to run when cleaning files managed by Git Large File Storage).
* `filter.lfs.smudge`: **git-lfs smudge -- %f** (Command to run when checking out files managed by Git LFS).
* `filter.lfs.process`: **git-lfs filter-process** (A filter process for LFS).
* `filter.lfs.required`: **true** (Specifies that Git LFS is required for this repository).
* `diff.astextplain.textconv`: **astextplain** (A text conversion filter for diffing, useful for non-text files).

***

### **Color Settings** 🎨
* `color.ui`: **true** (Enables colorized output for all Git commands).
* `color.status`: **auto**
* `color.branch`: **auto**

***

### **Pull Configuration** ⬇️
* `pull.rebase`: **false** (When you run `git pull`, it will perform a merge instead of a rebase).


## 🔹 Key Takeaways
1. Git configs can be **system-wide**, **user-wide**, or **repo-specific**.
2. **Identity (name + email)** is required before making commits.
3. You can customize the **editor**, **colors**, and **default branch name**.
4. Use `git config --list --show-origin` to debug which file is setting a value.
   
