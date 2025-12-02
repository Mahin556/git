  * Used when the push is rejected due to non-fast-forward updates (e.g., after `git rebase`).
  * Danger: can **overwrite remote history**.
  * Examples:

    ```bash
    git push --force origin feature-branch
    git push --force-with-lease origin feature-branch   # safer, checks before overwriting
    ```
* **Troubleshooting**
  * **Non-fast-forward error** → run:
    ```bash
    git pull --rebase origin main
    git push origin main
    ```
  * **Authentication failed** → check repository access, SSH/HTTPS credentials, or GitHub token.
---

