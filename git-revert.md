

# 🔄 Git Revert – Complete Guide

## 🔹 What is Git Revert?

`git revert` is used to **undo a commit safely** by creating a **new commit that reverses the changes** of a specific commit.

👉 Key difference:

* `git reset` changes history (dangerous in shared repos).
* `git revert` **preserves history** (safe for collaboration).

---

## 🔹 Common Git Revert Commands

| Command                     | Purpose                                   |
| --------------------------- | ----------------------------------------- |
| `git revert HEAD`           | Revert the latest commit                  |
| `git revert <commit_hash>`  | Revert a specific commit                  |
| `git revert HEAD~2`         | Revert a commit 2 steps back              |
| `git revert --no-edit HEAD` | Revert without editing commit message     |
| `git revert --continue`     | Continue revert after conflict resolution |
| `git revert --abort`        | Abort the revert if conflicts occur       |
| `git log --oneline`         | View commit history to find commit hash   |
| `git revert --skip`         |                                           |
| ``

---

## 🔹 Step 1 – Find the Commit to Revert

Use:

```bash
git log --oneline
```

Example output:

```
52418f7 (HEAD -> master) Just a regular update, definitely no accidents here...
9a9add8 Added .gitignore
81912ba Corrected spelling error
...
221ec6e First release of Hello World!
```

---

## 🔹 Step 2 – Run Git Revert

### Revert the latest commit

```bash
git revert HEAD --no-edit
```

Output:

```
[master e56ba1f] Revert "Just a regular update, definitely no accidents here..."
 1 file changed, 0 insertions(+), 0 deletions(-)
```

---

### Revert a specific commit

```bash
git revert 9a9add8
```

---

### Revert multiple commits

```bash
git revert HEAD~3..HEAD
```

👉 This reverts the last **3 commits**.

---

## 🔹 Step 3 – Review Changes

After revert, check history again:

```bash
git log --oneline
```

Example:

```
e56ba1f (HEAD -> master) Revert "Just a regular update..."
52418f7 Just a regular update, definitely no accidents here...
9a9add8 Added .gitignore
...
```

---

## 🔹 Handling Conflicts During Revert

If conflicts occur:

1. Resolve conflicts in files manually.
2. Mark resolved files:

   ```bash
   git add <file>
   ```
3. Continue revert:

   ```bash
   git revert --continue
   ```
4. Or abort if needed:

   ```bash
   git revert --abort
   ```

---

## 🔹 Tips & Best Practices

✅ Use `git revert` for **shared repositories** → safer than reset.
✅ Always check commit history with `git log --oneline`.
✅ Add `--no-edit` if you don’t want to open the commit message editor.
✅ Use `git revert --abort` if something goes wrong.
✅ For multiple commits, prefer `git revert <range>` instead of reverting one by one.

---

## 🔹 Quick Comparison – Revert vs Reset

| Command            | Effect                                   | Safe for Shared Repo? |
| ------------------ | ---------------------------------------- | --------------------- |
| `git reset --hard` | Removes commits permanently              | ❌ No                  |
| `git revert`       | Creates a new commit that undoes changes | ✅ Yes                 |


Great 👌 आपने अब **`git revert`** का transcript शेयर किया।
मैं इसे अब आपके लिए **साफ़-सुथरी English में** समझाता हूँ, ताकि आपको `git reset` और `git revert` का अंतर crystal clear हो जाए।

---

# 🔹 Git Revert – Complete Explanation

## 1. What is `git revert`?

* `git revert` is used when you want to **undo a commit**, but without changing the commit history.
* Instead of deleting commits, it **creates a new commit** that reverses the changes of a specific commit.

👉 This is safer than `git reset`, especially in a **shared repo with teammates**.

---

## 2. Why not always use `git reset`?

* `git reset` **rewrites history** (deletes commits).
* If you push this to a remote repo, teammates will face conflicts because their history has commits that you deleted.

📌 Example:

* You reset your branch to remove `C3`.
* Your teammate still has `C3`.
* When merging or pulling, Git sees different histories → **merge conflicts**.

---

## 3. How `git revert` works

* You choose a commit to revert.
* Git makes a **new commit** that applies the *opposite* of the chosen commit’s changes.
* History remains intact.

📌 Example commits:

```
C1 (Added file with "Read")
C2 (Added "Games")
C3 (Added "Gym")
```

Run:

```bash
git revert <commit-hash-of-C3>
```

Result:

```
C1 → C2 → C3 → C4 (Revert "Gym")
```

* `C4` is a new commit that cancels the changes from `C3`.
* File now contains only "Read" and "Games".

---

## 4. Revert Workflow

1. Run:

   ```bash
   git revert <commit-hash>
   ```
2. Git opens your editor with a default commit message:

   ```
   Revert "<original message>"
   This reverts commit <hash>.
   ```
3. Save & exit → Git creates the new revert commit.

---

## 5. Important Notes

* You can revert **any commit** in history, not just the last one.
* If the commit touches lines changed by later commits → you may face **conflicts** (just like merge conflicts). You must resolve them manually.
* `git revert` is **preferred for shared repos** because it doesn’t rewrite history.

---

## 6. Summary: Reset vs Revert

| Command      | What it Does                                                | History           | Safe in Team?         |
| ------------ | ----------------------------------------------------------- | ----------------- | --------------------- |
| `git reset`  | Moves HEAD to older commit (deletes later commits)          | Changes history   | ❌ Dangerous if pushed |
| `git revert` | Creates a new commit that undoes changes of a chosen commit | Preserves history | ✅ Safe                |

---

✅ In short:

* Use `git reset` only for **local/private cleanup**.
* Use `git revert` when working with **others (remote repo)**.

