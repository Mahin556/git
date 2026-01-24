```bash
git status #Show which files are staged/unstaged
git add .
git add *
git add --all/-A #Stage all changes (new, modified, deleted files)
git add <file_name>... #Stage specific file or files
git restore --staged <file> #Unstage a file or files
git reset HEAD <file> #(Alternative) Unstage a file
```

* **`git add -A` (or `--all`)**
  * Stages **everything**: new files, modified files, and deleted files across the **entire working tree**.
  * Works no matter where you run it (top-level or subdirectory).
  * Since Git v2, this is the **default behavior** of `git add`.

* **`git add -u` (or `--update`)**
  * Stages **only modified and deleted files**.
  * Does **not** stage new/untracked files.
  * Work like -A or --all but only for update and deleted files.

* **`git add .`**
  * Stages new, modified, and deleted files — **but only from the current directory downward**.
  * If run at the repo root → behaves like `git add -A`.
  * If run inside a subdirectory → ignores changes outside that directory.

* **`git add *`**
  * Uses the **shell’s wildcard expansion**, not Git’s logic.
  * Adds visible files in the current directory (no hidden files like `.gitignore` or `.env`).
  * Does not handle deleted files correctly.
  * Can produce **unexpected results**, so it’s generally **not recommended**.

```bash
git commit -m "message" #Commit staged changes with a message
git commit -a -m "message" #Commit all tracked changes (skip staging), but not work with new/untracked file only work with modified/deleted file
git commit --amend #to add files to your last commit.(first add file to staging)
git commit --amend --no-edit #Quickly add staged changes to last commit, keep message
git commit --amend -m "message" #Edit the most recent commit message
git commit --allow-empty -m "message" #Create an empty commit
git commit --no-edit #Use the previous commit message
git commit #add commit in message file or add multi-line commit
git reset --soft HEAD~1 #Undo last commit, keep changes staged

git commit -m "demo" --author="Alice <alice@example.com>"
```
```bash
git log #View commit history
git log --oneline #short history
git log --stat #Show files changed per commit

git log -n 5       # Show last 5 commits
git log -5         # Same as above
git log --oneline -n 1 #last commit in short

git log --pretty=short     # Short commit info
git log --pretty=full      # Author + Committer
git log --pretty=fuller    # Extra detail
git log --pretty=raw       # Raw format
git log --pretty=oneline   # Each commit in one line
git log --pretty=format:"%h %an %s"

# * `%h` → short hash
# * `%an` → author name
# * `%s` → subject (message)
# * `%ad` → author date
# * `%cn` → committer name
# * `%d` → decorations (branch, tag)

git log --pretty=format:"%h - %an (%ad): %s" --date=short

git log --author="Alice"

git log --grep="bugfix"

git log --since="2 weeks ago"
git log --until="2025-09-01"
git log --since="2025-08-01" --until="2025-09-01"

git log -- main.py
git log src/ utils/

git log abc123..def456   # Commits between two SHAs
git log last5th-commit..lastcommit
git log HEAD~5..HEAD     # Last 5 commits

git log --author="Bob" --grep="feature" --since="1 month ago"

git log --author="Alice" --oneline --stat #Show Author Stats

git log --graph #graph mode

#Decorate with Branch/Tags
git log --decorate
git log --oneline --decorate --graph

git log -p
git log -p -2   # Show last 2 commits with changes

git log --stat
git log --shortstat
git log --numstat

git log --date=relative #Relative Dates

#Different Date Formats
git log --date=iso
git log --date=short
git log --date=raw
git log --date=format:'%Y-%m-%d %H:%M'

git log --abbrev-commit #Abbrev Commit IDs

git log -g #Show Reflog

git log --merges --oneline #Show Only Merge Commits

git log --oneline --graph --all --decorate

git log -p -- README.md #Show Commits Touching a File
```
```bash
git help #List all commands

git help <command> #Full manual on browser
git <command> --help

git <command> -h #short help on terminal

git help --all #List all available Git commands, Shows every command grouped by category (Porcelain, Low-level, etc.)

git help -g #List guides and concepts
```
| **Action**            | **Key / Command**  | **Description**                            |
| --------------------- | ------------------ | ------------------------------------------ |
| Scroll down           | ↓ / Space          | Move down through the help text            |
| Scroll up             | `b`                | Move up one page                           |
| Search for a word     | `/` *word*         | Search for a specific word or phrase       |
| Next search result    | `n`                | Jump to the next match                     |
| Quit help viewer      | `q`                | Exit the help window                       |
| Quick command summary | `git <command> -h` | Shows a brief help summary in the terminal |
| Jump to end           | `SHIFT + G`        | Move directly to the end of the help text  |

---

* `git push` send local commits to the remote repo.
```bash
git push
git push -u <remote_repo> <brance>
git push -u origin main
git push --tags #Push all tags
git push origin v1.0 #push a specific tag
git push --all origin #push all local brances to github
git push --all

git push origin --delete <branch-name> #Push deleted branch on local (remove branch from remote)
git push origin --delete feature-login

git push origin dev
```

---

```bash
git branch #list branches
```

---

```bash
git checkout #swithch to brance
git checkout -b dev #create and switch to brance
```

---

* **Git tags** are use to mark a important point it the commit history.
* Used for release, attach to commit like label.
* Used to mark **important points** in history such as:
  * **Releases** (e.g., `v1.0`, `v2.0`).
  * **Milestones** (major features completed, bug fixes).
  * **Deployments** (tools use tags to know which version to deploy).
  * **Hotfixes** (easily find and patch old versions).
* Two types
  * Lightweight `git tag v1.0`
    * Just a name no extra data
  * Annotated `git tag v1.0 -m "Release version 1.0"`
    * Have metadata --> author name, email, date, message
    * Recommended for releases.

