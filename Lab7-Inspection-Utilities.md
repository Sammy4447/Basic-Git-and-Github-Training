# Lab 7 — Inspection & Utilities

[← Back to index](README.md)

## Step 28 — diff, show, blame, shortlog

> **Use these when:** you need to *understand* the repo rather than change it. All four are read-only and completely safe to run any time.
>
> - `git diff` — **"what have I changed but not staged yet?"** Run it before `git add` to review your own work.
> - `git diff --staged` — **"what am I about to commit?"** Run it after `git add`, before `git commit`, to catch a stray debug line or a file you didn't mean to include.
> - `git show <hash>` — **"what exactly did that commit change?"** Useful when `git log` gives you a message like "fix bug" and you need the actual code.
> - `git blame <file>` — **"who wrote this line and why?"** Find the author and the commit, then `git show` that commit for the reasoning. It's for context, not for blaming people.
> - `git shortlog -sn` — **"who has contributed how much?"** A quick contributor summary for a project.

Terminal:

```bash
git diff                            # see unstaged changes
git diff --staged                   # see staged changes
git show a1b2c3d                    # full detail of one commit
git blame hello.txt                 # who wrote which line
git shortlog -sn                    # commits count per author
```

---
[← Back to index](README.md)

jharana
