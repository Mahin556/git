```bash
git log #View commit history
git log --oneline #short history
git log --stat #Show files changed per commit

git log -n 5       # Show last 5 commits
git log -5         # Same as above
git log --oneline -n 1 #last commit in short

git log --pretty=short     # Short commit info
git log --pretty=full      # Author + Committer
git log --pretty=fuller    # Extra detail
git log --pretty=raw       # Raw format
git log --pretty=oneline   # Each commit in one line
git log --pretty=format:"%h %an %s"

git log --patch #log + diff
git log --patch --reverse
git log -S"hello"
git log -S"hello" --patch

# * `%h` → short hash
# * `%an` → author name
# * `%s` → subject (message)
# * `%ad` → author date
# * `%cn` → committer name
# * `%d` → decorations (branch, tag)

git log --pretty=format:"%h - %an (%ad): %s" --date=short

git log --author="Alice"

git log --grep="bugfix"

git log --since="2 weeks ago"
git log --until="2025-09-01"
git log --since="2025-08-01" --until="2025-09-01"

git log -- main.py
git log src/ utils/

git log abc123..def456   # Commits between two SHAs
git log last5th-commit..lastcommit
git log HEAD~5..HEAD     # Last 5 commits

git log --author="Bob" --grep="feature" --since="1 month ago"

git log --author="Alice" --oneline --stat #Show Author Stats

git log --graph #graph mode

#Decorate with Branch/Tags
git log --decorate
git log --oneline --decorate --graph

git log -p
git log -p -2   # Show last 2 commits with changes

git log --stat
git log --shortstat
git log --numstat
git log --reverse
git log --reverse --stat

git log --date=relative #Relative Dates

#Different Date Formats
git log --date=iso
git log --date=short
git log --date=raw
git log --date=format:'%Y-%m-%d %H:%M'

git log --abbrev-commit #Abbrev Commit IDs

git log -g #Show Reflog

git log --merges --oneline #Show Only Merge Commits

git log -p -- README.md #Show Commits Touching a File

# ✔ Visualize commit history as a graph of branches & merges
git log --graph --oneline --decorate --all

# =============================================================================
# FILE HISTORY ACROSS RENAMES — git log --follow
# =============================================================================
# By default, git log ONLY shows history of the file in its current path.
# If the file was renamed/moved, Git does NOT show history before rename.

# → Use --follow to track history through renames.

git log --follow <file>

# Example:
git log --follow about-us.html

# This shows:
#   • commits when file was called "about.html"
#   • commits after it became "about-us.html"

# -----------------------------------------------------------------------------
# Useful options with --follow
# -----------------------------------------------------------------------------

# ✔ Show commit diffs for this file only
git log --follow -p <file>

# ✔ One-line format
git log --follow --oneline <file>

# ✔ Show only last N commits
git log --follow -n 5 <file>

# ✔ Show complete rename detection + patches
git log --follow -M -p <file>

# =============================================================================
# VIEW REMOTE BRANCH LOGS
# =============================================================================

git log origin/main
git log origin/dev

# ✔ To see what changed on remote since last fetch:
git log HEAD..origin/main --oneline


```