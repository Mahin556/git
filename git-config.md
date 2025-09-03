
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

## 🔹 Key Takeaways

1. Git configs can be **system-wide**, **user-wide**, or **repo-specific**.
2. **Identity (name + email)** is required before making commits.
3. You can customize the **editor**, **colors**, and **default branch name**.
4. Use `git config --list --show-origin` to debug which file is setting a value.



Do you want me to also create a **one-page cheat sheet (with commands + short descriptions)** for Git configuration that you can keep as a quick reference?
