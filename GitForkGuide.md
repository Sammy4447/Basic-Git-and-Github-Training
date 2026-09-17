# How to Create a Pull Request (PR)

This file walks through the full flow: fork → clone → branch → change → commit → push → open PR.

## 1. Fork the repository
Click **Fork** (top right of the repo page) to create your own copy under your GitHub account.

## 2. Clone your fork locally
```bash
git clone https://github.com/<your-username>/Basic-Git-and-Github-Training.git
cd Basic-Git-and-Github-Training
```

## 3. Create a new branch
Never work directly on `main` — always branch first.
```bash
git checkout -b add-pr-guide
```

## 4. Make your change
Edit or add a file (like this one), then check what changed:
```bash
git status
git diff
```

## 5. Stage and commit
```bash
git add HOW_TO_CREATE_A_PR.md
git commit -m "Add guide: how to create a pull request"
```

## 6. Push your branch to GitHub
```bash
git push origin add-pr-guide
```

## 7. Open the Pull Request
1. Go to your fork on GitHub — you'll see a banner: **"Compare & pull request"**. Click it.
2. Set the base repository to the original repo (`Sammy4447/Basic-Git-and-Github-Training`) and base branch to `main`.
3. Set the compare branch to `add-pr-guide` (your branch).
4. Add a clear title and short description of what you changed and why.
5. Click **Create pull request**.

## 8. Respond to feedback (if any)
If the maintainer requests changes:
```bash
# make edits
git add .
git commit -m "Address review feedback"
git push origin add-pr-guide
```
The PR updates automatically — no need to open a new one.

## Quick reference (cheat sheet)
| Step | Command |
|---|---|
| Clone | `git clone <fork-url>` |
| New branch | `git checkout -b <branch-name>` |
| Stage changes | `git add <file>` |
| Commit | `git commit -m "message"` |
| Push | `git push origin <branch-name>` |
| Open PR | Done via GitHub UI (Compare & pull request button) |

---
*Tip: keep each PR focused on one small change — it's easier to review and merge.*