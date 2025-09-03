Git is a **Distributed Version Control System (DVCS)**.
Here’s what that means:

---

### 🔹 Centralized VCS (like SVN, CVS)

* There is **one central server** that stores all code + history.
* Developers check out code, but usually **don’t have full history** locally.
* If the central server goes down, no commits/pushes/pulls can happen.

---

### 🔹 Distributed VCS (like Git)

* Every developer’s machine has a **full copy of the repository**, including the entire history of commits.
* There’s no single point of failure — you can work **offline**, commit locally, branch, merge, etc.
* The remote server (GitHub, GitLab, Bitbucket) is just a place to **share and synchronize** work, not the single source of truth.

---

### 🔹 Key Benefits of Git being Distributed

1. **Offline work** → You can commit, branch, view history without internet.
2. **Backup** → Every developer’s machine is a complete backup of the repo.
3. **Speed** → Operations like branching, diff, log are very fast since everything is local.
4. **Collaboration** → You can share code peer-to-peer, not only through a central server.

---

👉 Simple Diagram:

```
           (GitHub/GitLab/Bitbucket)
                    [Remote Repo]
                          |
        -----------------------------------------
        |                   |                   |
 [Dev A's Repo]     [Dev B's Repo]     [Dev C's Repo]
 (full history)     (full history)     (full history)
```

Everyone has the **full repo** (history + branches).
The remote is just a **sync point**, not the only copy.