```bash
# List all tags
git tag
git tag -n #Show tag messages when listing

# Create lightweight tag
git tag v1.0  # creates tag on CURRENT commit

git tag -l "v1.*"      # List tags with pattern

# Create annotated tag
git tag -a v1.0 -m "Release 1.0"
git tag -a <tagname> -m "message" <commit-hash>

# Tag a specific commit
git tag v1.0 <commit-id>

git show <tag> #show tag detail

git tag new_name old_name     # create new tag pointing to old tag’s commit
git push origin new_name               # push new tag

# Push single tag to remote
git push origin v1.0

#   Signed tags prevent others from faking your releases.
#   You need GPG set up first.
git tag -s v2.0 -m "Signed release v2.0" #Annotated tag, but cryptographically signed for authenticity.

git tag -v v2.0 #Verify signed tag

git tag --contains abc123 #Show tags containing commit

git tag --merged HEAD #Show tags reachable from commit

# Push all tags
git push --tags
git push --tags origin
# Note: Running `git push` alone does **not** push tags.

# Delete local tag
git tag -d v1.0

# Delete remote tag
git push origin --delete tag v1.0
git push origin --delete v1.0

# Checkout code at a tag (detached HEAD - read only)
git checkout v1.0

git checkout -b hotfix v1.0   # Create a new branch from tag

git tag -f v1.0 <new-commit-hash> #force move tag to diff commit

git push --force origin v1.0 #force push tag

# ============================================================
# TAG: TAGGING STRATEGIES (PROFESSIONAL WORKFLOWS)
# ============================================================

# Common release tagging patterns:
#
#   v1.0.0     -> Major.minor.patch (SEMVER standard)
#   prod-2024  -> Monthly/quarterly production builds
#   stable     -> Stable release marker
#   beta-1     -> Pre-release versions
#
# Professional teams use:
#
#   Major = Breaking changes
#   Minor = New features
#   Patch = Bug fixes

# ============================================================
# TAG: VERSION BUMPING WORKFLOW
# ============================================================

# Typical release process:

git commit -m "Add new feature"
git tag -a v1.3.0 -m "Release v1.3.0"
git push origin main
git push origin v1.3.0
```

---

```bash
# ============================================================
#                 GIT + GPG COMPLETE SETUP TUTORIAL
#         (All theory written in comments for easy learning)
# ============================================================


# ------------------------------------------------------------
# STEP 1 — INSTALL GPG
#   GPG (GNU Privacy Guard) allows cryptographic signing of commits.
#   GitHub uses GPG to verify commits with a "Verified" badge.
# ------------------------------------------------------------

# Ubuntu/Debian
sudo apt install gnupg

# RHEL/CentOS
sudo yum install gnupg

# macOS (Homebrew)
brew install gnupg

# Windows:
# Download Gpg4win from https://gpg4win.org/


# ------------------------------------------------------------
# STEP 2 — GENERATE A NEW GPG KEY
# THEORY:
#   This creates your personal digital identity for signing commits.
#   Use the same email as your GitHub account for verification.
# ------------------------------------------------------------

gpg --full-generate-key

# Prompts:
#    (1) RSA and RSA        -> choose option 1
#    Keysize: 4096          -> strongest
#    Expiration: 0          -> never expires
#    Name & Email: must match your GitHub Git config
#    Passphrase: secure password to protect your key


# ------------------------------------------------------------
# STEP 3 — FIND YOUR KEY ID
# THEORY:
#   Git needs the key ID to sign commits/tags with it.
# ------------------------------------------------------------

gpg --list-secret-keys --keyid-format=long

# Output example:
# sec   rsa4096/ABCD1234EFGH5678 2025-01-01
#       1234567890ABCDEF1234567890ABCDEF12345678
# uid   [ultimate] My Name <me@example.com>
#
# KEYID = ABCD1234EFGH5678


# ------------------------------------------------------------
# STEP 4 — CONFIGURE GIT TO USE THIS GPG KEY
# THEORY:
#   Git signs commits/tags using your selected key ID.
# ------------------------------------------------------------

git config --global user.signingkey ABCD1234EFGH5678

# Automatically sign all commits
git config --global commit.gpgsign true

# Automatically sign tags
git config --global tag.gpgSign true


# ------------------------------------------------------------
# STEP 5 — EXPORT YOUR PUBLIC KEY (for GitHub)
# THEORY:
#   GitHub needs your PUBLIC key to verify your signatures.
#   DO NOT share your private key.
# ------------------------------------------------------------

gpg --armor --export ABCD1234EFGH5678

# Copy output:
# -----BEGIN PGP PUBLIC KEY BLOCK-----
# ...
# -----END PGP PUBLIC KEY BLOCK-----


# ------------------------------------------------------------
# STEP 6 — ADD GPG KEY TO GITHUB
# THEORY:
#   This lets GitHub validate your signed commits.
# ------------------------------------------------------------

# Go to:
# GitHub -> Settings -> SSH and GPG Keys -> New GPG Key
# Paste the output of your public key.


# ------------------------------------------------------------
# STEP 7 — TEST GPG SIGNING
# THEORY:
#   A signed commit should show "Verified" on GitHub.
# ------------------------------------------------------------

git commit -m "Test GPG signing"

# Push the commit:
git push

# Check GitHub commit -> should show ✔ Verified


# ------------------------------------------------------------
# STEP 8 — IF GIT CANNOT FIND GPG, FIX PATH
# THEORY:
#   Some systems require explicit gpg binary path.
# ------------------------------------------------------------

git config --global gpg.program gpg

# Windows (Gpg4win):
git config --global gpg.program "C:/Program Files (x86)/GnuPG/bin/gpg.exe"


# ------------------------------------------------------------
# STEP 9 — OPTIONAL: STOP GPG FROM ASKING PASS EVERY TIME
# THEORY:
#   GPG agent can cache your passphrase for hours.
# ------------------------------------------------------------

# Edit config:
nano ~/.gnupg/gpg-agent.conf

# Add:
# default-cache-ttl 7200
# max-cache-ttl 999999

# Reload agent:
gpgconf --reload gpg-agent


# ------------------------------------------------------------
# QUICK SUMMARY (MOST IMPORTANT COMMANDS)
# ------------------------------------------------------------

# Install GPG:
#   sudo yum install gnupg

# Create GPG key:
#   gpg --full-generate-key

# List keys:
#   gpg --list-secret-keys --keyid-format=long

# Configure Git:
#   git config --global user.signingkey KEYID
#   git config --global commit.gpgsign true

# Export public key (for GitHub):
#   gpg --armor --export KEYID

# Test signing:
#   git commit -m "Signed commit"

```

