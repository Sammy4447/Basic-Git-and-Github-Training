GitHub Basic Guide — Beginner
1. What is GitHub?

GitHub is an online platform where you can:

Store your Git projects
Upload code
Download/clone projects
Work with other developers
Create branches
Create Pull Requests
Track issues
Review code
Manage projects

Simple:

Git       = Version control on your computer
GitHub    = Online platform for Git repositories
VS Code   = Where you write your code
Terminal  = Where you run Git commands
2. Create a GitHub Account

Go to GitHub and create an account.

GitHub

After creating your account, you can create repositories.

3. Create a GitHub Repository

On GitHub:

GitHub
  ↓
New Repository
  ↓
Repository name
  ↓
Public / Private
  ↓
Create repository

Example repository name:

my-first-project
Public vs Private

Public

Anyone can see the repository.

Private

Only people you give access to can see it.

4. Create a Repository Without README

If you're learning Git locally, you can create an empty repository on GitHub.

For example:

Repository name:
my-first-project

Description:
My first GitHub project

Public

You can leave these unchecked initially:

☐ Add a README file
☐ Add .gitignore
☐ Choose a license

Then click:

Create repository
5. Create a Local Project

Open VS Code terminal.

mkdir my-first-project

Enter the folder:

cd my-first-project

Open it in VS Code:

code .
6. Initialize Git

Inside your project:

git init

Check:

git status

You should see something similar to:

On branch master
No commits yet

or:

On branch main
7. Create a File

Create:

index.html

Example:

<!DOCTYPE html>
<html>
<head>
    <title>My First Project</title>
</head>
<body>
    <h1>Hello GitHub</h1>
</body>
</html>
8. Check Git Status
git status

You might see:

Untracked files:
    index.html

This means Git sees the file but isn't tracking it yet.

9. Add the File

Add one file:

git add index.html

Or add everything:

git add .

Check:

git status

Now you should see:

Changes to be committed:
    new file: index.html
10. Make Your First Commit
git commit -m "Initial commit"

Now your project has its first Git checkpoint.

11. Rename Branch to Main

Use:

git branch -M main

Check:

git branch

You should see:

* main

The * means you are currently on that branch.

12. Connect Git to GitHub

Copy your GitHub repository URL.

Example:

https://github.com/your-username/my-first-project.git

Add it as the remote:

git remote add origin https://github.com/your-username/my-first-project.git

Check it:

git remote -v

You should see:

origin  https://github.com/your-username/my-first-project.git (fetch)
origin  https://github.com/your-username/my-first-project.git (push)
13. Push Your Project to GitHub

First push:

git push -u origin main

After this finishes, refresh your GitHub repository.

Your files should appear online.

14. Complete First-Time GitHub Workflow

These are the commands you should understand:

mkdir my-first-project
cd my-first-project
git init
git branch -M main
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/your-username/my-first-project.git
git push -u origin main

If you already created your files before git add ., this complete flow works.

15. GitHub → Local Computer: Clone

If someone already has a project on GitHub, you can download it using:

git clone https://github.com/username/project.git

Example:

git clone https://github.com/username/my-first-project.git

Enter the project:

cd my-first-project

Open in VS Code:

code .
16. Check Remote Repository
git remote -v

Example:

origin  https://github.com/username/my-first-project.git (fetch)
origin  https://github.com/username/my-first-project.git (push)
17. GitHub → Local: Pull

Suppose another team member changed the project on GitHub.

Get their changes:

git pull

Or explicitly:

git pull origin main

Think:

GitHub
   ↓
git pull
   ↓
Your computer
18. Local → GitHub: Push

After changing your code:

git status

Add changes:

git add .

Commit:

git commit -m "Update project"

Push:

git push

Think:

Your computer
      ↓
   git push
      ↓
   GitHub
19. The Most Important GitHub Workflow

Use this every day:

git pull

Work on your code.

Then:

git status

Add:

git add .

Commit:

git commit -m "Describe your changes"

Push:

git push

So:

PULL
 ↓
WORK
 ↓
STATUS
 ↓
ADD
 ↓
COMMIT
 ↓
PUSH
20. Create a Branch

Never make every change directly on main in a team project.

