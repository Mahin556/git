Got it 👍 You want **`git log` with ALL its options**, explained in detail. This is a **big command** with many flags, so I’ll cover:

* Basic usage
* Formatting options
* Filtering commits
* Decoration & graph view
* Advanced pretty formats

---

# 🔹 `git log` — Full Reference

**Basic Syntax:**

```bash
git log [<options>] [<revision range>] [[--] <path>…]
```

By default, `git log` shows commit history in reverse chronological order.

---

## 🔹 Common Options

1. **Limit the Number of Commits**

```bash
git log -n 5       # Show last 5 commits
git log -5         # Same as above
```

2. **Pretty Print Formats**

```bash
git log --oneline          # Short: commit hash + message
git log --pretty=short     # Short commit info
git log --pretty=full      # Author + Committer
git log --pretty=fuller    # Extra detail
git log --pretty=raw       # Raw format
git log --pretty=oneline   # Each commit in one line
```

3. **Custom Pretty Print**

```bash
git log --pretty=format:"%h %an %s"
```

* `%h` → short hash
* `%an` → author name
* `%s` → subject (message)
* `%ad` → author date
* `%cn` → committer name
* `%d` → decorations (branch, tag)

Example:

```bash
git log --pretty=format:"%h - %an (%ad): %s" --date=short
```

---

## 🔹 Filtering Commits

1. **By Author**

```bash
git log --author="Alice"
```

2. **By Commit Message**

```bash
git log --grep="bugfix"
```

3. **By Date**

```bash
git log --since="2 weeks ago"
git log --until="2025-09-01"
git log --since="2025-08-01" --until="2025-09-01"
```

4. **By Path (specific files)**

```bash
git log -- main.py
git log src/ utils/
```

5. **By Range of Commits**

```bash
git log abc123..def456   # Commits between two SHAs
git log HEAD~5..HEAD     # Last 5 commits
```

6. **Combine Filters**

```bash
git log --author="Bob" --grep="feature" --since="1 month ago"
```

---

## 🔹 Display Options

1. **Graph Mode**

```bash
git log --graph
```

2. **Decorate with Branch/Tags**

```bash
git log --decorate
git log --oneline --decorate --graph
```

3. **Show Patch (Diff)**

```bash
git log -p
git log -p -2   # Show last 2 commits with changes
```

4. **Show Stats**

```bash
git log --stat
git log --shortstat
git log --numstat
```

---

## 🔹 Advanced Formatting

1. **Relative Dates**

```bash
git log --date=relative
```

(Shows "2 hours ago" instead of full date)

2. **Different Date Formats**

```bash
git log --date=iso
git log --date=short
git log --date=raw
git log --date=format:'%Y-%m-%d %H:%M'
```

3. **Abbrev Commit IDs**

```bash
git log --abbrev-commit
```

4. **Show Reflog**

```bash
git log -g
```

---

## 🔹 Other Useful Flags

* `--reverse` → Show commits oldest to newest
* `--follow <file>` → Track history of a file across renames
* `--merges` → Show only merge commits
* `--no-merges` → Exclude merge commits
* `--all` → Show logs of all branches
* `--first-parent` → Follow only first parent in merges
* `--cherry` → Show commits unique to a branch

---

## 🔹 Examples

1. **Compact Branch History**

```bash
git log --oneline --graph --all --decorate
```

2. **Show Only Merge Commits**

```bash
git log --merges --oneline
```

3. **Show Commits Touching a File**

```bash
git log -p -- README.md
```

4. **Show Author Stats**

```bash
git log --author="Alice" --oneline --stat
```

---

✅ **Summary**:

* Use **`--pretty`** to control formatting.
* Use **`--grep`, `--author`, `--since`, `--until`** to filter.
* Use **`--stat`, `-p`** to see code changes.
* Use **`--graph --decorate`** to visualize branching.

---

Do you want me to also build a **cheat sheet table (all `git log` flags with descriptions in one place)** so you can keep it handy while practicing?
