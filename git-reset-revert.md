# Git for Data Folks — Revert vs Reset (the *everything-you-need* guide)

Here’s a clean breakdown of your tutorial on **Git Revert vs Git Reset** into bullet points for clarity:

* Git was once mainly for software developers but is now widely used by **data scientists, data engineers, and ML engineers** for version control.
* **Git** (created by Linus Torvalds in 2005) tracks project changes, enables collaboration, and preserves history.

---

* **Git Reset**

  * Moves `HEAD` to a previous commit and modifies working directory/staging depending on options.
  * Types:

    * `git reset --soft <commit>` → Moves `HEAD` back, keeps changes staged.
    * `git reset --mixed <commit>` (default) → Moves `HEAD` back, unstages changes.
    * `git reset --hard <commit>` → Moves `HEAD` back, deletes staged + working directory changes.
  * Best for **private branches** where rewriting history is safe.
  * Example uses:

    * Fixing forgotten files in last commit (`--soft`).
    * Removing files from staged commit (`--mixed`).
    * Resetting everything including working files (`--hard`).

---

* **Git Revert**

  * Creates a **new commit** that undoes the effect of a previous commit (safe for public branches).
  * Does not delete history—preserves commit log.
  * Common forms:

    * `git revert <commit>` → Safely undoes one commit by creating an inverse commit.
    * `git revert --no-edit <commit>` → Uses default commit message without editing.
    * `git revert HEAD` → Reverts the latest commit.
    * `git revert --no-commit <commit>` → Prepares changes without committing automatically (for review).
  * Example: If commit `X` adds two files, `git revert X` will create a new commit that removes those files.

---

* **Revert vs Reset Comparison**

  * **Revert:**

    * Safe for **public branches** (keeps history intact).
    * Creates a new commit that undoes changes.
  * **Reset:**

    * Useful for **private branches** (rewrites history).
    * Moves `HEAD` and optionally modifies staged/working files.

---

👉 Rule of Thumb:

* Use **`git revert`** when working with a **shared/public branch** (collaborators won’t lose history).
* Use **`git reset`** when working on your **local/private branch** (safe to rewrite history).

Do you want me to also create a **step-by-step practical workflow example** where we use both `git reset` and `git revert` on the same repo so you can see the difference in action?


You’re right: Git isn’t just for app devs anymore. Data scientists/engineers and ML folks benefit hugely from clean, auditable history. Below is a **clear mental model** + a **hands-on lab** that takes you from project init to safely undoing changes with **`reset`** and **`revert`**, plus how to **monitor** everything as you go.

---

## 1) The mental model (3 trees + commits)

Git keeps three “copies” of your project:

* **HEAD** → snapshot of your last commit (what’s in history).
* **Index / Staging area** → what will go into the next commit.
* **Working tree** → files on disk you’re editing right now.

Different “undo” commands move or sync these three places.

```
[HEAD]  ←commit
  ↑
[INDEX] ←git add
  ↑
[WORKTREE] ←you edit files
```

---

## 2) Create the practice repo (data-project flavored)

```bash
mkdir git_revert_reset
cd git_revert_reset
git init

# Pretend files for a DS/ML pipeline
touch data_acquisition.py data_preprocessing.py model_training.py

git add data_acquisition.py data_preprocessing.py
git commit -m "feat: add data acquisition & preprocessing scripts"
```

Check state any time:

```bash
git status
git log --oneline --graph --decorate
```

---

## 3) `git reset` — move HEAD (and maybe index/worktree)

**What it is:** “Time travel” your branch pointer (and optionally stage/working files) to an *earlier* commit. It **rewrites history**. Use on **local** branches you haven’t pushed (or you’re okay rewriting).

### Modes (what gets changed)

| Command               | Moves HEAD | Resets INDEX | Resets WORKTREE | Typical use                                                        |
| --------------------- | ---------- | ------------ | --------------- | ------------------------------------------------------------------ |
| `git reset --soft`    | ✅          | ❌            | ❌               | Keep staged/working changes; redo the last commit(s) message/scope |
| `git reset --mixed`\* | ✅          | ✅            | ❌               | **Default**: uncommit *and* unstage, keep changes in working tree  |
| `git reset --hard`    | ✅          | ✅            | ✅               | Throw away local changes to match that commit exactly (**danger**) |

> \*If you run `git reset` with no flag, it’s `--mixed`.

### How to point to a commit

* `HEAD~1` (one commit back), `HEAD~2`, …
* `HEAD^` (parent; useful for merges with `^1`, `^2`)
* A full or short **commit hash**

### Practical scenarios

**A) Forgot a file in the last commit → use `--soft`**

```bash
git reset --soft HEAD~1
git add model_training.py
git commit -m "feat: add all three pipeline scripts"
```

**B) You staged the wrong files → use default (`--mixed`)**

```bash
git reset       # uncommit+unstage but keep edits
git add data_acquisition.py data_preprocessing.py
git commit -m "chore: exclude WIP model_training.py"
```

**C) Nuke local edits and go back → `--hard` (careful)**

```bash
git reset --hard HEAD~1
```

> **Important reality check:** `git reset --hard` resets *tracked* files.
> It **does not delete untracked** files; to remove those you’d use:
>
> ```bash
> git clean -fd   # delete untracked files & dirs
> ```
>
> If an “untracked” file vanished after `--hard`, it likely was **tracked** (verify with `git ls-files --error-unmatch <path>`).

