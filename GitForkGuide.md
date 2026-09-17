# How to Create a Pull Request (PR)

This guide walks through the full open-source workflow: fork → clone → set upstream → branch → change → commit → push → open PR → sync fork.

---

## 1. Fork the repository
Click **Fork** (top right of the repo page) to create your own copy under your GitHub account.

## 2. Clone your fork locally
```bash
git clone https://github.com/<your-username>/Basic-Git-and-Github-Training.git
cd Basic-Git-and-Github-Training
```

## 3. Keep your fork updated (Upstream Setup)
To sync changes from the original repository into your fork later:
```bash
# Add original repo as 'upstream'
git remote add upstream https://github.com/<original-owner>/Basic-Git-and-Github-Training.git

# Verify remotes (should show origin and upstream)
git remote -v
```

To fetch and merge new changes from upstream:
```bash
git checkout main
git fetch upstream
git merge upstream/main
git push origin main
```

## 4. Create a new branch
Never work directly on `main` — always create a feature branch first.
```bash
git checkout -b feature/add-pr-guide
```

## 5. Make your change
Edit or add files, then inspect what changed:
```bash
git status
git diff
```

## 6. Stage and commit
```bash
git add .
git commit -m "docs: add guide on creating pull requests"
```

## 7. Push your branch to GitHub
```bash
git push origin feature/add-pr-guide
```

## 8. Open the Pull Request
1. Go to your fork on GitHub — you'll see a banner: **"Compare & pull request"**. Click it.
2. Set the **base repository** to the original repository (`<original-owner>/Basic-Git-and-Github-Training`) and base branch to `main`.
3. Set the **compare branch** to `feature/add-pr-guide` (your branch).
4. Add a clear title and short description of what you changed and why.
5. Click **Create pull request**.

## 9. Respond to review feedback
If maintainers request changes:
```bash
# Make edits in your files
git add .
git commit -m "docs: address review feedback"
git push origin feature/add-pr-guide
```
The PR updates automatically — no need to open a new one.

---

## Quick Reference Cheat Sheet

| Action | Command |
|---|---|
| Clone fork | `git clone https://github.com/<your-username>/<repo>.git` |
| Add upstream | `git remote add upstream https://github.com/<original-owner>/<repo>.git` |
| Sync main | `git checkout main && git fetch upstream && git merge upstream/main` |
| New branch | `git checkout -b <branch-name>` |
| Check status | `git status` |
| Stage changes | `git add <file>` |
| Commit | `git commit -m "type: brief description"` |
| Push | `git push origin <branch-name>` |
| Open PR | Done via GitHub UI (**Compare & pull request** button) |

---
*Tip: Keep each PR focused on one small feature or fix — concise PRs are much easier to review and merge!*