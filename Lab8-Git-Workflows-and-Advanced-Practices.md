# Lab 8 — Working with Git Worktrees

[← Back to index](README.md)

## Step 29 — Open a second working directory

> **Use it when:** you need to work on another branch or fix a bug without disturbing the current branch state.
>
> - `git worktree add <path> -b <branch>` — creates a second checkout linked to the same repository.
> - `git worktree list` — shows all worktrees connected to the repo.
> - `git worktree remove <path>` — deletes a worktree when you are done.

Terminal:

```bash
git worktree add ../project-hotfix -b hotfix
cd ../project-hotfix
git worktree list
```

> This is helpful when you want to keep your current work untouched while testing a fix or reviewing another branch in parallel.

---

## Step 30 — Keep both branches active at once

> **Use it when:** you want to compare code, fix a bug, or review two branches side by side without switching and losing context.
>
> - `git status` — confirm which worktree you are in.
> - `git branch` — check the branch in each checkout.
> - `git worktree remove <path>` — clean up when finished.

Terminal:

```bash
cd ../project-hotfix
git status
git branch
cd ../Basic-Git-and-Github-Training
git status
git worktree remove ../project-hotfix
```

> Worktrees are especially useful for large projects where you want multiple independent workspaces without cloning the repo again.

---

This topic is newer and practical in real repositories: `git worktree` lets you work on more than one branch at the same time without disturbing the current checkout.

[← Back to index](README.md)