---

```bash
git branch <branch-name>          # Create a new branch
git branch hello-world-images     # Example

git checkout -b <branch-name>     # Create and switch to new branch
git checkout -b emergency-fix     # Example

git branch -m <old> <new>         # Rename a branch
git branch -m old-name new-name   # Example

git branch                        # List all branches
# Output example:
#   hello-world-images
# * master

git checkout <branch-name>        # Switch to an existing branch
git checkout hello-world-images   # Example

git switch <branch-name>          # Modern alternative to checkout

git status                        # Check which branch & file status

git add --all                     # Stage all changes
git add <file-name>               # Stage specific file
git add index.html                # Example

git commit -m "msg"               # Commit staged changes
git commit -m "Added image"       # Example

git merge <branch-name>           # Merge into current branch
git merge emergency-fix           # Example

git branch -d <branch-name>       # Delete merged branch
git branch -d hello-world-images  # Example

git branch -D <branch-name>       # Force delete unmerged branch

ls                                # List files in current directory

git status                        # Check staged + unstaged changes

git push --set-upstream origin <branch-name>    # Push new branch
git push --set-upstream origin branch-one       # Example
```

---

```bash
git remote                        # Show short list of remote names
git remote -v                     # Show remote names with fetch/push URLs

git remote add <name> <url>       # Add a new remote with given name and URL
git remote add origin https://github.com/user/repo.git  # Example: add origin
git remote add origin https://<ACCOUNT>:<TOKEN>@github.com/user/repo.git  

git remote remove <name>          # Remove the named remote (safe - only deletes the bookmark)
git remote rm <name>              # Alternative shorthand to remove a remote

git remote rename <old> <new>     # Rename an existing remote
git remote rename origin upstream # Example rename

git remote show <name>            # Show detailed info about a remote (tracked branches, URLs, etc.)
git remote show origin            # Example: inspect origin

git fetch <remote>                # Download commits/branches from remote without merging
git fetch upstream                # Example: fetch from upstream

git pull <remote> <branch>        # Fetch + merge changes from remote branch into current branch
git pull upstream main            # Example: pull upstream/main into current branch

git pull --rebase origin main     # Fetch then rebase your local commits on top of origin/main (avoids merge commit)

git push <remote> <branch>        # Push local branch commits to the remote branch
git push origin feature-branch    # Example: push feature-branch to origin

git push -u origin <branch>       # Push and set the remote upstream for the local branch
git push -u origin main           # Example: push main and track origin/main

git remote set-url <name> <url>   # Change the URL for an existing remote
git remote set-url origin git@github.com:you/repo.git  # Example: switch origin to SSH URL

ssh -T git@github.com             # Test SSH access to GitHub (will show your GitHub username if successful)

git remote set-url --add --push origin <url>  # Add an additional push URL so pushing goes to multiple remotes
git remote set-url --add --push origin https://gitlab.com/you/repo.git  # Example: add GitLab as extra push target

git remote set-url --push upstream no_push   # Make remote read-only for pushes (prevents accidental pushes)

git clone --mirror <url>          # Create a mirrored clone (all refs, for backup/migration)
git push --mirror <new-url>       # Push mirrored clone to another host (mirror migration)

git checkout -b <local> <remote>/<branch>  # Create local branch that tracks a remote branch
git checkout -b new-feature upstream/new-feature  # Example: track upstream/new-feature locally

git remote -v | sed -n 's/#.*//g' # (optional) quick pipe to view/clean remote output in shell  # show raw remote list

git remote prune <name>           # Remove stale remote-tracking branches that no longer exist on the remote
git remote prune origin           # Example: clean up origin/* refs that were deleted upstream

git remote show origin | grep "Local branches" -A5   # Quick inspect to see tracking/branch differences   # helpful for debugging

# Troubleshooting commands:
git remote -v                     # Confirm correct remote URLs before pushing
git fetch origin                  # Ensure you have latest remote refs for diagnostics
git status                        # Check local branch and staged/unstaged changes before push/pull
```

---

### Scenarios