### Undoing a bad reset (life saver)

Use the reflog to find your previous HEAD, then jump back:

```bash
git reflog                     # find the old HEAD (e.g., abc123)
git reset --hard abc123
```

---

## 4) `git revert` — create a new commit that *undoes* another

**What it is:** Safely “undo” by **adding** a commit that inverses an earlier one. It **preserves history** and is the right choice on **shared/public branches**.

### Revert a single commit

```bash
git revert <commit>
# Fix conflicts if prompted, then
git commit        # if revert opened your editor with a message
```

### Revert a range

```bash
# Revert commits (A, B] — i.e., everything after A up to and including B
git revert A..B

# Or pick multiple with no immediate commit, then commit once:
git revert --no-commit A..B
git commit -m "revert: roll back problematic range"
```

### Revert a **merge commit**

You must choose the “mainline” parent (usually `-m 1`):

```bash
git revert -m 1 <merge-commit-hash>
```

* `-m 1` → treat parent #1 as the mainline (the branch you merged *into*).
* Use `git show <merge>` to inspect parents if unsure.

### Re-revert (“undo a revert”)

Just revert the revert commit:

```bash
git revert <revert-commit-hash>
```

### When to choose which

* **Local/private history?** `reset` is fine (faster, cleaner).
* **Shared/public history?** **Prefer `revert`** (no history rewrite).
* You can always **reset locally** and **force-push**… but only if your team’s policies allow it and you’re sure it won’t stomp on others. Safer alternative: revert.

---

## 5) A compact practice lab (do this once, you’ll remember forever)

```bash
# Start clean
rm -rf git_revert_reset && mkdir git_revert_reset && cd git_revert_reset && git init
echo "acq" > data_acquisition.py
echo "prep" > data_preprocessing.py
git add . && git commit -m "feat: add acquisition & preprocessing"

# Commit a bug
echo "buggy" > model_training.py
git add model_training.py
git commit -m "feat: add training (buggy)"

/* --- Try RESET paths --- */

# (A) --soft: pretend last commit didn’t happen; keep staging
git reset --soft HEAD~1
# fix something, restage, recommit
git add model_training.py
git commit -m "feat: add training (fixed)"

/* reset again to recreate buggy state for revert practice */
git reset --hard HEAD~1
git add model_training.py
git commit -m "feat: add training (buggy)"

/* --- Try REVERT paths --- */

# Revert the buggy commit (public-safe)
git revert HEAD            # creates "Revert 'feat: add training (buggy)'" commit

# Introduce two commits, then revert them together
echo "line" >> data_acquisition.py && git add -A && git commit -m "chore: touch acq"
echo "line" >> data_preprocessing.py && git add -A && git commit -m "chore: touch prep"

# Revert both in one shot without committing each:
git revert --no-commit HEAD~1..HEAD
git commit -m "revert: undo recent chores together"
```

Inspect often:

```bash
git log --oneline --graph --decorate --all
git show HEAD
git diff            # unstaged vs worktree
git diff --staged   # staged vs HEAD
```

If you break something:

```bash
git reflog
git reset --hard <good-ref>
```

---

## 6) Monitoring changes like a pro

* **Status & diffs**

  ```bash
  git status
  git diff            # unstaged changes
  git diff --staged   # what will be committed
  ```
* **History**

  ```bash
  git log --oneline --graph --decorate --all
  git show <commit>
  git log -p <path>   # history of a file with patches
  ```
* **Safety net**

  ```bash
  git reflog          # every move HEAD made (resets, checkouts, rebases)
  ```

---

## 7) Team-safe habits (especially for DS/ML repos)

* Do feature work on branches; keep `main` deployable.
* Small, focused commits with clear messages (`feat:`, `fix:`, `chore:`).
* **Use `revert` on shared branches**; keep `reset --hard` for private/local cleanup.
* Protect `main` (branch protection), use PRs + CI for tests.
* Add `.gitignore` (artifacts, datasets, notebooks’ outputs), and consider `.gitattributes`:

  * normalize line endings, mark binaries, or use **Git LFS** for large data.

---

## 8) Quick decision table

| Goal                                      | Command to prefer                       |
| ----------------------------------------- | --------------------------------------- |
| “I want to remake my last commit”         | `git reset --soft HEAD~1` → recommit    |
| “Unstage everything I accidentally added” | `git reset` (mixed)                     |
| “Discard all local edits”                 | `git reset --hard HEAD` *(careful!)*    |
| “Undo a bad commit already pushed”        | `git revert <hash>`                     |
| “Roll back a range of commits”            | `git revert A..B` (maybe `--no-commit`) |
| “Oops, I reset too far”                   | `git reflog` → `git reset --hard <ref>` |
| “Delete untracked junk files/dirs”        | `git clean -fd` *(destructive)*         |

---

### Optional modern equivalents (Git ≥ 2.23)

* Unstage a path: `git restore --staged <path>`
* Discard edits in a path: `git restore <path>`
* Create/switch branch: `git switch -c <branch>`

---

## TL;DR

* **`reset`** rewrites history by moving HEAD (and maybe index/worktree). Great for **local** cleanup.
* **`revert`** *adds* a new commit that undoes another. Best for **shared/public** branches.
* Keep `git reflog` in your back pocket—**it rescues almost everything**.

If you want, I can turn this into a printable **cheat sheet PDF** (tables + commands + flowcharts) for your team.
