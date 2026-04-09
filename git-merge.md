# Git Merge --continue – Notes

## What is `git merge --continue`?

`git merge --continue` is a command used to **resume and complete a merge** after you have resolved merge conflicts. When Git encounters conflicts during a merge, it pauses the process and gives you control to fix them. Once you've resolved the conflicts, `git merge --continue` tells Git to proceed with finalizing the merge commit .

## When Is It Used?

The command can only be run **after a merge has resulted in conflicts** or when the `--no-commit` option was used during the initial merge . It will fail if there is no ongoing merge in progress .

## Complete Workflow for Resolving Conflicts

Here's the step-by-step process when a merge conflict occurs:

**Step 1: Attempt a merge that causes conflicts**
```bash
git merge feature-branch
# Output: "Automatic merge failed; fix conflicts and then commit the result."
```

**Step 2: Resolve the conflicts manually**
- Git marks conflicts in the working tree with special markers (`<<<<<<<`, `=======`, `>>>>>>>`)
- Edit the conflicted files to keep the correct changes

**Step 3: Stage the resolved files**
```bash
git add <resolved-file>
# Or stage all resolved files:
git add .
```

**Step 4: Complete the merge**
```bash
git merge --continue
```

The command checks for an ongoing merge and then calls `git commit` to create the merge commit .

## Relationship with `git commit`

`git merge --continue` is essentially a **synonym for `git commit`** when a merge is in progress . Both commands achieve the same result. The `--continue` option was introduced to make the workflow more consistent with other Git commands like `git rebase --continue` and `git cherry-pick --continue` .

## Other Related Commands

| Command | Purpose |
|---------|---------|
| `git merge --abort` | Aborts the merge and tries to restore the pre-merge state  |
| `git merge --quit` | Forgets the current merge but keeps the index and working tree unchanged  |
| `git commit` | Alternative way to complete a merge (works the same as `--continue`)  |

## Important Notes

1. **You must stage resolved files first** – `git merge --continue` won't work until you've used `git add` to mark conflicts as resolved 

2. **It only works during an active merge** – The command fails if `MERGE_HEAD` doesn't exist (no merge in progress) 

3. **`--continue` takes no arguments** – Running `git merge --continue` with additional arguments will produce an error 

4. **Warning about uncommitted changes** – Starting a merge with uncommitted changes is discouraged, as it may leave you in a state that's hard to recover from if conflicts occur 

## Summary

> **`git merge --continue`** completes a paused merge after you've resolved conflicts. First fix the conflicts, stage the resolved files with `git add`, then run `git merge --continue` to create the merge commit. It works the same as `git commit` but is more explicit about continuing the merge process.