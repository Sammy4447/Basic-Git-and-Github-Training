# Lab 8 — Advanced Git Tools & Repository Recovery

## 🎯 Objective

In this lab, you will explore several Git features that become useful when working with larger projects and more complex repositories.

You will learn how to:

* Recover lost commits using `git reflog`
* Find problematic commits using `git bisect`
* Work on multiple branches simultaneously using `git worktree`
* Manage repositories inside repositories using Git submodules
* Inspect remote branches and references using advanced Git commands

> **Prerequisite:** You should be comfortable with commits, branches, merging, remote repositories, and basic Git history.

---

# Part 1 — Recovering Lost Work with `git reflog`

Git normally shows commits that are reachable from your current branches.

But what happens if you accidentally reset a branch and appear to lose a commit?

This is where **reflog** becomes extremely useful.

## 1. Create some commits

Create a new repository for this exercise:

```bash
mkdir reflog-lab
cd reflog-lab
git init
```

Create a file:

```bash
echo "Version 1" > file.txt
```

Commit it:

```bash
git add file.txt
git commit -m "Add version 1"
```

Make another change:

```bash
echo "Version 2" >> file.txt
git add file.txt
git commit -m "Add version 2"
```

And another:

```bash
echo "Version 3" >> file.txt
git add file.txt
git commit -m "Add version 3"
```

Check the history:

```bash
git log --oneline
```

---

## 2. Accidentally reset the branch

Run:

```bash
git reset --hard HEAD~2
```

Now check:

```bash
git log --oneline
```

The last two commits appear to have disappeared.

But the commits are not necessarily gone.

---

## 3. Use `git reflog`

Run:

```bash
git reflog
```

You should see entries similar to:

```text
abc1234 HEAD@{0}: reset: moving to HEAD~2
def5678 HEAD@{1}: commit: Add version 3
ghi9012 HEAD@{2}: commit: Add version 2
```

The reflog records movements of references such as `HEAD`.

Find the commit corresponding to:

```text
Add version 3
```

Then recover it by creating a new branch:

```bash
git branch recovered-work <commit-hash>
```

For example:

```bash
git branch recovered-work def5678
```

Check:

```bash
git branch
```

Switch to the recovered branch:

```bash
git switch recovered-work
```

Verify:

```bash
git log --oneline
```

### 💡 Key Idea

`git reflog` can help recover commits that are no longer reachable through the normal branch history.

It is especially useful after accidentally running commands such as:

```bash
git reset --hard
```

> **Note:** Reflog entries are stored locally and are not a replacement for a remote backup.

---

# Part 2 — Finding Bugs with `git bisect`

Imagine a project has 100 commits.

The application worked correctly last week, but now it is broken.

Checking every commit manually would be inefficient.

Git provides `git bisect` to perform a **binary search through the commit history**.

---

## 4. Create a test repository

Create a new directory:

```bash
mkdir bisect-lab
cd bisect-lab
git init
```

Create the initial file:

```bash
echo "OK" > status.txt
```

Commit it:

```bash
git add status.txt
git commit -m "Initial version"
```

Now create several commits:

```bash
echo "Feature 1" >> status.txt
git add status.txt
git commit -m "Add feature 1"
```

```bash
echo "Feature 2" >> status.txt
git add status.txt
git commit -m "Add feature 2"
```

Now introduce a bug:

```bash
echo "BUG" >> status.txt
git add status.txt
git commit -m "Introduce bug"
```

Continue creating commits:

```bash
echo "Feature 3" >> status.txt
git add status.txt
git commit -m "Add feature 3"
```

```bash
echo "Feature 4" >> status.txt
git add status.txt
git commit -m "Add feature 4"
```

---

## 5. Start bisecting

Start the bisect process:

```bash
git bisect start
```

Tell Git that the current version is broken:

```bash
git bisect bad
```

Find the earliest commit:

```bash
git log --oneline --reverse
```

Copy the hash of the first working commit and mark it as good:

```bash
git bisect good <commit-hash>
```

Git will automatically check out a commit somewhere between the known good and bad commits.

Test the project.

If the project works:

```bash
git bisect good
```

