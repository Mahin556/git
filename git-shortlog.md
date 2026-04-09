`git shortlog` summarizes `git log` output by grouping commits **by author** and showing their commit messages. It's perfect for generating release notes or seeing who contributed what .

```bash
git shortlog [options] [revision-range]
# Or pipe from git log
git log --pretty=short | git shortlog [options]
```

## Most Useful Options

| Option | Description | Example |
|--------|-------------|---------|
| `-s` or `--summary` | Show **only commit count**, no messages | `git shortlog -s` |
| `-n` or `--numbered` | Sort by **number of commits** (descending) | `git shortlog -sn` |
| `-e` or `--email` | Show **email addresses** of authors | `git shortlog -se` |
| `-c` or `--committer` | Group by **committer** instead of author | `git shortlog -sc` |
| `--no-merges` | **Exclude merge commits** | `git shortlog -sn --no-merges` |


### 1. Team Leaderboard (Most Commits First)
```bash
git shortlog -sn --all --no-merges
```
Output:
```
   80  Harry Roberts
   34  Samantha Peters
    3  Tom Smith
```

### 2. Summary with Email Addresses
```bash
git shortlog -se --all
```
Shows each author with their email - useful when the same person uses multiple accounts .

### 3. Time-Range Specific (e.g., Sprint)
```bash
git shortlog -sn --since="2024-01-01" --until="2024-02-01"
```
```bash
git shortlog -sn --since="10 weeks" --until="2 weeks"
```


### 4. Excluding Merge Commits
```bash
git shortlog -sn --no-merges
```

### 5. Specific Branch or Range
```bash
git shortlog -sn main..feature
```
Shows commits on `feature` branch that aren't on `main`.

### 6. Custom Format with Commit Hashes
```bash
git shortlog --format="%h %s" -sn
```


## Advanced Options

| Option | Description |
|--------|-------------|
| `-w[<w>,<i1>,<i2>]` | Line wrap output (width, indent1, indent2)  |
| `--group=trailer:<field>` | Group by commit trailer like `Reviewed-by`  |
| `--group=author --group=trailer:co-authored-by` | Count both authors and co-authors  |

## Fixing Duplicate Authors with .mailmap

When the same person appears as multiple authors (e.g., using different email addresses), create a `.mailmap` file in your repo root:

```
Proper Name <correct@email.com> <wrong@email.com>
Jane Doe <jane@company.com> <jane@laptop.local>
```

After adding `.mailmap`, `git shortlog` will combine commits under the canonical name .

## Quick Reference Card

```bash
# Simple - just counts
git shortlog -sn

# Across all branches
git shortlog -sn --all

# Last 2 weeks only
git shortlog -sn --since="2 weeks"

# Exclude merges, with emails
git shortlog -sne --no-merges

# For release notes (full details)
git shortlog -n --no-merges
```

## Summary

> **`git shortlog`** groups commits by author - perfect for contribution tracking and release notes. Use `-s` for summary counts, `-n` for numeric sorting, and `-e` to show emails. Add a `.mailmap` file to consolidate duplicate author entries .