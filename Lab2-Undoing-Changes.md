# Lab 2 — Undoing Changes

[← Back to index](README.md)

Git has four different "undo" commands and picking the wrong one is how people lose work. Use this table to choose:

| Your situation | Command | What survives |
|---|---|---|
| Edited a file, not committed yet, want the old version back | `git restore <file>` | Your edits are **gone** |
| Staged a file (`git add`) by mistake, not committed yet, want it unstaged | `git restore --staged <file>` | Your edits stay, just unstaged |
| Bad commit already pushed to GitHub / shared with teammates | `git revert HEAD` | Everything — history is kept, a new commit undoes it |
| Committed too early, want to fix the message or add a file | `git reset --soft HEAD~1` | Your changes, still staged |
| Commit is garbage and nobody else has it | `git reset --hard HEAD~1` | Nothing — commit **and** changes are gone |

> *Step 10 — Reset Soft (reset --soft)

Use it when: you made a commit too early, but the changes are still correct. Maybe you forgot a file, made a typo in the commit message, or want to combine commits into one.
Real example: you committed as "fix", then realised you forgot to include config.js. git reset --soft HEAD~1 removes the commit but keeps your changes staged, so you can add the missing file and commit everything properly.
Only if: you have not pushed that commit yet.

In VSCode — open hello.txt, add a line:

Hello Git
I am learning Git
Git is a version control system
accidental line


Save — Ctrl + S

Terminal:

git add .
git commit -m "temporary commit"
git log --oneline         # see the commit at the top

git reset --soft HEAD~1   # remove the commit, keep changes staged
git status                # changes are still staged

git commit -m "proper commit"

```bash
git add .
git commit -m "accidental commit"
git log --oneline             # see it at top

git reset --soft HEAD~1       # commit gone, changes still staged
git status                    # file still green (staged)
git log --oneline             # commit is gone ✅
```

## Step 11 — Reset Hard (reset --hard)

> **Use it when:** you want the commit **and** the work in it completely gone — a failed experiment, debug code you committed by mistake, a branch you want back to a clean state.
> **This is the destructive one.** It deletes your files' changes with no undo. Before running it, ask two questions: *Have I pushed this?* (if yes → use `revert`) and *Do I want any of this work?* (if maybe → use `git stash` or `reset --soft`).

In VSCode — open `hello.txt`, add a line:

```
Hello Git
I am learning Git
Git is a version control system
delete everything including this
```

Save — `Ctrl + S`

Terminal:

```bash
git add .
git commit -m "commit to destroy"
git log --oneline

git reset --hard HEAD~1       # commit gone + file changes gone
git log --oneline             # commit removed ✅
```

Open `hello.txt` in VSCode — the line is completely gone ✅

---
Next: [Lab 3 — GitHub Basics](Lab3-GitHub-Basics.md)