```bash
git reset --hard HEAD~1     # Reset last commit locally (completely removes the commit)
git push --force            # Force push to overwrite remote history (dangerous, ONLY for practice)
```
```bash
# -----------------------------
# 1. Reset to a specific commit
# -----------------------------
git reset --hard <commit-id>        # Move HEAD and working directory to a specific commit (destructive)
git reset --soft <commit-id>        # Move HEAD only, keep staged changes
git reset <commit-id>               # Move HEAD, keep changes unstaged (mixed reset)

# Example:
git reset --hard a3f5b92            # Reset project to commit a3f5b92


# -----------------------------
# 2. Undo a hard reset (recover lost work)
# -----------------------------
git reflog                          # Show all HEAD history including before resets
git reset --hard <reflog-id>        # Restore lost commit/state using reflog

# Example:
git reset --hard HEAD@{2}           # Return to previous HEAD before reset


# -----------------------------
# 3. Restore deleted commits
# -----------------------------
git reflog                          # Find the commit that was deleted
git checkout <commit-id>            # Temporarily view deleted commit
git branch restore-branch <commit>  # Create a branch from the deleted commit (permanent recovery)

# Example:
git branch restored a3f5b92         # Recover deleted commit into a new branch


# -----------------------------
# 4. Safe vs Unsafe Resets
# -----------------------------

# SAFE (does not rewrite remote history):
git reset --soft <commit>           # Keep all changes staged
git reset <commit>                  # Keep changes unstaged
git revert <commit>                 # Make opposite commit to undo safely
git restore <file>                  # Undo file changes safely

# UNSAFE (rewrites history):
git reset --hard <commit>           # Deletes commits + file changes
git push --force                    # Overwrites remote history (DANGEROUS)
git push --force-with-lease         # Safer force push, avoids overwriting others' work


# -----------------------------
# 5. Revert vs Reset (comparison)
# -----------------------------
# RESET:
git reset --hard <commit>           # Moves branch pointer backward & deletes commits (unsafe for remote)
# Use when: Fixing your own mistakes before pushing

# REVERT:
git revert <commit>                 # Creates NEW commit that reverses the changes
# Use when: Undoing changes AFTER push (safe for team & remote history)

# Example:
git revert a3f5b92                  # Undo commit but keep history intact
```
```bash
git pull --rebase      # Download new commits from remote and reapply your commits on top (fixes push conflicts)
git push               # Push your rebased commits successfully after resolving the history mismatch
```

---

```bash
# ─────────────────────────────────────────────────────────────────────────────
# GIT CHECKOUT — COMPLETE PRACTICAL + INTERNALS GUIDE (CLEAN & COMBINED)
# ─────────────────────────────────────────────────────────────────────────────

# 1️⃣ WHAT IS `git checkout`?
# ---------------------------
# A multi-purpose Git command used to:
#   • switch branches
#   • create new branches
#   • restore files
#   • checkout old commits (detached HEAD mode)

# Since Git 2.23+, Git added:
#   • `git switch`   → for branch switching
#   • `git restore`  → for file restoration
# but `git checkout` still works universally.

# ─────────────────────────────────────────────────────────────────────────────
# 2️⃣ COMMON USAGE OF git checkout
# -------------------------------

# ✓ Switch to a branch
git checkout feature
git checkout master

# ✓ Switch back to previous branch
git checkout -

# ✓ Create & switch to a new branch
git checkout -b test

# ✓ Delete a branch
git branch -d branch-name

# ✓ Restore (discard) changes in a file
git checkout hobbies.txt

# ✓ Restore all files
git checkout .

# ✓ Restore file from a specific commit
git checkout <commit-hash> -- file.txt

# ✓ Checkout a commit (detached HEAD)
git checkout <commit-hash>

# ✓ Relative checkout
git checkout HEAD~2

# ✓ Checkout remote branch
git checkout -t origin/feature
# or
git checkout feature

# ─────────────────────────────────────────────────────────────────────────────
# 3️⃣ DETACHED HEAD (VERY IMPORTANT)
# ---------------------------------
# Normal:
#   HEAD → branch → latest commit
#
# Detached HEAD:
#   HEAD → specific commit (no branch)
#
# If you want to save work in detached mode:
git checkout -b backup

# ─────────────────────────────────────────────────────────────────────────────
# 4️⃣ GIT INTERNALS — HOW CHECKOUT WORKS INTERNALLY
# -------------------------------------------------

# The `.git/HEAD` file tells Git WHERE YOU ARE.

# 📌 Two modes of HEAD:

# A. ATTACHED HEAD (normal branch mode)
# --------------------------------------
# HEAD contains a reference (not a commit hash):
ref: refs/heads/main

# Meaning:
#   HEAD → refs/heads/main → commit hash

# B. DETACHED HEAD
# ----------------
# HEAD contains a commit hash directly:
a1b2c3d4e5f67890...

# Working tree now corresponds to that commit only.

# 📌 refs/ directory structure
# ----------------------------
# .git/
#   ├─ HEAD
#   └─ refs/
#       ├─ heads/     # Local branches
#       │    ├─ main
#       │    ├─ feature1
#       │    └─ bugfix
#       ├─ remotes/   # Remote tracking branches
#       └─ tags/      # Tags

# When you run `git checkout branch`:
#   → HEAD changes to "ref: refs/heads/branch"
#   → Working directory updates to that commit.

# When you run `git checkout <commit>`:
#   → HEAD becomes a raw hash (detached)
#   → Working directory reflects that old snapshot.

# ─────────────────────────────────────────────────────────────────────────────
# 5️⃣ HEAD vs INDEX vs WORKING DIRECTORY
# --------------------------------------

# HEAD  → last committed snapshot of your current branch
# INDEX → staging area (files to be committed next)
# WORKING DIRECTORY → your actual files on disk

# Example:
git checkout -- file.txt
# Restores file from HEAD → discards local changes.

# ─────────────────────────────────────────────────────────────────────────────
# 6️⃣ git checkout vs git switch / git restore
# --------------------------------------------

# Switch branch:
git checkout main       # old
git switch main         # new

# Create branch:
git checkout -b dev     # old
git switch -c dev       # new

# Restore file:
git checkout -- file    # old
git restore file        # new

# Checkout commit:
git checkout abc123     # old
git switch --detach abc123   # new

```

---

