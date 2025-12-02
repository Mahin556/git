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