# Lab 1 — Initial Setup & First Commits

[← Back to index](README.md)

## Definitions

- Repository: A project folder tracked by Git.
- Commit: A saved snapshot of your project.
- Working directory: The files currently on your machine.
- Staging area: The prepared changes before a commit.
- Branch: A separate line of development.
- Remote: The GitHub version of the repository.

## Step 1 — Configure Git (One Time Only)

> **Use it when:** you just installed Git on a new laptop and haven't committed anything yet.
> **Why it matters:** Git stamps your name and email on every commit. Skip this and your commits show up as `unknown`, or Git refuses to commit at all. Do it once per machine.

Terminal:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@email.com"
git config --list
```

## Step 2 — Create Project & Initialize

> **Use it when:** you're starting a brand new project on your own machine and want version control from day one.
> **Don't use it when:** the project already came from GitHub — in that case you `git clone` instead (Step 14). Running `git init` inside an already-cloned repo is not needed.

Terminal:

```bash
mkdir my-project
cd my-project
git init
```

## Step 3 — Open in VSCode

> **Use it when:** you want to edit files and run Git commands in the same window instead of switching between a file manager and a separate terminal.

File → Open Folder → select `my-project`

Then open terminal inside VSCode:

```
Ctrl + `
```

## Step 4 — First Commit

> **Use it when:** you've written something you want to keep — a working file, a finished section, a fix. A commit is a save point you can always come back to.
> **Rule of thumb:** `git status` first (what changed?), `git add` next (which changes do I want to save?), `git commit` last (save them with a message).

In VSCode — right click in Explorer panel → New File → name it `hello.txt`

Type inside `hello.txt`:

```
Hello Git
```

Save — `Ctrl + S`

Terminal:

```bash
git status
git add .
git commit -m "first commit"
```

## Step 5 — Second Commit

> **Use it when:** you've made the next meaningful change. Commit small and often — one logical change per commit — so that undoing later (Lab 2) removes only what you meant to remove.

In VSCode — open `hello.txt`, add a new line:

```
Hello Git
I am learning Git
```

Save — `Ctrl + S`

Terminal:

```bash
git status
git add .
git commit -m "second commit"
```

## Step 6 — Third Commit

> **Use it when:** same as above — you're building a history. By now you should have three save points, which is exactly what you need to practise undoing things.

In VSCode — open `hello.txt`, add one more line:

```
Hello Git
I am learning Git
Git is a version control system
```

Save — `Ctrl + S`

Terminal:

```bash
git status
git add .
git commit -m "third commit"
```
i anm learning pull request
## Step 7 — View History

> **Use it when:** you want to know what happened in this project — who changed what, when, and in what order. Also how you find a commit hash to use with `revert`, `cherry-pick`, or `show`.
> **Which one:**
> - `git log` — full detail: author, date, full message.
> - `git log --oneline` — one line per commit; best for quickly grabbing a hash.
> - `git log --oneline --graph --all` — draws the branch structure; use it when branches and merges are involved (Lab 4).

Terminal:

```bash
git log
git log --oneline
git log --oneline --graph --all
```

---
Next: [Lab 2 — Undoing Changes](Lab2-Undoing-Changes.md)