```bash
# ─────────────────────────────────────────────────────────────────────────────
# ⚙️ GIT CONFIGURATION GUIDE — SYSTEM, GLOBAL, LOCAL, COMMANDS, VIEWING & EDITING
# ─────────────────────────────────────────────────────────────────────────────

# 1️⃣ WHERE GIT STORES CONFIGURATIONS
# -----------------------------------
# Git uses `git config` to manage settings at 3 levels:

# SYSTEM LEVEL  (affects ALL users + ALL repos)
# Location: /etc/gitconfig  (or Program Files/Git/etc/gitconfig on Windows)
git config --system <key> <value>

# GLOBAL LEVEL  (affects CURRENT USER across all repos)
# Location: ~/.gitconfig OR ~/.config/git/config
git config --global <key> <value>

# LOCAL LEVEL  (affects ONLY the current repository)
# Location: .git/config inside the repo
git config --local <key> <value>

# ✔ Precedence: LOCAL > GLOBAL > SYSTEM
# If the same key exists in multiple locations, LOCAL overrides GLOBAL,
# and GLOBAL overrides SYSTEM.

# ─────────────────────────────────────────────────────────────────────────────
# 2️⃣ VIEW CONFIGURATIONS
# -----------------------

# View all settings + which file they came from:
git config --list --show-origin

# View only local settings:
git config --local --list

# View only global settings:
git config --global --list

# View only system settings:
git config --system --list

# View a single config value:
git config user.name
git config user.email

# See origin of a specific key:
git config --show-origin user.name

# ─────────────────────────────────────────────────────────────────────────────
# 3️⃣ SETTING USER IDENTITY (REQUIRED BEFORE COMMITS)
# ---------------------------------------------------

# Set global identity:
git config --global user.name "Your Name"
git config --global user.email "you@example.com"

# Set identity for a specific repo only:
git config user.name "Project User"
git config user.email "project@example.com"

# ─────────────────────────────────────────────────────────────────────────────
# 4️⃣ CONFIGURE YOUR DEFAULT EDITOR
# ---------------------------------

# VS Code:
git config --global core.editor "code --wait"

# Vim:
git config --global core.editor "vim"

# Nano:
git config --global core.editor "nano"

# Windows Notepad:
git config --global core.editor "notepad"

# Full path example (Windows):
git config --global core.editor "H:/Microsoft VS Code/bin/code --wait"

# ─────────────────────────────────────────────────────────────────────────────
# 5️⃣ ENABLE COLORS FOR BETTER READABILITY
# ---------------------------------------

git config --global color.ui true
git config --global color.status auto
git config --global color.branch auto

# ─────────────────────────────────────────────────────────────────────────────
# 6️⃣ SET DEFAULT BRANCH NAME
# ---------------------------

git config --global init.defaultBranch main

# ─────────────────────────────────────────────────────────────────────────────
# 7️⃣ EDIT, CHANGE OR UNSET CONFIG VALUES
# ---------------------------------------

# Open global config in editor:
git config --global -e

# Unset (remove) a config:
git config --global --unset core.editor

# Replace/update a config:
git config --global user.name "New Name"

# ─────────────────────────────────────────────────────────────────────────────
# 8️⃣ COMMON GIT CONFIG COMMANDS (CHEAT SHEET)
# -------------------------------------------

git config credential.helper "cache --timeout=3600"
git config --local --list
git config user.name
git config --local user.name
git config --system user.name "Your Name"
git config --global core.autocrlf
git config --global color.ui auto
git config --global init.defaultBranch main
git config --global core.editor "code --wait"

# ─────────────────────────────────────────────────────────────────────────────
# 9️⃣ INTERPRETING YOUR CONFIG OUTPUT
# -----------------------------------

# USER INFO:
#   user.name = MahinRaza / Mahin55   (local override beats global)
#   user.email = mahinraza556@gmail.com

# CORE SETTINGS:
#   core.filemode = false            (ignore permission changes)
#   core.ignorecase = true           (case-insensitive FS, Windows/Mac)
#   core.autocrlf = true             (line-end normalization)
#   core.fscache = true              (performance improvement)
#   core.symlinks = false            (Windows limitation)

# REMOTE & BRANCH:
#   remote.origin.url = https://github.com/Mahin556/demo-git.git
#   branch.main.remote = origin
#   branch.main.merge = refs/heads/main

# HTTP / CREDENTIAL:
#   http.sslbackend = schannel
#   credential.helper = manager

# LFS FILTER:
#   filter.lfs.clean = git-lfs clean
#   filter.lfs.smudge = git-lfs smudge
#   filter.lfs.required = true

# COLOR SETTINGS:
#   color.ui = true

# PULL BEHAVIOR:
#   pull.rebase = false  (git pull = merge)

# ─────────────────────────────────────────────────────────────────────────────
# 🔟 KEY TAKEAWAYS
# ----------------
# ✔ Git has 3 config levels — LOCAL > GLOBAL > SYSTEM  
# ✔ You MUST set user.name + user.email before commits  
# ✔ `git config --list --show-origin` helps debug config issues  
# ✔ Editors, colors, default branch & line endings are commonly configured  
# ✔ Local configuration always overrides global/system  
# ✔ Use `git config -e` to safely edit config files  

# ─────────────────────────────────────────────────────────────────────────────
# 🎯 BEST PRACTICE SUMMARY
# -------------------------
#   • Set your identity globally  
#   • Customize your editor  
#   • Configure colors for clarity  
#   • Prefer `main` as default branch  
#   • Use `--show-origin` to resolve conflicts  
#   • Understand precedence to avoid confusion  

# ─────────────────────────────────────────────────────────────────────────────
```

---

```bash
# =============================================================================
# 1️⃣ FIX THE LAST COMMIT (safest)
# =============================================================================

# Change last commit message:
git commit --amend -m "New commit message"

# Add/remove files into last commit:
git add file.txt
git commit --amend

# Amend without changing message:
git commit --amend --no-edit
git commit --amend --no-edit #Delete latest commit and create a new one with new hash with same content.
```

---

