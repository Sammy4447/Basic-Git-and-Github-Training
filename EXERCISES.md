# Practice Exercises

After completing the labs, test your knowledge with these exercises. Each one focuses on a specific skill.

## Exercise 1: Redo Commits with a Message

**What you'll practice:** Committing often, using clear messages

**Setup:**
```bash
git checkout -b exercise/messaging
mkdir exercise1
cd exercise1
```

**Task:**
1. Create a file `steps.txt`
2. Add one line: `Step 1 complete`
3. Commit with message: `"add step 1"`
4. Add a new line: `Step 2 complete`
5. Commit: `"add step 2"`
6. Add a new line: `Step 3 complete`
7. Commit: `"add step 3"`
8. View your history: `git log --oneline` (you should see 3 commits)

**Check:**
```bash
git log --oneline              # should show 3 commits with your messages
```

---

## Exercise 2: Branch Practice

**What you'll practice:** Creating branches, switching, merging

**Task:**
1. Make sure you're on `main`: `git checkout main`
2. Create a file `main-file.txt` with content `This is on main`
3. Commit: `"initial file on main"`
4. Create a new branch: `git checkout -b feature/sidebar`
5. Create `sidebar.txt` with content `This is the sidebar`
6. Commit: `"add sidebar component"`
7. Switch back to main: `git checkout main`
8. Check: `sidebar.txt` should **not** be here
9. Merge the feature branch: `git merge feature/sidebar`
10. Check: `sidebar.txt` **should** be here now
11. Delete the feature branch: `git branch -d feature/sidebar`

**Verify:**
```bash
git branch                     # only main should remain
ls                             # should see both main-file.txt and sidebar.txt
```

---

## Exercise 3: Undoing the Right Way

**What you'll practice:** Undoing changes, resetting commits, reverting

**Setup:**
```bash
git checkout -b exercise/undo
```

