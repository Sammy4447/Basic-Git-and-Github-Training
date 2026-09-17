# Lab 7 — Inspection & Utilities

[← Back to index](README.md)

## Step 28 — diff, show, blame, shortlog

> **Use these when:** you need to _understand_ the repo rather than change it. All four are read-only and completely safe to run any time.
>
> - `git status` — **"what's my current state?"** Staged, unstaged, untracked files.
> - `git diff` — **"what have I changed but not staged yet?"** Run it before `git add` to review your own work.
> - `git diff --stat` — **"which files changed, and by how much?"** Use it for a quick summary before reading the full diff.
> - `git diff --name-only` — **"which files changed?"** Use it when you only need the list of affected files.
> - `git diff --staged` — **"what am I about to commit?"** Run it after `git add`, before `git commit`, to catch a stray debug line or a file you didn't mean to include.
> - `git diff <commit1> <commit2>` — **"what changed between two points in history?"** Works with commit hashes or branch names — e.g. `git diff main feature-branch` to see how a branch differs from `main` before merging.
> - `git show <hash>` — **"what exactly did that commit change?"** Useful when `git log` gives you a message like "fix bug" and you need the actual code.
> - `git log --oneline --decorate --graph -5` — **"what does recent history look like?"** Shows the last five commits and branch pointers in a compact graph.
> - `git blame <file>` — **"who wrote this line and why?"** Find the author and the commit, then `git show` that commit for the reasoning. It's for context, not for blaming people.
> - `git shortlog -sn` — **"who has contributed how much?"** A quick contributor summary for a project. The SN stands for summary numbered.

### Typical Workflow

```bash
git status              # what changed?
git diff                # review unstaged changes
git add file.js         # stage file
git diff --staged       # confirm before commit
git commit -m "fix bug" # commit
```

Terminal:

```bash
git status                          # current state
git diff                            # see unstaged changes
git diff --stat                     # summarize changed files
git diff --name-only                # list changed files
git diff --staged                   # see staged changes
git diff main feature-branch        # compare two branches or commits
git show a1b2c3d                    # full detail of one commit
git log --oneline --decorate --graph -5 # show recent history
git blame hello.txt                 # who wrote which line
git shortlog -sn                    # commits count per author
```

### Pro Tip — Read History Like a Detective

1. **Blame → Show combo:** `git blame` tells you which commit introduced a line, but not *why*. Always follow up with `git show`:

   ```bash
   git blame hello.txt        # copy the short hash from the line you care about
   git show <hash>            # read the full commit message + diff for context
   ```

2. **Smarter diffs for reviews:**

   ```bash
   git diff --word-diff       # highlight changed words, not whole lines — great for docs
   git diff --check           # catch trailing whitespace before you commit
   git diff --stat HEAD~3     # how much changed in the last 3 commits?
   ```

3. **Smarter log / blame:**

   ```bash
   git log -p --follow hello.txt   # full patch history of one file, even across renames
   git blame -L 10,20 hello.txt    # blame only lines 10-20, ignore noise
   git shortlog -sne               # add -e to see names + emails for contact
   ```

### 2-Minute Practice

```bash
# 1. Pick a line you didn't write
git blame hello.txt

# 2. Understand it
git show <hash-from-blame>

# 3. Summarize the repo
git log --oneline --decorate --graph -5
git shortlog -sn
```

> **Rule of thumb:** `status` for now, `diff` for uncommitted work, `show` / `log` / `blame` / `shortlog` for history and people. If you're about to change code, inspect first.

---

[← Back to index](README.md)
