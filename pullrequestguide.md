# Complete Pull Request (PR) Guide

[← Back to index](README.md)

A **Pull Request (PR)** is a way to propose changes from your branch (or fork) into another repository branch (typically `main`). It provides a collaborative space for code review, discussion, automated testing (CI), and approval before code is merged.

---

## Table of Contents

1. [Workflows: Feature Branch vs. Fork](#1-workflows-feature-branch-vs-fork)
2. [Step-by-Step: Creating a Pull Request](#2-step-by-step-creating-a-pull-request)
   - [Step 1: Get the Latest Changes](#step-1-get-the-latest-changes)
   - [Step 2: Create a Dedicated Branch](#step-2-create-a-dedicated-branch)
   - [Step 3: Make Changes & Test](#step-3-make-changes--test)
   - [Step 4: Stage & Commit](#step-4-stage--commit)
   - [Step 5: Push Your Branch to GitHub](#step-5-push-your-branch-to-github)
   - [Step 6: Open the Pull Request on GitHub](#step-6-open-the-pull-request-on-github)
3. [Step-by-Step: Addressing Feedback & Updating Your PR](#3-step-by-step-addressing-feedback--updating-your-pr)
4. [Step-by-Step: Merging & Cleanup](#4-step-by-step-merging--cleanup)
5. [Pull Request Description Template](#5-pull-request-description-template)
6. [Resolving Conflicts Before/During PR](#6-resolving-conflicts-beforeduring-pr)
7. [PR Quick Reference & Best Practices](#7-pr-quick-reference--best-practices)

---

## 1. Workflows: Feature Branch vs. Fork

Depending on your access level, you will use one of two workflows:

| Workflow | When to Use | How it Works |
|---|---|---|
| **Feature Branch Workflow** | You are a member/collaborator of the repo (e.g., in a company or team project). | You clone the repo directly, push a feature branch to the same repository, and create a PR to `main`. |
| **Fork & Pull Workflow** | You are contributing to public/open-source repos where you don't have write access. | You fork the repo to your own GitHub account, clone your fork, push branches there, and open a PR across repositories. |

---

## 2. Step-by-Step: Creating a Pull Request

### Step 1: Get the Latest Changes

Always start from an up-to-date `main` branch to avoid merge conflicts later.

```bash
git checkout main
git pull origin main
```

*(If working on a fork, ensure your local main is synced with the original upstream repo)*:
```bash
git remote add upstream https://github.com/original-owner/repo-name.git  # only needed once
git fetch upstream
git merge upstream/main
```

---

### Step 2: Create a Dedicated Branch

Never commit directly to `main`. Use a descriptive branch prefix (e.g., `feat/`, `fix/`, `docs/`, `refactor/`).

```bash
# Format: git checkout -b <type>/<short-description>
git checkout -b feat/add-user-auth
```

---

### Step 3: Make Changes & Test

1. Edit, add, or delete files in VS Code.
2. Test your changes locally to ensure nothing is broken.
3. Check what was modified:

```bash
git status
git diff
```

---

### Step 4: Stage & Commit

Group your changes into logical, well-described commits.

```bash
# Stage specific files (recommended) or all changes
git add src/auth.js

# Write a clear, concise commit message
git commit -m "feat: implement JWT token authentication"
```

> **Tip (Conventional Commits):**
> - `feat:` new feature
> - `fix:` bug fix
> - `docs:` documentation changes
> - `style:` formatting, missing semicolons (no code logic changes)
> - `refactor:` code restructuring without changing behavior
> - `test:` adding or modifying tests

---

### Step 5: Push Your Branch to GitHub

Upload your branch to the remote repository.

```bash
# Push and set upstream tracking (-u)
git push -u origin feat/add-user-auth
```

---

### Step 6: Open the Pull Request on GitHub

1. Navigate to the repository on GitHub in your browser.
2. You will usually see a gold banner: **`feat/add-user-auth had recent pushes. [Compare & pull request]`** — click it!
3. If the banner is not visible:
   - Click the **Pull requests** tab.
   - Click **New pull request**.
   - Set **Base** to `main` (the destination) and **Compare** to `feat/add-user-auth` (your branch).
4. Fill in:
   - **Title**: A clear summary (e.g., `feat: Add JWT authentication for login`).
   - **Description**: Explain *what* was changed and *why*.
   - **Reviewers / Assignees**: Tag teammates if applicable.
5. Click **Create pull request**.

---

## 3. Step-by-Step: Addressing Feedback & Updating Your PR

Code review is a normal, healthy part of development! When a reviewer asks for changes:

1. You **do not** need to close the PR or create a new one.
2. Simply switch to your branch locally, make the edits, and commit:

```bash
git checkout feat/add-user-auth

# Make edits...
git add .
git commit -m "refactor: address review feedback on token expiration"

# Push the new commit
git push origin feat/add-user-auth
```

GitHub will automatically update the open Pull Request with your new commits.

---

## 4. Step-by-Step: Merging & Cleanup

Once all checks pass and reviewers approve:

1. **Merge on GitHub**: Click **Merge pull request** (or *Squash and merge* / *Rebase and merge* depending on team conventions).
2. **Delete the remote branch**: Click the **Delete branch** button on GitHub.
3. **Clean up your local machine**:

```bash
# Switch back to main and update it
git checkout main
git pull origin main

# Delete the local branch
git branch -d feat/add-user-auth

# Prune remote branch references
git remote prune origin
```

---

## 5. Pull Request Description Template

Copy and paste this markdown template into your PR description on GitHub:

```markdown
## 📌 Summary
A concise description of the problem this PR solves or the feature it introduces.

## 🛠️ Changes Made
- Added JWT authentication middleware in `src/auth.js`
- Created user login route in `routes/user.js`
- Added unit tests for invalid token handling

## 🧪 How to Test
1. Run `npm test` to verify all test suites pass.
2. Start the dev server (`npm start`) and send a POST request to `/api/login`.
3. Verify that a valid token is returned in the response header.

## 📸 Screenshots / Demos (if applicable)
*(Attach before/after screenshots, GIFs, or CLI outputs here)*

## 🔗 Related Issues
Closes #123
```

---

## 6. Resolving Conflicts Before/During PR

If changes were merged to `main` while you were working on your branch, GitHub may show **"This branch has conflicts that must be resolved"**.

### Method 1: Rebase on `main` (Recommended for clean history)
```bash
git checkout feat/add-user-auth
git fetch origin
git rebase origin/main

# If conflicts occur:
# 1. Open conflicted files in VS Code and resolve markers (<<<<<<<, =======, >>>>>>>)
# 2. Stage resolved files:
git add <resolved-file>
# 3. Continue rebase:
git rebase --continue

# Force-push with lease after rebase
git push --force-with-lease origin feat/add-user-auth
```

### Method 2: Merge `main` into your branch
```bash
git checkout feat/add-user-auth
git fetch origin
git merge origin/main

# Resolve any conflict markers in VS Code, then:
git add .
git commit -m "Merge branch 'main' into feat/add-user-auth"
git push origin feat/add-user-auth
```

---

## 7. PR Quick Reference & Best Practices

### Cheat Sheet

| Action | Command |
|---|---|
| Start from main | `git checkout main && git pull origin main` |
| Create branch | `git checkout -b <branch-name>` |
| Check status & diff | `git status` / `git diff` |
| Stage changes | `git add <files>` |
| Commit | `git commit -m "<message>"` |
| Push to GitHub | `git push -u origin <branch-name>` |
| Push updates to PR | `git push origin <branch-name>` |
| Delete local branch | `git branch -d <branch-name>` |

### 5 Rules for Great Pull Requests

1. **Keep PRs small**: Smaller PRs (under 300 lines) are reviewed 3x faster and with higher quality.
2. **One feature per PR**: Don't combine unrelated bug fixes or refactors into one PR.
3. **Self-review first**: Check your own `Files changed` tab on GitHub before requesting review.
4. **Write descriptive titles & bodies**: Help the reviewer understand context without having to guess.
5. **Keep branch synced**: Regularly pull or rebase from `main` to prevent big merge conflicts.