Create a branch:

git switch -c feature/login

This creates and switches to:

feature/login

Check:

git branch

Example:

* feature/login
  main
21. Make Changes on Your Branch

Edit your files.

Then:

git status

Add:

git add .

Commit:

git commit -m "Add login page"
22. Push Your Branch
git push -u origin feature/login

Now your branch exists on GitHub.

GitHub

main
│
└── feature/login
23. Pull Request

After pushing your branch, GitHub can show:

Compare & pull request

Click it.

Then:

feature/login
      ↓
Pull Request
      ↓
main

A Pull Request means:

"Please review my changes and consider merging them into the main branch."

24. Merge Pull Request

After review, the repository maintainer can merge the Pull Request.

feature/login
      ↓
Pull Request
      ↓
Review
      ↓
Merge
      ↓
main
25. Delete a Branch

After merging, delete the local branch:

git branch -d feature/login

Delete remote branch:

git push origin --delete feature/login
26. Fork

A Fork creates your own GitHub copy of another person's repository.

Example:

Original Repository
        ↓
       Fork
        ↓
Your GitHub Account

Fork is commonly used when you don't have direct permission to modify the original repository.

27. Fork + Clone Workflow

Suppose you want to contribute to:

https://github.com/other-user/project.git

First:

GitHub → Fork

Then clone your fork:

git clone https://github.com/YOUR-USERNAME/project.git

Enter:

cd project

Create a branch:

git switch -c fix/navbar

Make changes.

Then:

git add .
git commit -m "Fix navbar"

Push:

git push -u origin fix/navbar

Then create a Pull Request.

28. Fork vs Clone
Feature	Fork	Clone
Where?	GitHub	Computer
Creates copy?	Yes	Downloads copy
Used for	Contributing	Local development
Command?	GitHub button	git clone

Usually:

Fork
 ↓
Clone
 ↓
Branch
 ↓
Edit
 ↓
Commit
 ↓
Push
 ↓
Pull Request
29. GitHub Repository Settings

A repository can contain:

Code
Issues
Pull Requests
Actions
Projects
Wiki
Security
Insights
Settings

Not every repository has every feature enabled.

30. README.md

A README explains your project.

Create:

README.md

Example:

# My First Project

This is my first GitHub project.

## Features

- Homepage
- Login
- Registration

## Technologies

- HTML
- CSS
- JavaScript

## Installation

Clone the repository:

```bash
git clone https://github.com/username/my-first-project.git
Author

Your Name


Then:

```bash
git add README.md
git commit -m "Add README"
git push
31. .gitignore

Create:

.gitignore

For a Node.js project:

node_modules/
.env
dist/
build/
*.log

Then:

git add .
git commit -m "Add gitignore"
git push
Why .gitignore?

It tells Git:

"Don't track these files/folders."

For example:

node_modules/

should normally not be uploaded to GitHub.

32. GitHub Issues

Issues are used to track:

Bug
Task
Feature
Improvement
Question

Example:

Issue #1

Title:
Login button is not working

Description:
The login button doesn't submit the form.

After fixing it, you can create:

git switch -c fix/login-button

Then commit and push.

33. GitHub Stars

A user can click ⭐ on a public repository.

Stars are commonly used to show interest or bookmark repositories.

They do not mean the repository is officially verified or technically perfect.

34. Watch a Repository

GitHub allows you to watch repositories for notifications about activity such as issues and Pull Requests.

35. GitHub Releases

Projects can publish versions such as:

v1.0.0
v1.1.0
v2.0.0

Create a Git tag:

git tag v1.0.0

Push it:

git push origin v1.0.0

Or push all tags:

git push origin --tags
36. GitHub Actions

GitHub Actions can automatically perform tasks when code changes.

Example:

Developer
    ↓
git push
    ↓
GitHub
    ↓
GitHub Actions
    ↓
Run tests
    ↓
Build project
    ↓
Deploy

Example uses:

Testing
Building
Linting
Deployment
CI/CD
37. GitHub Pages

GitHub Pages can host static websites.

Suitable examples:

HTML
CSS
JavaScript

Basic flow:

Website
   ↓
GitHub Repository
   ↓
