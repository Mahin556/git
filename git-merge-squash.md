Nice 👍 You’re asking about

```bash
git merge --squash demo
```

Let’s break it down:

---

## 🔹 What it does

* `git merge --squash demo` **merges all commits** from the branch `demo` **into the current branch**,
  **but instead of keeping each commit, it squashes them into one single commit**.
* The changes from `demo` are applied in your working directory, but **no merge commit is created automatically**.
* You then manually commit them.

---

## 🔹 Example workflow

```bash
# make sure you are on the branch you want to merge into
git checkout main

# squash merge demo branch into main
git merge --squash demo

# all changes from demo are staged now
# you create ONE commit
git commit -m "Merged demo branch as a single commit"
```

---

## 🔹 Difference from normal merge

* `git merge demo`: keeps **all commits** from `demo` + creates a **merge commit**.
* `git merge --squash demo`: takes **all changes** from `demo`, stages them, and lets you commit them as **one commit**. No merge commit.

---

## 🔹 When to use

✅ Useful if:

* You want to keep your **history clean**.
* You don’t want all the small commits from `demo`, only the final result.

⚠️ Note: After a squash merge, Git does **not record the branch as merged**. So if you run `git branch --merged`, `demo` won’t show up.

---

👉 Do you want me to also show you how to **squash commits during rebase** (instead of squash merge)? That’s another common way people clean history.
