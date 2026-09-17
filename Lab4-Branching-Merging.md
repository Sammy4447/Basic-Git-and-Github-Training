# Lab 4 — Branching & Merging

[← Back to index](README.md)

## Step 16 — Create a Branch

> _“Creating a branch is just opening a new timeline in the multiverse.”_
> **Use it when:** you're about to start a new feature, a bug fix, or an experiment and you don't want half-finished work sitting on `main`. A branch is a private lane — you can commit freely, and `main` stays working the whole time.
> **Naming:** teams usually use `feature/...`, `bugfix/...`, `hotfix/...` so the branch name says what it's for.

Terminal:

```bash
git branch                          # see current branches
git checkout -b feature/login       # create and switch
git branch                          # confirm you are on new branch
```

## Step 17 — Work on Branch & Commit

> **Use it when:** you're on your branch and building. Commit as often as you like here — these commits are yours alone until you merge or push, so nobody sees the messy middle.

In VSCode — right click → New File → `login.txt`

Type inside `login.txt`:

```
This is the login page
```

Save — `Ctrl + S`

Terminal:

```bash
git add .
git commit -m "add login page"
```

## Step 18 — Merge Branch into Main

> **Use it when:** the feature is finished and tested, and you want it in `main` for everyone.
> **Order matters:** always `git checkout` the branch you want to merge _into_ first (here, `main`), then `git merge <the-other-branch>`. Doing it backwards merges main into your feature instead.
> **On a team:** you'd usually push the branch and open a Pull Request on GitHub rather than merging locally — same idea, but with review.

Terminal:

```bash
git checkout main
ls                              # login.txt not here
git merge feature/login
ls                              # login.txt is here now ✅
git log --oneline --graph --all
```

## Step 19 — Create a Merge Conflict

> **Why practise this:** a conflict happens whenever two branches changed the _same lines_ of the _same file_. It is normal, not a bug or a mistake — every developer hits it. Better to meet it here, on a throwaway file, than the first time on real work.

Terminal:

```bash
git checkout -b feature/conflict
```

In VSCode — open `hello.txt`, change first line to:

```
Hello from feature branch
I am learning Git
Git is a version control system
```

Save — `Ctrl + S`

Terminal:

```bash
git add .
git commit -m "feature branch change"
git checkout main
```

In VSCode — open `hello.txt`, change first line to:

```
Hello from main branch
I am learning Git
Git is a version control system
```

Save — `Ctrl + S`

Terminal:

```bash
git add .
git commit -m "main branch change"
git merge feature/conflict          # conflict will appear
```

## Step 20 — Resolve the Conflict

> **Use it when:** a merge or pull stops with "CONFLICT" and Git asks you to decide. Git can't know which version is right, so it puts both in the file and hands it to you.
> **How to read the markers:** everything between `<<<<<<< HEAD` and `=======` is _your current branch_; between `=======` and `>>>>>>>` is _the branch coming in_. Keep one, keep the other, or write a combination — then delete all three marker lines, save, `git add`, `git commit`.
> **VSCode shortcut:** it shows "Accept Current / Accept Incoming / Accept Both" buttons above the conflict — clicking those does the same thing.
> **Panicking?** `git merge --abort` puts everything back the way it was before the merge.

In VSCode — open `hello.txt`, you will see:

```
<<<<<<< HEAD
Hello from main branch
=======
Hello from feature branch
>>>>>>> feature/conflict
```

Delete the conflict markers, keep what you want:

```
Hello from main branch
I am learning Git
Git is a version control system
```

Save — `Ctrl + S`

Terminal:

```bash
git add .
git commit -m "conflict resolved"
git log --oneline --graph --all
```

## Step 21 — Delete a Branch

> **Use it when:** the branch is merged and you're done with it. Old branches pile up fast and make `git branch` unreadable.
> **Safe vs forced:** `-d` refuses to delete a branch that hasn't been merged — that refusal is a safety net protecting unmerged work. `-D` forces it, so only use `-D` when you're sure you want to throw that work away.

Terminal:

```bash
git branch -d feature/login         # safe delete
git branch -d feature/conflict      # safe delete
git branch                          # confirm deleted ✅
```

## Bonus command — Switch Between Branches with `git switch`

> **Use it when:** you want to move between branches. `git switch` is the modern, branch-focused alternative to using `git checkout`.

```bash
git branch                         # see all branches
git switch main                    # switch to an existing branch
git switch feature/login           # switch to feature/login
git switch -c feature/dashboard    # create + switch to a new branch
git branch                         # confirm current branch
git status                         # check current branch
```

`git switch <branch>` switches to an existing branch.

`git switch -c <branch>` creates a new branch and switches to it.

For example:

```bash
git switch main
git switch -c feature/profile
git switch main
git switch feature/profile
```

> **Remember:** `git checkout -b feature/login` and `git switch -c feature/login` both create and switch to a new branch, but `git switch` is clearer because it is specifically designed for branch switching.

> **Tip:** Run `git status` before switching if you have uncommitted changes, so you know what work is currently in your working tree.

---

Next: [Lab 5 — Advanced Commands](Lab5-Advanced-Commands.md)