GitHub Pages
   ↓
Online Website
38. Collaboration With 3 Developers

For a team of three:

                    main
                     │
        ┌────────────┼────────────┐
        ↓            ↓            ↓
   feature/ui   feature/backend  feature/login
        │            │            │
        ↓            ↓            ↓
     Developer    Developer     Developer
        │            │            │
        └────────────┼────────────┘
                     ↓
              Pull Requests
                     ↓
                   Review
                     ↓
                   Merge
                     ↓
                   main

Example branches:

git switch -c feature/frontend
git switch -c feature/backend
git switch -c feature/database
39. Update Your Branch

Before starting new work:

git switch main
git pull origin main

Then create your new branch:

git switch -c feature/new-feature

This helps you start from the latest main.

40. Check Your Current Branch
git branch

The branch with:

*

is your current branch.

Example:

  main
* feature/login

You are currently on:

feature/login
41. See All Remote Branches
git branch -r

See local + remote:

git branch -a
42. See Commit History
git log

Short:

git log --oneline

Graph:

git log --oneline --graph --all
43. See Changes
git diff

See staged changes:

git diff --staged
44. Undo a File Change

If you changed a file but haven't committed it:

git restore filename

Example:

git restore index.html

⚠️ This can discard your uncommitted changes to that file.

45. Unstage a File

If you accidentally did:

git add index.html

Remove it from staging:

git restore --staged index.html

Your file changes remain.

46. Temporarily Save Work

If you're working on something unfinished:

git stash

See stash:

git stash list

Restore:

git stash pop
47. GitHub Remote Commands

See remote:

git remote -v

Add remote:

git remote add origin https://github.com/USERNAME/REPOSITORY.git

Change remote:

git remote set-url origin https://github.com/USERNAME/REPOSITORY.git

Remove remote:

git remote remove origin
48. Important GitHub Terms
Term	Simple meaning
Repository	Project stored on GitHub
Commit	Saved version/checkpoint
Branch	Separate line of development
Main	Main project branch
Remote	Online repository connection
Origin	Common name for remote
Push	Upload commits
Pull	Get remote changes
Clone	Download repository
Fork	Copy repository to your GitHub account
Pull Request	Request to merge changes
Issue	Track bug/task/feature
Merge	Combine branches
Tag	Mark a specific version
Release	Published project version
README	Project documentation
.gitignore	Files Git should ignore
49. Most Important Commands
Setup
git --version
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
Repository
git init
git status
Files
git add .
git add filename
Commits
git commit -m "Your message"
git log --oneline
Branches
git branch
git switch -c feature-name
git switch main
git merge feature-name
GitHub
git remote -v
git push
git pull
git clone https://github.com/USERNAME/REPOSITORY.git
Remote branch
git push -u origin feature-name
50. Complete Real-World Workflow

For your normal projects, remember this:

git switch main
git pull origin main
git switch -c feature/login

Now work on your code.

Then:

git status
git add .
git commit -m "Add login feature"
git push -u origin feature/login

Then on GitHub:

Pull Request
     ↓
Review
     ↓
Merge

After merging:

git switch main
git pull origin main
51. Beginner GitHub Practice

Create a practice repository:

git-practice

Then run:

mkdir git-practice
cd git-practice
git init
git branch -M main

Create:

index.html

Then:

git status
git add .
git commit -m "Initial commit"

Connect GitHub:

git remote add origin https://github.com/YOUR-USERNAME/git-practice.git

Push:

git push -u origin main

Create a branch:

git switch -c feature/about

Create:

about.html

Then:

git add .
git commit -m "Add about page"

Push:

git push -u origin feature/about

Go to GitHub → create Pull Request → review → merge.

Then:

git switch main
git pull origin main

You have now practiced the complete basic GitHub workflow:

CREATE REPOSITORY
       ↓
    git init
       ↓
    git add
       ↓
   git commit
       ↓
 CONNECT GITHUB
       ↓
    git push
       ↓
 CREATE BRANCH
       ↓
     EDIT
       ↓
    COMMIT
       ↓
     PUSH
       ↓
 PULL REQUEST
       ↓
     REVIEW
       ↓
     MERGE
       ↓
     MAIN