```bash
# ─────────────────────────────────────────────────────────────────────────────
# 🔥 GIT RESET IN DEPTH — SOFT vs MIXED vs HARD (FULL EXPLANATION)
# ─────────────────────────────────────────────────────────────────────────────
# Git reset moves:
#   1. HEAD       → which commit your branch points to
#   2. INDEX      → staging area (what’s ready to commit)
#   3. WORKTREE   → actual files on disk
#
# Reset changes WHERE your branch points AND optionally resets staged/unstaged files.
#
# Reset types:
#   • --soft      → move HEAD ONLY
#   • --mixed     → move HEAD + reset INDEX
#   • --hard      → move HEAD + reset INDEX + reset WORKTREE
#
# NOTE: "HEAD~1" means "one commit before the current commit".
# ─────────────────────────────────────────────────────────────────────────────


# =============================================================================
# 1️⃣ SOFT RESET — HEAD moves, INDEX + WORKING DIRECTORY remain untouched
# =============================================================================
git reset --soft HEAD~1

# ✔ WHAT IT DOES:
#   • HEAD moves backward by 1 commit
#   • The undone commit’s changes remain *staged*
#
# ✔ IDEAL WHEN:
#   • You want to combine (squash) multiple commits into one
#   • You committed too early, want to re-commit with more changes
#   • You want to redo last commit cleanly
#
# ✔ VISUAL:
# BEFORE:
#   HEAD → C3 → C2 → C1
#
# AFTER `git reset --soft HEAD~1`:
#   HEAD → C2 → C1
#   Changes from C3 = staged in INDEX
#
# ✔ EXAMPLE WORKFLOW:
#   # You made commit with typo or incomplete changes:
#   git reset --soft HEAD~1     # Undo commit but keep changes staged
#   git add more_changes.txt
#   git commit -m "Fixed + completed commit"
#
# Nothing in working directory is touched. Nothing is lost.
# Safe and easy for rewriting your *last few commits*.
# Give prefrence to file from CWD-->STAGING over a files from COMMIT-->STAGING.


# =============================================================================
# 2️⃣ MIXED RESET — HEAD moves, INDEX reset (default mode)
# =============================================================================
git reset HEAD~1        # same as: git reset --mixed HEAD~1

# ✔ WHAT IT DOES:
#   • HEAD moves backward by 1 commit
#   • Changes from undone commit become *unstaged*
#   • Working directory remains unchanged
#
# ✔ IDEAL WHEN:
#   • You want to edit part of the undone commit
#   • You want to re-stage files selectively
#   • You want to "uncommit" but not lose changes
#
# ✔ VISUAL:
# BEFORE:
#   HEAD → C3 → C2 → C1
#
# AFTER:
#   HEAD → C2 → C1
#   Changes from C3 → moved to WORKING DIRECTORY (unstaged)
#
# ✔ EXAMPLE WORKFLOW:
#   git reset HEAD~1
#   # Now you can stage files selectively:
#   git add file1
#   git add file3
#   git commit -m "New cleaner commit"
#
# This is the most common reset for fixing a bad commit.


# =============================================================================
# 3️⃣ HARD RESET — HEAD, INDEX, WORKTREE all reset (DANGEROUS)
# =============================================================================
git reset --hard HEAD~1

# ✔ WHAT IT DOES:
#   • HEAD moves backward by 1 commit
#   • INDEX cleared to match commit
#   • WORKING DIRECTORY files overwritten
#
# ⚠ RESULT:
#   • The undone commit disappears
#   • All changes in INDEX + WORKTREE are ERASED
#
# ✔ IDEAL WHEN:
#   • You want to discard local experiments completely
#   • You want to return repo EXACTLY to a previous commit
#
# ✔ VISUAL:
# BEFORE:
#   HEAD → C3 → C2 → C1
#
# AFTER:
#   HEAD → C2 → C1
#   Changes in C3 + working directory = ERASED
#
# ✔ EXAMPLE USE CASE:
#   # You created garbage commits and want to start over:
#   git reset --hard HEAD~1
#
# ⚠ WARNING:
#   • DO NOT USE if commit was already pushed.
#   • Only use when you're 100% sure losing changes is OK.


# =============================================================================
# 4️⃣ COMPARISON TABLE — SOFT vs MIXED vs HARD
# =============================================================================

# WHAT IS RESET?
# Reset modifies 3 things: HEAD (branch pointer), INDEX (staging area), WORKTREE (files).

#      ┌──────────────┬──────────────┬──────────────┬───────────────┐
#      │ RESET TYPE    │ HEAD MOVED?  │ INDEX RESET? │ WORKTREE RESET│
#      ├──────────────┼──────────────┼──────────────┼───────────────┤
#      │ --soft        │ YES          │ NO           │ NO            │
#      │ --mixed       │ YES          │ YES          │ NO            │
#      │ --hard        │ YES          │ YES          │ YES           │
#      └──────────────┴──────────────┴──────────────┴───────────────┘

# Cheat Summary:
#   soft  → "undo commit but leave everything staged"
#   mixed → "undo commit but leave changes unstaged"
#   hard  → "undo commit AND delete changes"


# =============================================================================
# 5️⃣ PRACTICAL USAGE SCENARIOS
# =============================================================================

# ● YOU WANT TO FIX THE LAST COMMIT (typo, forgot files)
git reset --soft HEAD~1
# → fixes commit but keeps all changes staged

# ● YOU WANT TO MODIFY PART OF THE LAST COMMIT
git reset HEAD~1
# → files are unstaged; choose what to commit

# ● YOU WANT TO DELETE BAD CHANGES ENTIRELY
git reset --hard HEAD~1

# ● YOU WANT TO SQUASH MULTIPLE COMMITS MANUALLY
git reset --soft HEAD~3
git commit -m "Squashed all 3 commits"

# ● YOU COMMITTED WRONG FILES
git reset HEAD~1   # unstages them so you can re-commit correctly


# =============================================================================
# 6️⃣ VERY IMPORTANT WARNINGS
# =============================================================================

# ❌ Never hard reset a pushed commit.
# ❌ Never rewrite public/shared history unless coordinated.
# ✔ Always make a backup branch before resetting:

git branch backup-before-reset

# ✔ Use hard reset ONLY in personal branches or local experiments.


# =============================================================================
# 7️⃣ BONUS: RESET VS REVERT (MOST COMMON CONFUSION)
# =============================================================================

# RESET  → rewrites history (dangerous), moves HEAD backwards.
# REVERT → creates a new commit that undoes changes safely.

# Example:
git revert <commit-id>
# → safe for shared branches because it does NOT delete history.

# Reset = rewrite
# Revert = patch that undoes safely
# =============================================================================
```