If it is broken:

```bash
git bisect bad
```

Continue until Git identifies the first bad commit.

---

## 6. Finish the bisect

Once the problematic commit has been identified:

```bash
git bisect reset
```

This returns your repository to the branch state from before the bisect operation.

Check:

```bash
git status
```

### 💡 Key Idea

`git bisect` uses binary search.

Instead of testing every commit:

```text
Commit 1 → Commit 2 → Commit 3 → Commit 4 → Commit 5
```

Git narrows the search:

```text
Good ---------------------- Bad
            ↓
          Test
       ↓         ↓
    Good         Bad
       ↓         ↓
       ...
```

This becomes extremely valuable when debugging projects with hundreds or thousands of commits.

---

# Part 3 — Working on Multiple Branches with `git worktree`

Normally, switching branches changes the files in your working directory.

But sometimes you need two branches available at the same time.

`git worktree` allows you to create multiple working directories connected to the same Git repository.

---

## 7. Create a repository

Create:

```bash
mkdir worktree-lab
cd worktree-lab
git init
```

Create a file:

```bash
echo "Main project" > README.md
```

Commit:

```bash
git add README.md
git commit -m "Initial commit"
```

Create a branch:

```bash
git switch -c feature
```

Make a change:

```bash
echo "Feature development" >> README.md
git add README.md
git commit -m "Add feature"
```

Return to main:

```bash
git switch main
```

---

## 8. Create another working directory

Run:

```bash
git worktree add ../feature-work feature
```

Now your project exists in two directories:

```text
worktree-lab/
feature-work/
```

Check your worktrees:

```bash
git worktree list
```

You should see something similar to:

```text
/path/worktree-lab       abc1234 [main]
/path/feature-work       def5678 [feature]
```

You can now work on `main` and `feature` simultaneously.

---

## 9. Remove the worktree

When finished:

```bash
git worktree remove ../feature-work
```

Check again:

```bash
git worktree list
```

### 💡 When is `git worktree` useful?

It can be useful when:

* You need to compare two branches.
* You are working on two features simultaneously.
* You need to quickly switch to another branch without losing your current working environment.
* You are reviewing another branch while keeping your current branch open.

---

# Part 4 — Git Submodules

Sometimes a project depends on another Git repository.

Instead of copying that repository directly into the project, Git can track it as a **submodule**.

---

## 10. Create a repository

Create a main project:

```bash
mkdir main-project
cd main-project
git init
```

Create a file:

```bash
echo "# Main Project" > README.md
git add README.md
git commit -m "Create main project"
```

---

## 11. Add another repository as a submodule

Use a public repository for practice:

```bash
git submodule add https://github.com/octocat/Spoon-Knife.git external/Spoon-Knife
```

Check the status:

```bash
git status
```

You should see:

```text
.gitmodules
external/Spoon-Knife
```

Commit the submodule:

```bash
git add .
git commit -m "Add Spoon-Knife as submodule"
```

---

## 12. Clone a repository containing a submodule

If someone else clones your repository:

```bash
git clone <repository-url>
```

The submodule directory may initially be empty.

Initialize and download the submodule:

```bash
git submodule update --init --recursive
```

Alternatively, clone everything at once:

```bash
git clone --recurse-submodules <repository-url>
```

### 💡 Key Idea

A submodule allows one Git repository to reference another repository at a specific commit.

This is useful for:

* Shared libraries
* External dependencies
* Large projects with independently maintained components

---

# Part 5 — Advanced Remote Inspection

Git provides several commands for understanding the relationship between your local repository and remote repositories.

---

## 13. View remote repositories

Run:

```bash
git remote -v
```

You might see:

```text
origin  https://github.com/user/project.git (fetch)
origin  https://github.com/user/project.git (push)
```

---

## 14. Inspect a remote

Run:

```bash
git remote show origin
```

This provides information such as:

* Remote URL
* Remote branches
* Tracking branches
* Local branches configured for push/pull

---

## 15. View remote branches

Run:

```bash
git branch -r
```

To see both local and remote branches:

```bash
git branch -a
```

Example:

