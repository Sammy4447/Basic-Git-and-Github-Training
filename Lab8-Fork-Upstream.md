# Lab 8 — Forking & Upstream

[← Back to index](README.md)

## Step 29 — Fork a Repository

> **Use it when:** you want to contribute to a repo you don't have write access to — someone else's open-source project, or your instructor's training repo. You can't push to it directly, so you make **your own copy on GitHub** (a fork), push there, and then ask them to pull your work in.
> **Fork vs clone:** a **fork** is a copy of the repo on *GitHub*, under your account. A **clone** is a copy on *your computer*. The normal flow is: fork first (on the website), then clone your fork.

On GitHub:

```
1. Open the repo you want to contribute to
2. Click Fork (top right) → Create fork
3. You now have github.com/<your-username>/<repo-name>
```

Terminal — clone **your fork**, not the original:

```bash
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>
git remote -v                       # origin = your fork ✅
```

In VSCode:

```
File → Open Folder → select the cloned folder
```

## Step 30 — Add the `upstream` Remote

> **Use it when:** right after cloning a fork. Your fork does **not** update itself — the moment the original repo gets new commits, your fork is stale. Adding the original repo as a second remote called `upstream` gives you a way to pull those updates down.
> **The two remotes:** `origin` = your fork (you can push here). `upstream` = the original repo (you only pull from here).

Terminal:

```bash
git remote add upstream https://github.com/<original-owner>/<repo-name>.git
git remote -v                       # origin AND upstream listed ✅
```

You should see four lines — `origin` (fetch/push) and `upstream` (fetch/push).

## Step 31 — Sync Your Fork with Upstream

> **Use it when:** before starting any new piece of work, and again before you open a pull request. If the original repo has moved ahead, you want your branch based on the *latest* code — otherwise your PR arrives with conflicts.
> **What each command does:** `fetch` downloads upstream's commits without touching your files; `merge` (or `rebase`) then applies them to your branch; `push` sends the updated `main` back up to your fork.

Terminal:

```bash
git checkout main
git fetch upstream                  # download upstream's latest
git merge upstream/main             # bring them into your main
git push origin main                # update your fork on GitHub ✅
```

Prefer a straight-line history? Use rebase instead of merge — see [Step 24](Lab5-Advanced-Commands.md):

```bash
git fetch upstream
git rebase upstream/main
git push origin main
```

> **Tip:** GitHub also has a **Sync fork** button on your fork's page that does the same thing in the browser. The commands are worth knowing because they work when you're offline from the website and when you need rebase instead of merge.

---
Next: [Lab 9 — Pull Requests](Lab9-Pull-Requests.md)

[← Back to index](README.md)