**Task:**
1. Create `log.txt` with one line: `First entry`
2. Commit: `"add first log entry"`
3. Edit `log.txt`, add line: `Second entry`
4. Commit: `"add second entry"`
5. Edit `log.txt`, add line: `Third entry` (don't commit yet)
6. Run `git status` and `git diff` — see your uncommitted changes
7. Discard the uncommitted changes: `git restore log.txt`
8. Check: `Third entry` is gone, file only has first two lines
9. Commit something new: create `metadata.txt` with `Created today`, commit `"add metadata"`
10. Undo this commit but keep changes: `git reset HEAD~1`
11. You should see `metadata.txt` in working directory but not in commit history
12. Now commit it: `git add . && git commit -m "add metadata properly"`

**Verify:**
```bash
git log --oneline              # should see 4 commits
ls                             # should see log.txt and metadata.txt
```

---

## Exercise 4: Stash and Switch

**What you'll practice:** Using stash for context switching

**Setup:**
```bash
git checkout -b exercise/stash-demo
```

**Task:**
1. Create `work.txt` with: `Important work in progress`
2. Edit but **don't commit**: add line `Not done yet`
3. Check: `git status` shows changes
4. Suddenly you need to switch to main (emergency!)
5. Stash your work: `git stash`
6. Check: `git status` is clean
7. You can now switch branches: `git checkout main`
8. Do something on main: create `urgent.txt` with `Fixed the bug`, commit
9. Switch back: `git checkout exercise/stash-demo`
10. Pop the stash: `git stash pop`
11. Check: `work.txt` is back with all your changes

**Verify:**
```bash
git stash list                 # should be empty (you popped it)
cat work.txt                   # should see "Not done yet"
```

---

## Exercise 5: Cherry Pick a Single Commit

**What you'll practice:** Picking one commit from another branch

**Task:**
1. Make sure you're on main: `git checkout main`
2. Create a new branch: `git checkout -b feature/database`
3. Make 3 commits:
   - Create `db-config.txt` with `Connection string`, commit: `"add db config"`
   - Create `db-schema.txt` with `Schema definition`, commit: `"add db schema"`
   - Create `db-backup.txt` with `Backup script`, commit: `"add backup script"`
4. Go to main: `git checkout main`
5. Get the commit hash of just the "add db config" commit:
   ```bash
   git log feature/database --oneline
   ```
6. Cherry pick only that commit: `git cherry-pick <hash-of-db-config-commit>`
7. Check: only `db-config.txt` should be on main (not the other two files)

**Verify:**
```bash
ls                             # only db-config.txt, NOT db-schema.txt or db-backup.txt
git log --oneline              # should show "add db config" commit on main
```

---

## Exercise 6: Tag a Release

**What you'll practice:** Creating tags for releases

**Task:**
1. Create a file `version.txt` with `1.0.0`
2. Commit: `"release 1.0.0"`
3. Tag this commit: `git tag -a v1.0.0 -m "First release"`
4. Make a new feature: create `feature2.txt` with `New feature`, commit
5. Create another tag: `git tag -a v1.1.0 -m "Second release with new feature"`
6. List all tags: `git tag`
7. Show details of a tag: `git show v1.0.0`

**Verify:**
```bash
git tag                        # should show v1.0.0 and v1.1.0
git show v1.0.0                # should show commit message and version.txt
```

---

## Exercise 7: Create and Resolve a Merge Conflict

**What you'll practice:** Handling merge conflicts

**Task:**
1. Create `config.txt` with content: `debug = false`
2. Commit: `"initial config"`
3. Create a branch: `git checkout -b feature/debug-mode`
4. Edit `config.txt`: change to `debug = true`
5. Commit: `"enable debug mode"`
6. Go back to main: `git checkout main`
7. Edit `config.txt`: change to `debug = advanced` (different change!)
8. Commit: `"set advanced debug"`
9. Try to merge: `git merge feature/debug-mode`
10. **CONFLICT!** Open `config.txt` and you'll see:
    ```
    <<<<<<< HEAD
    debug = advanced
    =======
    debug = true
    >>>>>>> feature/debug-mode
    ```
11. Decide to keep the advanced mode, edit to just: `debug = advanced`
12. Remove the conflict markers
13. Stage and commit: `git add config.txt && git commit -m "resolve conflict: keep advanced"`

**Verify:**
```bash
cat config.txt                 # should have only "debug = advanced"
git log --oneline              # merge commit should be visible
```

---

## Exercise 8: Compare Branches

**What you'll practice:** Viewing differences between branches

**Task:**
1. On main, create `README.md` with `Project version 1`
2. Commit: `"version 1 readme"`
3. Create branch: `git checkout -b feature/docs`
4. Edit `README.md` to add line: `Added features for version 2`
5. Create `CONTRIBUTING.md` with `How to contribute`
6. Commit both: `git add . && git commit -m "add contributing guide and update readme"`
7. Go to main: `git checkout main`
8. Compare the branches:
   ```bash
   git diff main feature/docs              # see all differences
   git diff main feature/docs --name-only  # just the file names
   git diff main feature/docs --stat       # summary of changes
   ```

**Verify:**
```bash
git diff main feature/docs                # should show README.md and CONTRIBUTING.md changes
git diff main feature/docs --name-only    # should list: README.md, CONTRIBUTING.md
```

---

## Challenge: Full Workflow

Combine everything you learned!

**Scenario:** You're adding a new feature. Do this:

1. Create a new branch: `git checkout -b feature/user-auth`
2. Make 3 commits:
   - Create `login.py` with `def login_user(): pass`
   - Create `auth.py` with `def authenticate(): pass`
   - Update `login.py` with `def login_user(username, password):`
3. Switch to main and make a conflicting change (edit `login.py`)
4. Merge `feature/user-auth` into main and resolve the conflict
5. Tag the merge as `v2.0.0-beta`
6. List all your commits and tags
7. Clean up: delete the feature branch

**Final check:**
```bash
git branch                     # only main remains
git tag                        # shows v2.0.0-beta
git log --oneline --all        # shows all commits including merge
```

---

## Tips for All Exercises

- **Always check first:** `git status` before every major action
- **View history:** `git log --oneline` to see what you've done
- **Review changes:** `git diff` before committing
- **Branch early:** create a new branch for each exercise
- **Don't panic:** you can't lose commits in Git — they're always recoverable!

---

**Stuck?** Check [TROUBLESHOOTING.md](TROUBLESHOOTING.md) or review the corresponding lab.

**Want more?** Try combining exercises or think of real workflows you encounter and practice them!

