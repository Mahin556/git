Got it 👍 Let’s go over the **`git switch`** command clearly.

---

# 🔄 Git Switch – Complete Guide

## 🔹 What is `git switch`?

The `git switch` command (introduced in **Git 2.23**, Aug 2019) is a **simpler, safer way to switch branches**.

Before, you would use:

```bash
git checkout branch-name
```

But `git checkout` had **too many roles** (switching branches, restoring files, creating branches, etc.), which often confused people.

👉 To fix this, Git split it into:

* `git switch` → for **branches**
* `git restore` → for **files**

---

## 🔹 Basic Usage

### 1. Switch to an Existing Branch

```bash
git switch branch-name
```

✅ Moves HEAD to the given branch.

---

### 2. Create and Switch to a New Branch

```bash
git switch -c new-branch
```

✅ Equivalent to:

```bash
git checkout -b new-branch
```

---

### 3. Switch to a Branch from Remote Tracking

```bash
git switch -t origin/feature
```

✅ Creates a local branch and tracks the remote one.

Or, shorter:

```bash
git switch feature
```

(if `feature` only exists remotely).

---

### 4. Switch Back to Previous Branch

```bash
git switch -
```

✅ Just like `cd -` in Linux, it goes back to the branch you were on before.

---

## 🔹 Key Options

* `-c <name>` → Create and switch to new branch
* `-C <name>` → Create and switch, but overwrite if branch already exists
* `-d` → Detach HEAD at a commit (like checkout in detached mode)
* `-t` → Set up tracking branch when switching to remote branch

---

## 🔹 Difference Between `git switch` and `git checkout`

| Command        | Purpose                                    |
| -------------- | ------------------------------------------ |
| `git switch`   | Only for **branches** (clear & safe)       |
| `git restore`  | Only for **files**                         |
| `git checkout` | Does **both** (but confusing & overloaded) |

👉 So `git switch` is the modern recommended way to move between branches.

---

## 🔹 Examples

1. Switch to `main` branch:

```bash
git switch main
```

2. Create and switch to `dev` branch:

```bash
git switch -c dev
```

3. Switch to a remote-tracking branch:

```bash
git switch -t origin/bugfix
```

4. Go back to the last branch:

```bash
git switch -
```

---

✅ In short:

* Use `git switch` for **branches**
* Use `git restore` for **files**
* Use `git checkout` only if you’re on older Git versions

---

Do you want me to also make a **Git Switch vs Checkout Quick Reference Table** (side-by-side commands) for easy comparison?
