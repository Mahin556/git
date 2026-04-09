### Git Squash & Merge – Notes

#### What is Squash & Merge?
- It is an alternative to normal `git merge` (like 3-Way Merge or Fast-Forward Merge).
- It combines all the commits from a feature branch into **a single commit** before merging into `main`.
- The result is a **clean, linear history** without all the intermediate commits from the feature branch.

#### Why Use Squash & Merge?
- To keep the commit history **clean and simple**.
- When you have 50-60 small commits on a feature branch (e.g., "WIP", "fix typo", "update"), you don't want all of them in the main branch.
- You want just **one commit** representing the entire feature/module.

#### How It Works (Based on the Demo)

1. You have a `main` branch and a `feature/video` branch with 2+ commits.
2. While on `main`, run:
   ```bash
   git merge --squash feature/video
   ```
3. Git stages all changes from the feature branch but **does NOT create a merge commit**.
4. You then create a **single commit** manually:
   ```bash
   git commit -m "Video feature added"
   ```

#### Visual & History Difference
- **Normal merge (3-way/fast-forward):** All individual commits from the feature branch appear in the history.
- **Squash & Merge:** Only the **final single commit** appears. The branch's individual commits are not carried over.

#### Important Things to Remember

1. **No automatic merge commit** – you must commit manually after `--squash`.
2. **The feature branch is NOT marked as merged** – Git does not record that the branch was merged.
   - `git branch --merged` → will **not** show this branch.
   - `git branch --no-merged` → will **still** show this branch.
3. **You must delete the feature branch manually** after squashing and committing.
   - Normal delete (`-d`) will fail (Git thinks it's unmerged).
   - Force delete with capital `-D`:
     ```bash
     git branch -D feature/video
     ```
4. The commits from the feature branch still exist locally but will eventually be cleaned up by Git's garbage collector.

#### Commands Recap

| Command | Purpose |
|---------|---------|
| `git merge --squash <branch>` | Bring changes from `<branch>` into current branch without commit history |
| `git commit -m "message"` | Create a single commit for the squashed changes |
| `git branch --merged` | Lists branches that are considered merged (squash branches won't appear here) |
| `git branch --no-merged` | Lists branches not merged (squash branches will appear here) |
| `git branch -D <branch>` | Force delete a branch (needed after squash & merge) |

#### Summary
> Use **Squash & Merge** when you want a **clean, linear history** and don't need to preserve all the intermediate commits from a feature branch. Remember to manually commit and force-delete the feature branch afterward.