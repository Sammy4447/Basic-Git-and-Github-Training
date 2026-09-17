# Git Command Cheatsheet

A quick reference for commands covered in the labs. For detailed explanations, see the corresponding lab.

## Setup (One Time)

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --list                          # verify settings
```

## Initialize & Clone

```bash
git init                                   # start version control in current folder
git clone <url>                            # copy a remote repo to your machine
```

## Check Status

```bash
git status                                 # what changed?
git log                                    # commit history
git log --oneline                          # compact history
git log --oneline --decorate --graph       # visual history with branches
git show <commit-hash>                     # full details of one commit
```

## Staging & Committing

```bash
git add <file>                             # stage one file
git add .                                  # stage all changes
git status                                 # verify what's staged
git commit -m "message"                    # save staged changes
git commit -am "message"                   # stage & commit in one (modified files only)
```

## Viewing Changes

```bash
git diff                                   # unstaged changes
git diff --staged                          # staged changes (before commit)
git diff main feature-branch               # compare two branches
git diff --stat                            # summary of changed files
git diff --name-only                       # list of changed files
```

## Branches

```bash
git branch                                 # list local branches
git branch -a                              # list all branches (local + remote)
git checkout -b <branch-name>              # create and switch to new branch
git checkout <branch-name>                 # switch to existing branch
git branch -d <branch-name>                # delete branch (safe — won't delete unmerged)
git branch -D <branch-name>                # force delete branch
git merge <branch-name>                    # merge another branch into current branch
```

## Undoing Changes

```bash
git restore <file>                         # discard changes in working directory
git restore --staged <file>                # unstage a file
git reset HEAD~1                           # undo last commit (keep changes)
git reset --hard HEAD~1                    # undo last commit (discard changes)
git revert <commit-hash>                   # create new commit that undoes old commit
git checkout <commit-hash> -- <file>       # restore file to specific commit
```

## Stashing (Temporary Storage)

```bash
git stash                                  # save uncommitted work
git stash list                             # see all stashed work
git stash pop                              # restore last stashed work (remove from stash)
git stash apply                            # restore last stashed work (keep in stash)
git stash drop                             # delete stashed work
```

## Cherry Pick (One Commit from Another Branch)

```bash
git cherry-pick <commit-hash>              # apply specific commit to current branch
```

## Tags & Releases

```bash
git tag <tag-name>                         # create lightweight tag
git tag -a <tag-name> -m "message"        # create annotated tag with message
git tag                                    # list all tags
git show <tag-name>                        # show tag details
git push origin <tag-name>                 # push tag to GitHub
git push origin --tags                     # push all tags to GitHub
```

## Remote & GitHub

```bash
git remote -v                              # see remote URLs
git fetch                                  # update local refs from remote
git pull                                   # fetch + merge remote changes
git push                                   # push local commits to remote
git push origin <branch-name>              # push specific branch
git push -u origin <branch-name>           # push and set upstream (for first push)
```

## Inspection & Utilities

```bash
git blame <file>                           # who wrote which line?
git shortlog -sn                           # commits per contributor
git log --stat -1                          # files changed in latest commit
git diff <file1> <file2>                   # compare two files
```

## Common Workflows

### Starting a New Feature
```bash
git checkout -b feature/login              # create feature branch
# ... make changes and commits ...
git checkout main                          # switch to main
git merge feature/login                    # merge feature into main
```

### Fixing an Urgent Bug While Working on Feature
```bash
git stash                                  # save feature work
git checkout main                          # go to main
git checkout -b hotfix/critical            # create hotfix branch
# ... fix and commit ...
git checkout main
git merge hotfix/critical
git checkout feature/login
git stash pop                              # resume feature work
```

### Undoing the Last Commit
```bash
git reset HEAD~1                           # keep changes, undo commit
git reset --hard HEAD~1                    # discard everything
```

### Viewing History Before Pushing
```bash
git log origin/main..HEAD                  # commits not yet pushed
git log --oneline --graph -10              # visual history of last 10 commits
```

---

**Want details on any command?** See the corresponding lab in [README.md](README.md)

