# Lab 8 — Everyday Workflow & Troubleshooting

[← Back to index](README.md)

This capstone lab combines the earlier commands into the workflow you will use for a real change: update your local copy, create a branch, inspect the work, commit it, push it, and respond to review.

## Step 29 — Start from a clean, current branch

> **Use it when:** you are beginning work for the day or starting a new feature, fix, or documentation change.
> **Why it matters:** checking first prevents you from accidentally mixing old work with a new change. `--ff-only` refuses to create an unexpected merge commit while updating `main`.

Terminal:

```bash
git status
git switch main
git pull --ff-only origin main
git switch -c docs/my-change
```

If `git status` shows uncommitted work, stop and decide whether to commit it, stash it, or discard it before switching branches. If the project has no remote yet, skip the `git pull` command.

## Step 30 — Make the change and inspect it

Edit the file or files needed for one small piece of work. Then review the result before staging anything:

```bash
git status
git diff
git diff --check
```

`git diff --check` reports common whitespace mistakes. Stage only the files that belong to this change, then inspect the staged version:

```bash
git add <file-name>
git diff --staged
```

Using an explicit filename makes it harder to include a temporary file, credential, or unrelated change by mistake. Use `git add .` only after `git status` confirms that every listed file belongs in the commit.

## Step 31 — Create a useful commit

A commit message should describe the result, not the time spent working on it.

```bash
git commit -m "docs: improve the contributor workflow"
git log --oneline --decorate -3
```

Good examples:

```text
docs: add troubleshooting guide
fix: correct repository badge links
feat: add release instructions
```

Keep each commit focused. A reviewer should be able to explain what the commit changes after reading its message and diff.

## Step 32 — Push the branch and open a pull request

Push the branch to your fork or to the shared repository, depending on your access:

```bash
git push -u origin docs/my-change
```

On GitHub, open a pull request and include:

- what changed;
- why the change is useful;
- how you checked it;
- screenshots or examples when the change affects presentation.

For the full fork-to-pull-request process, see [How to Create a Pull Request](HOW_TO_CREATE_A_PR.md).

## Keep a pull request current

If `main` changes while your pull request is open, update your branch deliberately:

```bash
git fetch origin
git switch main
git pull --ff-only origin main
git switch docs/my-change
git merge main
git push
```

Run the checks again after the merge. If the project asks contributors to rebase instead, use the project’s instructions. Do not rebase a branch that other people are already using without agreeing first.

## Common problems and safe responses

| Situation | What to do | Avoid |
|---|---|---|
| `nothing to commit` | Run `git status`, save the file, and confirm you are on the intended branch. | Creating an empty commit just to make the message disappear. |
| `rejected — non-fast-forward` | Run `git fetch origin`, update your branch with the project’s chosen merge or rebase process, resolve conflicts if needed, then push again. | Force-pushing a shared branch. |
| A file was staged by mistake | Run `git restore --staged <file-name>`. Your edits remain in the working directory. | Deleting the file or using a hard reset. |
| You need to pause unfinished work | Run `git stash push -m "work in progress"`, do the other task, then run `git stash pop`. | Switching branches without checking whether your edits will follow you. |
| A merge conflict appears | Run `git status`, edit the conflict markers, `git add <resolved-file>`, and commit. | Leaving `<<<<<<<`, `=======`, or `>>>>>>>` in the file. |
| You want to cancel an unfinished merge | Run `git merge --abort` before making further edits. | Running `git reset --hard` without confirming what it will remove. |
| You are in detached HEAD state | If the work matters, preserve it with `git switch -c rescue/my-work`; otherwise switch back to the required branch. | Continuing to make commits without creating a branch. |
| A password, token, or key was committed | Stop sharing it, revoke or rotate it immediately, and tell the repository maintainer. Remove the secret from the project only after it is invalidated. | Relying on `.gitignore` to erase a secret that is already in Git history. |

## A five-minute pre-push check

```bash
git status
git diff --check
git diff --staged
git log --oneline --decorate -3
git push
```

Before any destructive command, make sure you know which branch you are on and whether the commit has been pushed. If you are unsure, make a safety branch first:

```bash
git branch safety-copy
```

Once this workflow feels familiar, the earlier labs become individual tools you can choose with confidence rather than commands to memorise.

---

[← Back to index](README.md)
