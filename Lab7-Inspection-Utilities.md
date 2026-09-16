# Lab 7 — Inspection & Utilities

[← Back to index](README.md)

## Step 28 — diff, show, blame, shortlog

> **Use these when:** you need to _understand_ the repo rather than change it. All four are read-only and completely safe to run any time.
>
> - `git diff` — **"what have I changed but not staged yet?"** Run it before `git add` to review your own work.
> - `git diff --stat` — **"which files changed, and by how much?"** Use it for a quick summary before reading the full diff.
> - `git diff --name-only` — **"which files changed?"** Use it when you only need the list of affected files.
> - `git diff --staged` — **"what am I about to commit?"** Run it after `git add`, before `git commit`, to catch a stray debug line or a file you didn't mean to include.
> - `git show <hash>` — **"what exactly did that commit change?"** Useful when `git log` gives you a message like "fix bug" and you need the actual code.
> - `git log --stat -1` — **"what files changed in the latest commit?"** Shows the latest commit with a short file summary.
> - `git log --oneline --decorate --graph -5` — **"what does recent history look like?"** Shows the last five commits and branch pointers in a compact graph.
> - `git blame <file>` — **"who wrote this line and why?"** Find the author and the commit, then `git show` that commit for the reasoning. It's for context, not for blaming people.
### Practical workflow: reviewing changes before a commit

A useful workflow is to inspect your changes at two stages:

1. Make changes to a file.
2. Run `git diff` to review changes that are not staged.
3. Run `git add <file>` to stage the changes.
4. Run `git diff --staged` to review exactly what is prepared for the next commit.
5. If everything looks correct, run `git commit`.

Example:

```bash
git diff
git add hello.txt
git diff --staged
git commit -m "Update hello.txt"

Terminal:

```bash
git diff                            # see unstaged changes
git diff --stat                     # summarize changed files
git diff --name-only                # list changed files
git diff --staged                   # see staged changes
git show a1b2c3d                    # full detail of one commit
git log --stat -1                   # summarize the latest commit
git log --oneline --decorate --graph -5 # show recent history
git blame hello.txt                 # who wrote which line
git shortlog -sn                    # commits count per author
```

---

[← Back to index](README.md)