```text
* main
  feature/login
  remotes/origin/main
  remotes/origin/feature/login
```

---

## 16. Fetch without merging

Run:

```bash
git fetch origin
```

This downloads information about changes from the remote repository without changing your current working files.

After fetching:

```bash
git branch -r
```

You can inspect remote changes before deciding what to do with them.

---

# Part 6 — Useful Git Aliases

If you frequently use a Git command, you can create a shorter alias.

For example:

```bash
git config --global alias.co checkout
```

Now instead of:

```bash
git checkout main
```

you can use:

```bash
git co main
```

Create another alias:

```bash
git config --global alias.st status
```

Now:

```bash
git st
```

is equivalent to:

```bash
git status
```

You can create a useful history alias:

```bash
git config --global alias.lg "log --oneline --graph --decorate --all"
```

Now:

```bash
git lg
```

will display a compact graphical history.

View your configured aliases:

```bash
git config --global --get-regexp alias
```

### ⚠️ Note

Aliases are optional conveniences. They do not create new Git commands; they simply provide shortcuts for commands you already know.

---

# 🧩 Part 7 — Mini Challenge

## Scenario: The Missing Commit

You are working on a project with several developers.

One developer accidentally runs:

```bash
git reset --hard HEAD~3
```

Three commits appear to have disappeared.

### Your task:

1. Create at least five commits.
2. Perform a reset that moves the branch backwards.
3. Use `git reflog` to find the lost commit.
4. Recover the commit using a new branch.
5. Verify the recovered history.

---

## 🐛 Bonus Challenge — Find the Bug

Create at least eight commits.

Introduce a deliberate bug somewhere in the middle of the history.

Then:

1. Mark the current version as `bad`.
2. Find an earlier working commit.
3. Mark it as `good`.
4. Use `git bisect` to locate the problematic commit.
5. Reset the bisect process when finished.

---

# 📝 Questions

Answer the following questions after completing the lab.

1. What information does `git reflog` store?
2. Why can `git reflog` be useful after a `git reset --hard`?
3. What is the purpose of `git bisect`?
4. How does `git bisect` reduce the number of commits that need to be tested?
5. What problem does `git worktree` solve?
6. What is a Git submodule?
7. What is the difference between `git fetch` and `git pull`?
8. What is the purpose of a Git alias?
9. What is the difference between a local branch and a remote-tracking branch?
10. Why might a developer use multiple worktrees instead of repeatedly switching branches?

---

# 📌 Quick Reference

| Command                     | Purpose                                      |
| --------------------------- | -------------------------------------------- |
| `git reflog`                | View changes to `HEAD` and branch references |
| `git bisect start`          | Start a binary search through commit history |
| `git bisect good`           | Mark the current commit as working           |
| `git bisect bad`            | Mark the current commit as broken            |
| `git bisect reset`          | End the bisect operation                     |
| `git worktree add`          | Create another working directory             |
| `git worktree list`         | List active worktrees                        |
| `git worktree remove`       | Remove a worktree                            |
| `git submodule add`         | Add another repository as a submodule        |
| `git submodule update`      | Initialize/update submodules                 |
| `git remote -v`             | Display remote URLs                          |
| `git remote show origin`    | Display detailed remote information          |
| `git branch -r`             | Display remote-tracking branches             |
| `git fetch`                 | Download remote changes without merging      |
| `git config --global alias` | Create a Git command shortcut                |

---

# ✅ Lab Completion Checklist

* [ ] Used `git reflog`
* [ ] Recovered a commit after a reset
* [ ] Used `git bisect`
* [ ] Identified a deliberately broken commit
* [ ] Created and inspected a Git worktree
* [ ] Added a Git submodule
* [ ] Cloned/initialized a repository with a submodule
* [ ] Inspected remote branches
* [ ] Used `git fetch`
* [ ] Created a Git alias
* [ ] Completed the recovery challenge
* [ ] Answered the lab questions

---

## 🎓 Learning Outcome

After completing this lab, you should be able to use Git beyond the standard add → commit → push workflow.

You should now have practical experience with **repository recovery, debugging commit history, parallel development, external repositories, remote inspection, and Git customization**.
