# Lab 9 — Pull Requests

[← Back to index](README.md)

## Step 32 — Create a Branch for Your Change

> **Use it when:** always — before you edit a single line for a contribution. Never work directly on `main` in a fork. A separate branch per change keeps your `main` clean for syncing, and lets you have more than one PR open at a time.
> **Naming:** short and descriptive — `fix/typo-in-lab3`, `feat/add-stash-example`, `docs/clarify-rebase`.

Terminal:

```bash
git checkout main
git fetch upstream                  # start from the latest code
git merge upstream/main
git checkout -b fix/typo-in-lab3    # create + switch to your branch
```

## Step 33 — Commit and Push to Your Fork

> **Use it when:** your change is done and you've reviewed it. Push goes to `origin` (your fork) — you have no write access to `upstream`, and that's fine; GitHub picks the branch up from your fork.
> **Before you commit:** run `git diff` and read your own change (see [Step 28](Lab7-Inspection-Utilities.md)). A PR with a stray debug line is the most common review comment there is.

In VSCode — make your edit and save with `Ctrl + S`.

Terminal:

```bash
git diff                            # review your own change
git add .
git commit -m "docs: fix typo in Lab 3"
git push origin fix/typo-in-lab3    # push the branch to YOUR fork ✅
```

The output prints a GitHub link to open a pull request — you can click it, or use the steps below.

## Step 34 — Open the Pull Request

> **Use it when:** your branch is pushed and you want the original project to take your change. A **pull request** is a request to the maintainer: "please pull these commits from my branch into yours." It's a conversation, not a command — they can comment, ask for changes, and merge when happy.
> **Direction matters:** base = the original repo's `main` (where it's going). compare = your fork's branch (where it's coming from). Getting these backwards is the classic first-PR mistake.

On GitHub:

```
1. Open your fork — a "Compare & pull request" banner appears
2. Click it (or go to Pull requests → New pull request)
3. Check the direction:
     base repository: <original-owner>/<repo>   base: main
     compare:         <your-username>/<repo>    compare: fix/typo-in-lab3
4. Write a title and description — what changed, and why
5. Click Create pull request ✅
```

A good description answers three things: **what** you changed, **why** it was needed, and **how** you tested it (if it's code).

## Step 35 — Update a PR After Review Feedback

> **Use it when:** the maintainer asks for changes. You do **not** open a new PR. A pull request tracks a *branch* — every new commit you push to that same branch appears in the existing PR automatically.
> **Why this surprises people:** there's no "resubmit" button. Just commit and push again, and refresh the PR page.

Terminal:

```bash
git checkout fix/typo-in-lab3       # make sure you're on the PR branch
# ...make the requested edits, save...
git add .
git commit -m "docs: address review feedback"
git push origin fix/typo-in-lab3    # the open PR updates itself ✅
```

If `main` moved ahead while your PR was waiting and GitHub says "This branch has conflicts":

```bash
git fetch upstream
git rebase upstream/main            # replay your commits on the latest main
# ...fix any conflicts, then:
git rebase --continue
git push origin fix/typo-in-lab3 --force-with-lease
```

> **Why `--force-with-lease`:** a rebase rewrites your commits into new ones ([Step 24](Lab5-Advanced-Commands.md)), so a normal push is rejected. `--force-with-lease` overwrites your branch but refuses if someone else pushed to it meanwhile — safer than plain `--force`.

## Step 36 — After the Merge

> **Use it when:** the PR is merged 🎉. Clean up so your next contribution starts from a tidy state.

Terminal:

```bash
git checkout main
git fetch upstream
git merge upstream/main             # your change is now in main
git push origin main                # sync your fork
git branch -d fix/typo-in-lab3      # delete the local branch
git push origin --delete fix/typo-in-lab3   # delete it on your fork
```

## Cheat sheet — the whole flow

| Step | Command / action |
|---|---|
| Fork | GitHub → **Fork** button |
| Clone your fork | `git clone <your-fork-url>` |
| Add upstream | `git remote add upstream <original-repo-url>` |
| Sync before starting | `git fetch upstream && git merge upstream/main` |
| New branch | `git checkout -b <branch-name>` |
| Review your change | `git status` / `git diff` |
| Stage | `git add <file>` |
| Commit | `git commit -m "message"` |
| Push to your fork | `git push origin <branch-name>` |
| Open PR | GitHub → **Compare & pull request** button |
| Update the PR | commit + `git push origin <branch-name>` again |
| Clean up after merge | `git branch -d <branch-name>` |

### Three habits worth keeping

1. **One small change per PR** — easier to review, faster to merge.
2. **Clear commit messages and a real description** — the reviewer shouldn't have to guess your intent.
3. **Sync before you open it** — `git fetch upstream && git merge upstream/main` avoids conflicts showing up in the PR.

> **Rule of thumb for the whole flow:** fork once → sync before you start → branch → commit → push to your fork → open PR → push more commits to the same branch until it's merged → clean up.

---

[← Back to index](README.md)
