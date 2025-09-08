Here’s a **clear and practical summary of Git push to GitHub** with the main ideas:

---

* **Purpose**

  * `git push` sends your **local commits** to a **remote repository** (e.g., GitHub).
  * You must commit changes locally (`git commit`) before pushing.

---

* **Basic Push**

  * Push your current branch to GitHub:

    ```bash
    git push origin main
    ```
  * `origin` = remote repo name (default for GitHub).
  * `main` = branch name.

---

* **Force Push**

  * Used when the push is rejected due to non-fast-forward updates (e.g., after `git rebase`).
  * Danger: can **overwrite remote history**.
  * Examples:

    ```bash
    git push --force origin feature-branch
    git push --force-with-lease origin feature-branch   # safer, checks before overwriting
    ```

---

* **Push Tags**

  * Push **all tags**:

    ```bash
    git push --tags
    ```
  * Push a **specific tag**:

    ```bash
    git push origin v1.0
    ```

Push all your local branches to GitHub:
```
git push --all origin
```

---

* **Troubleshooting**

  * **Non-fast-forward error** → run:

    ```bash
    git pull --rebase origin main
    git push origin main
    ```
  * **Authentication failed** → check repository access, SSH/HTTPS credentials, or GitHub token.

---

👉 **Core workflow with GitHub**:

1. Make changes → `git add .`
2. Commit changes → `git commit -m "message"`
3. Push to GitHub → `git push origin branch-name`

---

Do you want me to expand this into a **step-by-step mini-project** (with branches, rebases, force push, and tags) so you can practice **every type of push scenario**?
