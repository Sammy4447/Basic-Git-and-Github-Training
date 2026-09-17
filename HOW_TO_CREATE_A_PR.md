# How to Create a Pull Request (PR)

The fastest way to contribute to any GitHub project — fork, change, submit.

## 1. Fork the repository

Open the repo on GitHub and click **Fork** (top right). This makes a copy under your account.

## 2. Clone your fork

```bash
git clone https://github.com/<your-username>/Basic-Git-and-Github-Training.git
cd Basic-Git-and-Github-Training
```

## 3. Create a branch

Never commit directly on `main` — always use a branch.

```bash
git checkout -b add/your-change
```

## 4. Make your change

Edit or add a file, then review what you changed:

```bash
git status
git diff
```

## 5. Stage and commit

```bash
git add <file>
git commit -m "docs: short description of your change"
```

## 6. Push to your fork

```bash
git push origin add/your-change
```

## 7. Open the pull request

1. On your fork you'll see a **Compare & pull request** button — click it.
2. Base repository: the original repo → `main`.
3. Compare: your branch.
4. Add a clear title and a short description (what did you change, and why).
5. Click **Create pull request**.

## 8. Respond to feedback (if any)

If the maintainer requests changes, edit, commit, and push again — the PR updates automatically:

```bash
git add .
git commit -m "Address review feedback"
git push origin add/your-change
```

## Cheat sheet

| Step | Command / action |
|---|---|
| Fork | GitHub → **Fork** button |
| Clone | `git clone <fork-url>` |
| Branch | `git checkout -b <branch-name>` |
| Stage | `git add <file>` |
| Commit | `git commit -m "message"` |
| Push | `git push origin <branch-name>` |
| Open PR | GitHub → **Compare & pull request** button |

## Three tips

1. One small change per PR — it's easier to review and merge.
2. Write clear commit messages and a short PR description.
3. Keep your branch in sync: `git pull origin main` before you open the PR.

---

*Want the full skill-based walkthrough? See [GitForkGuide.md](GitForkGuide.md).*




## Useful Git Commands

Check the current branch:

git branch

Check the status of your files:

git status

Push a branch to GitHub:

git push origin branch-name