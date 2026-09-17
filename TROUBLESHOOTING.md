# Troubleshooting Common Git Issues

## "fatal: not a git repository"

### Problem
You get this error when running a git command.

### Cause
You're not inside a Git repository folder, or the `.git` folder is missing.

### Solution
1. Make sure you're in the right folder:
   ```bash
   pwd                            # what folder are you in?
   ls -la                         # do you see .git folder?
   ```

2. If not, navigate to your project:
   ```bash
   cd path/to/your/project
   ```

3. If `.git` is missing, initialize Git:
   ```bash
   git init
   ```

---

## "Author identity unknown" or "Please tell me who you are"

### Problem
Git refuses to commit with an error like:
```
*** Please tell me who you are.
Run
  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"
```

### Cause
Git doesn't know your name and email yet (usually on first install).

### Solution
Configure Git globally (one time):
```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Verify it worked:
```bash
git config --list | grep user
```

---

## "Changes not staged for commit" — files won't commit

### Problem
You ran `git commit` but git says there's nothing to commit, even though you changed files.

### Cause
You edited files but didn't `git add` them yet.

### Solution
1. Check what changed:
   ```bash
   git status                    # see which files changed
   git diff                      # see the actual changes
   ```

2. Stage the changes:
   ```bash
   git add .                     # stage all changes
   git add <filename>            # stage specific file
   ```

3. Now commit:
   ```bash
   git commit -m "your message"
   ```

**Pro tip:** Run `git status` before every `git add` and before every `git commit`. It's like checking twice before you finalize something.

---

## "fatal: pathspec ... did not match any files"

### Problem
```bash
git add somefile.txt
fatal: pathspec 'somefile.txt' did not match any files
```

### Cause
The file doesn't exist, or you spelled the name wrong, or you're in the wrong folder.

### Solution
1. Check the file exists:
   ```bash
   ls                            # list files in current folder
   ls -la                        # include hidden files
   ```

2. Make sure you're in the right folder:
   ```bash
   pwd
   ```

3. Use the correct filename and path:
   ```bash
   git add ./correct-filename.txt
   ```

---

## "Updates were rejected because the tip of your current branch is behind"

### Problem
```bash
git push
! [rejected]        main -> main (non-fast-forward)
error: failed to push some refs to ...
```

### Cause
Someone else (or another machine) pushed commits to the remote branch that you don't have locally yet.

### Solution
1. Fetch the remote changes:
   ```bash
   git fetch
   ```

2. Merge them into your branch:
   ```bash
   git merge origin/main
   ```

3. Now push:
   ```bash
   git push
   ```

Or use `git pull` (fetch + merge in one):
```bash
git pull
git push
```

---

## "error: Your local changes to ... would be overwritten by merge"

### Problem
You have uncommitted changes and Git won't let you switch branches or merge.

### Cause
Git is protecting you from losing work — if it switched branches now, your changes would be lost.

### Solution

**Option 1: Commit your changes first** (recommended)
```bash
git status                      # what files changed?
git add .
git commit -m "work in progress"
git checkout <other-branch>     # now it's safe to switch
```

**Option 2: Stash and come back later**
```bash
git stash                       # temporarily save work
git checkout <other-branch>     # now safe to switch
git checkout <first-branch>     # come back
git stash pop                   # restore work
```

**Option 3: Discard changes** (⚠️ careful!)
```bash
git restore .                   # permanently discard all changes
git checkout <other-branch>
```

---

## "nothing to commit, working tree clean" — but I made changes

### Problem
You edited a file but `git status` says nothing changed.

### Cause
Either:
1. You didn't save the file in your editor
2. You're looking at the wrong file
3. You actually have committed this state already

### Solution
1. In your editor (VSCode, etc.), make sure the file is **saved** — look for the white dot that means unsaved changes
2. Save the file: `Ctrl + S` (Windows/Linux) or `Cmd + S` (Mac)
3. Run `git status` again

---

## "git add ." added files I didn't want

### Problem
You ran `git add .` and now there are compiled files, node_modules, or other junk staged.

### Cause
You forgot to create a `.gitignore` file that tells Git what to ignore.

### Solution

1. Unstage everything:
   ```bash
   git reset
   ```

2. Create a `.gitignore` file (or add to it):
   ```bash
   # Linux/Mac
   echo "node_modules/" >> .gitignore
   echo "*.log" >> .gitignore
   
   # Windows (same idea)
   ```

3. Now stage only what you want:
   ```bash
   git add .gitignore myfile.txt
   git commit -m "add .gitignore and actual changes"
   ```

---

## "detached HEAD" — what does this mean?

### Problem
You see a message like "HEAD detached at abc1234" and you're confused.

### Cause
You checked out a specific commit instead of a branch. You're no longer on a branch.

### Solution

Go back to a branch:
```bash
git checkout main              # go to main branch
git checkout -b new-branch     # or create and switch to a new branch
```

**Why this matters:** Changes you make while detached will be lost if you check out another branch. Always work on a branch, not a detached commit.

---

## "merge conflict" — how to resolve it

### Problem
```bash
git merge feature/new-thing
CONFLICT (content): Merge conflict in hello.txt
Automatic merge failed; fix conflicts and then commit the result.
```

### Cause
You and someone else (or another branch) both changed the same lines in the same file.

### Solution

1. Open the conflicted file in your editor (VSCode, etc.)
2. Look for conflict markers:
   ```
   <<<<<<< HEAD
   this is from main
   =======
   this is from feature/new-thing
   >>>>>>> feature/new-thing
   ```

3. Decide which version to keep (or combine them), then delete the conflict markers
4. Stage and commit:
   ```bash
   git add .
   git commit -m "resolve merge conflict in hello.txt"
   ```

**Pro tip:** VSCode and most editors highlight these and offer buttons to "Accept Current" or "Accept Incoming" — use them!

---

## "Oops, I committed to the wrong branch"

### Problem
You committed to `main` but meant to commit to a feature branch.

### Cause
You forgot to checkout the feature branch first.

### Solution

1. Create the branch you meant to commit to (don't switch):
   ```bash
   git branch feature/my-feature
   ```

2. Undo the commit on main (keep changes):
   ```bash
   git reset HEAD~1
   ```

3. Switch to the feature branch:
   ```bash
   git checkout feature/my-feature
   ```

4. Stage and commit:
   ```bash
   git add .
   git commit -m "my feature"
   ```

---

## Still stuck?

- Re-read the corresponding lab in [README.md](README.md)
- Run `git status` — it usually gives a helpful hint about what to do next
- Run `git log --oneline` to see recent commits and understand what state you're in
- Ask in GitHub Issues

---

**Remember:** Git is designed to be hard to lose work. If something feels scary, `git status` first — it will tell you what's safe.