---

```bash
# ─────────────────────────────────────────────────────────────────────────────
# 📜 GIT HISTORY & DIFF COMMANDS — FULL GUIDE WITH THEORY (LOG, SHOW, DIFF, FOLLOW)
# ─────────────────────────────────────────────────────────────────────────────


# =============================================================================
# 1️⃣ VIEW COMMIT HISTORY
# =============================================================================

# ✔ Full commit history (detailed view: author, date, message, diff context)
git log

# ✔ One-line summary per commit (clean, compact)
git log --oneline

# ✔ Filter commits by author name or email
git log --author="Alice"

# ✔ Show commits from a specific period
git log --since="2 weeks ago"
git log --since="2024-01-01"

# ✔ Show which files changed per commit (summary)
git log --stat

# ✔ Visualize commit history as a graph of branches & merges
git log --graph --oneline --decorate --all


# =============================================================================
# 2️⃣ VIEW DETAILS OF A SPECIFIC COMMIT
# =============================================================================

# ✔ Display full commit info + patch/diff
git show <commit_hash>

# Example:
git show 09f4acd

# Shows:
#   • commit message
#   • author + date
#   • file changes
#   • diff of each changed file


# =============================================================================
# 3️⃣ COMPARE CHANGES (DIFF)
# =============================================================================

# ✔ Diff of unstaged changes (working directory vs last commit)
git diff

# ✔ Diff of staged changes (index vs last commit)
git diff --staged

# ✔ Compare ANY two commits
git diff <commit1> <commit2>

# Example:
git diff 1234567 89abcde

# ✔ Compare commit vs working directory:
git diff <commit> .


# =============================================================================
# 4️⃣ FILE HISTORY ACROSS RENAMES — git log --follow
# =============================================================================
# By default, git log ONLY shows history of the file in its current path.
# If the file was renamed/moved, Git does NOT show history before rename.

# → Use --follow to track history through renames.

git log --follow <file>

# Example:
git log --follow about-us.html

# This shows:
#   • commits when file was called "about.html"
#   • commits after it became "about-us.html"


# -----------------------------------------------------------------------------
# 🔹 Useful options with --follow
# -----------------------------------------------------------------------------

# ✔ Show commit diffs for this file only
git log --follow -p <file>

# ✔ One-line format
git log --follow --oneline <file>

# ✔ Show only last N commits
git log --follow -n 5 <file>

# ✔ Show complete rename detection + patches
git log --follow -M -p <file>


# =============================================================================
# 5️⃣ BEST PRACTICES
# =============================================================================

# ✔ Make small, meaningful commits
# ✔ Review changes using:
git diff         # before staging
git diff --staged   # before committing

# ✔ Use compact history view:
git log --oneline --graph

# ✔ Press 'q' to exit log, diff, or show views
# ✔ Use --since to find active development periods
# ✔ Use --follow for files that were moved or renamed


# =============================================================================
# 🧠 SUMMARY OF WHAT EACH COMMAND DOES
# =============================================================================

# git log              → detailed commit history
# git log --oneline   → compact history
# git log --graph     → visualize branches and merges
# git show <commit>   → inspect a specific commit
# git diff            → working directory vs HEAD
# git diff --staged   → index vs HEAD
# git diff A B        → compare any two commits
# git log --follow    → show file history including renames


# ─────────────────────────────────────────────────────────────────────────────
```

---

