# Git & GitHub — Command Cheat Sheet

[← Back to index](README.md)

Every command taught across the 7 labs, grouped by purpose. The "Lab" column tells you where to find the full hands-on walkthrough.

## Configuration & Setup

| Command | What it does | Lab |
|---|---|---|
| `git config --global user.name "Your Name"` | Set your name (one time per machine) | [1](Lab1-Initial-Setup-First-Commits.md) |
| `git config --global user.email "you@example.com"` | Set your email (one time per machine) | [1](Lab1-Initial-Setup-First-Commits.md) |
| `git config --list` | See your saved Git settings | [1](Lab1-Initial-Setup-First-Commits.md) |
| `git init` | Turn the current folder into a repo (new project) | [1](Lab1-Initial-Setup-First-Commits.md) |
| `git clone <url>` | Copy an existing remote repo to your machine | [3](Lab3-GitHub-Basics.md) |
| `.gitignore` | Files/folders Git must not track or upload | [1](Lab1-Initial-Setup-First-Commits.md) |

## Daily Workflow (status → add → commit)

| Command | What it does | Lab |
|---|---|---|
| `git status` | What changed, what is staged | [1](Lab1-Initial-Setup-First-Commits.md) |
| `git add .` | Stage all changes | [1](Lab1-Initial-Setup-First-Commits.md) |
| `git commit -m "message"` | Save staged changes with a message | [1](Lab1-Initial-Setup-First-Commits.md) |

## Inspecting History & Diffs

| Command | What it does | Lab |
|---|---|---|
| `git log` | Full history — author, date, message | [1](Lab1-Initial-Setup-First-Commits.md) |
| `git log --oneline` | One line per commit; grab a hash fast | [1](Lab1-Initial-Setup-First-Commits.md) |
| `git log --oneline --graph --all` | Draw the branch structure | [1](Lab1-Initial-Setup-First-Commits.md) |
| `git log --stat -1` | Files changed in the latest commit | [7](Lab7-Inspection-Utilities.md) |
| `git log --oneline --decorate --graph -5` | Recent history with branch pointers | [7](Lab7-Inspection-Utilities.md) |
| `git diff` | Unstaged changes | [7](Lab7-Inspection-Utilities.md) |
| `git diff --stat` | Which files changed and by how much | [7](Lab7-Inspection-Utilities.md) |
| `git diff --name-only` | Just the list of changed files | [7](Lab7-Inspection-Utilities.md) |
| `git diff --staged` | What you are about to commit | [7](Lab7-Inspection-Utilities.md) |
| `git diff <commit1> <commit2>` | Changes between two commits or branches | [7](Lab7-Inspection-Utilities.md) |
| `git show <hash>` | What exactly one commit changed | [7](Lab7-Inspection-Utilities.md) |
| `git blame <file>` | Who wrote each line, and in which commit | [7](Lab7-Inspection-Utilities.md) |
| `git shortlog -sn` | Commit counts per author | [7](Lab7-Inspection-Utilities.md) |

## Undoing Changes

| Command | What it does | Lab |
|---|---|---|
| `git restore <file>` | Discard unstaged edits (gone forever) | [2](Lab2-Undoing-Changes.md) |
| `git restore --staged <file>` | Unstage a file, keep your edits | [2](Lab2-Undoing-Changes.md) |
| `git revert HEAD` | Safe undo of a pushed commit — adds a new commit | [2](Lab2-Undoing-Changes.md) |
| `git reset --soft HEAD~1` | Remove the last commit, changes stay staged | [2](Lab2-Undoing-Changes.md) |
| `git reset --hard HEAD~1` | Remove the last commit AND its changes | [2](Lab2-Undoing-Changes.md) |
| `git merge --abort` | Cancel a conflicting merge, back to square one | [4](Lab4-Branching-Merging.md) |

## Branching & Merging

| Command | What it does | Lab |
|---|---|---|
| `git branch` | List branches (current one marked) | [4](Lab4-Branching-Merging.md) |
| `git checkout -b <name>` | Create + switch to a branch | [4](Lab4-Branching-Merging.md) |
| `git switch <name>` | Modern way to switch branches | [4](Lab4-Branching-Merging.md) |
| `git switch -c <name>` | Modern create + switch | [4](Lab4-Branching-Merging.md) |
| `git checkout main` | Switch back to main before merging | [4](Lab4-Branching-Merging.md) |
| `git merge <branch>` | Merge a branch into the current one | [4](Lab4-Branching-Merging.md) |
| `git branch -d <name>` | Delete a merged branch (safe) | [4](Lab4-Branching-Merging.md) |
| `git branch -D <name>` | Force-delete an unmerged branch | [4](Lab4-Branching-Merging.md) |

## GitHub & Remotes

| Command | What it does | Lab |
|---|---|---|
| `git remote add origin <url>` | Connect your repo to GitHub | [3](Lab3-GitHub-Basics.md) |
| `git remote -v` | Show configured remotes | [3](Lab3-GitHub-Basics.md) |
| `git remote set-url origin <url>` | Point at a different remote | [3](Lab3-GitHub-Basics.md) |
| `git push -u origin main` | First push — links local `main` to `origin/main` | [3](Lab3-GitHub-Basics.md) |
| `git push` | Push commits once `-u` is set | [3](Lab3-GitHub-Basics.md) |
| `git pull origin main` | Download + merge remote changes | [3](Lab3-GitHub-Basics.md) |
| `ssh -T git@github.com` | Test your SSH connection to GitHub | [3](Lab3-GitHub-Basics.md) |

## Advanced — Stash, Cherry-Pick, Rebase

| Command | What it does | Lab |
|---|---|---|
| `git stash` | Save work in progress, clean the tree | [5](Lab5-Advanced-Commands.md) |
| `git stash list` | See saved stashes | [5](Lab5-Advanced-Commands.md) |
| `git stash pop` | Restore the latest stash and remove it | [5](Lab5-Advanced-Commands.md) |
| `git stash apply` | Restore the latest stash but keep a copy | [5](Lab5-Advanced-Commands.md) |
| `git cherry-pick <hash>` | Apply one specific commit from another branch | [5](Lab5-Advanced-Commands.md) |
| `git rebase <branch>` | Replay your commits on top of another branch | [5](Lab5-Advanced-Commands.md) |

## Tags & Releases

| Command | What it does | Lab |
|---|---|---|
| `git tag` | List tags | [6](Lab6-Tags-Releases.md) |
| `git tag -a v1.0.0 -m "message"` | Create an annotated tag | [6](Lab6-Tags-Releases.md) |
| `git push origin --tags` | Push tags to GitHub | [6](Lab6-Tags-Releases.md) |
| `git tag -d v1.0.0` | Delete a tag locally | [6](Lab6-Tags-Releases.md) |
| `git push origin --delete v1.0.0` | Delete a tag on GitHub | [6](Lab6-Tags-Releases.md) |

---

[← Back to index](README.md)