```bash
# ─────────────────────────────────────────────────────────────────────────────
# 🔄 GIT FETCH, DIFF, MERGE, PULL, PUSH — FULL GUIDE (BRANCH COMPARISON)
# ─────────────────────────────────────────────────────────────────────────────


# =============================================================================
# 1️⃣ LIST ALL BRANCHES (LOCAL + REMOTE)
# =============================================================================

git branch -a

# Shows:
#   • Local branches        →   main, feature/login
#   • Remote branches       →   origin/main, origin/dev, upstream/main


# =============================================================================
# 2️⃣ UPDATE REMOTE-TRACKING BRANCHES (IMPORTANT)
# =============================================================================
# Before comparing your work with remote, always fetch updates.

git fetch                  # updates all remotes
git fetch origin           # updates only origin
git fetch origin main      # fetch only main branch from origin
git fetch upstream main    # fetch from another remote


# WHY FETCH?
# ----------
# Git does NOT automatically update:
#   origin/main
#   origin/dev
#   upstream/main
# You MUST fetch to sync remote-tracking references.


# =============================================================================
# 3️⃣ COMPARE LOCAL BRANCH WITH REMOTE BRANCH
# =============================================================================

# Syntax:
git diff <local-branch> <remote>/<branch>

# Examples:
git diff origin/main              # compare current branch with origin/main
git diff main origin/main         # compare local main vs remote main
git diff feature/login origin/main

# Meaning:
#   → Shows what will change if you merge or pull.


# TIP:
# To preview what your *push* will send to remote:
git diff origin/main main


# =============================================================================
# 4️⃣ COMPARE TWO COMMITS
# =============================================================================

git diff <commit1> <commit2>

# Example:
git diff 12ab34c a98fde0


# =============================================================================
# 5️⃣ MERGE REMOTE BRANCH INTO LOCAL BRANCH
# =============================================================================
# You must be on the branch you want to update.

# Example: Merge remote main → local main
git checkout main
git merge origin/main

# After merge:
#   → Your local main now includes remote changes.


# =============================================================================
# 6️⃣ GIT PULL (FETCH + MERGE)
# =============================================================================

git pull

# Equivalent to:
#   git fetch
#   git merge origin/<current-branch>

# Example:
git pull origin main


# =============================================================================
# 7️⃣ PUSH CHANGES TO REMOTE
# =============================================================================

git push origin main

# If remote is already set for the branch:
git push origin


# =============================================================================
# 8️⃣ VIEW REMOTE BRANCH LOGS
# =============================================================================

git log origin/main
git log origin/dev


# =============================================================================
# 9️⃣ SHORTCUTS & BEST PRACTICES
# =============================================================================

# ✔ Before comparing: always fetch
git fetch

# ✔ To compare your branch with upstream:
git diff origin

# This works if:
#   • Your branch tracks origin/<branch>
#   • "origin" is the upstream of your branch


# ✔ Best way to preview changes before pushing:
git diff origin/<branch> <branch>

# Example:
git diff origin/main main


# ✔ To see what changed on remote since last fetch:
git log HEAD..origin/main --oneline


# =============================================================================
#  🔟 COMPARISON SUMMARY TABLE
# =============================================================================

# Compare local ↔ remote:
git diff main origin/main

# Compare working directory ↔ HEAD:
git diff

# Compare staging area ↔ HEAD:
git diff --staged

# Compare commit ↔ commit:
git diff C1 C2

# Compare remote ↔ local BEFORE pulling:
git diff origin/main main

# View remote logs:
git log origin/main

# Fetch remote updates:
git fetch


# ─────────────────────────────────────────────────────────────────────────────
```


* git switch
```bash
# Introduced in Git 2.23 to simplify branch switching and creation.
# `git switch` is safer and clearer than:
#     git checkout <branch>
# switch   = branch-only operations (clean, simple)
# ─────────────────────────────────────────────────────────────────────────────

# =============================================================================
# 1️⃣ SWITCH TO AN EXISTING BRANCH
# =============================================================================
git switch <branch>
# Example:
git switch main
git switch dev
# This is equivalent to:
#   git checkout main
# But safer and clearer.

# =============================================================================
# 2️⃣ CREATE A NEW BRANCH AND SWITCH TO IT
# =============================================================================
git switch -c <new-branch>
# Example:
git switch -c feature/login
# Same as:
#   git checkout -b feature/login


# =============================================================================
# 3️⃣ SWITCH BACK TO PREVIOUS BRANCH (toggle)
# =============================================================================
git switch -
#git checkout -
# Useful when switching between two branches repeatedly.


# =============================================================================
# 4️⃣ SWITCH BRANCHES EVEN WITH UNSAVED CHANGES
# =============================================================================
# If your working directory has modifications:
#   • Git may block switching if changes would be overwritten.
# Force switch while keeping changes:
git switch --merge <branch>
# OR:
git switch --discard-changes <branch>   # WARNING: discards changes permanently

# =============================================================================
# 5️⃣ SWITCH TO A BRANCH THAT HAS NO WORKTREE YET (multi-worktree setups)
# =============================================================================
git switch --detach <commit>
# Equivalent of: git checkout <commit> (detached HEAD)
# Example:
git switch --detach HEAD~2

# =============================================================================
# 6️⃣ VIEW WHICH BRANCH WILL BE SWITCHED TO (tracking info)
# =============================================================================
# List branches:
git branch
# Show branch + upstream tracking:
git branch -vv
```

```bash
┌──────────────────────── HOW TO CLONE ALL BRANCHES IN GIT ────────────────────────┐
│                                                                                  │
│ By default, when you clone a Git repository, all branches are downloaded,        │
│ but only one branch (usually main or master) is checked out locally.             │
│                                                                                  │
│ Clone the repository (this already fetches all branches):                        │
│                                                                                  │
│   git clone <repository-url>                                                     │
│                                                                                  │
│ View all branches (local + remote):                                              │
│                                                                                  │
│   git branch -a                                                                  │
│                                                                                  │
│ Fetch all remote branches explicitly:                                            │
│                                                                                  │
│   git fetch --all                                                               │
│                                                                                  │
│ Create local branches for all remote branches:                                   │
│                                                                                  │
for branch in $(git branch -r | grep -v '\->'); do                             
  git branch --track "${branch#origin/}" "$branch"                             
done                                                                           
│                                                                                  │
│ Verify all local branches:                                                       │
│                                                                                  │
│   git branch                                                                    │
│                                                                                  │
│ Switch to any branch:                                                            │
│                                                                                  │
│   git checkout <branch-name>                                                     │
│   or                                                                             │
│   git switch <branch-name>                                                       │
│                                                                                  │
│ Important points:                                                                │
│ • git clone downloads all branch data by default                                 │
│ • Remote branches appear as origin/branch-name                                   │
│ • Local branches are created only when checked out or tracked                    │
│ • Loop command is useful when repository has many branches                       │
│                                                                                  │
│ Manual alternative:                                                             │
│                                                                                  │
│   git branch -r                                                                 │
│   git checkout -b <branch-name> origin/<branch-name>                              │
│                                                                                  │
│ Interview one-liner:                                                             │
│ “Git clone fetches all branches by default, but only the default branch is       │
│  checked out locally. Other branches must be explicitly created or tracked.”     │
│                                                                                  │
└──────────────────────────────────────────────────────────────────────────────────┘
```