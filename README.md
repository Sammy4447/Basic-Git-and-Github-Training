# Git & GitHub — Complete Step by Step (VSCode + Terminal)

![Last Commit](https://img.shields.io/github/last-commit/pr4shxnt/Basic-Git-and-Github-Training)
![Repo Size](https://img.shields.io/github/repo-size/pr4shxnt/Basic-Git-and-Github-Training)
![Issues](https://img.shields.io/github/issues/pr4shxnt/Basic-Git-and-Github-Training)
![Stars](https://img.shields.io/github/stars/pr4shxnt/Basic-Git-and-Github-Training?style=flat)
![Made with Markdown](https://img.shields.io/badge/made%20with-Markdown-1f425f.svg)

A hands-on, step-by-step training for learning Git and GitHub using VSCode and the terminal side by side. No prior Git experience required — just follow the labs in order.

## How to use this training

1. Open this repo in VSCode.
2. Work through the labs **in order** — each one builds on commands and state from the last.
3. Type the terminal commands yourself instead of copy-pasting; muscle memory is the point.
4. Use the "Back to index" link at the bottom of each lab to return here.

## Labs

This training is split into 7 labs, each in its own file.

| Lab | Topic | File |
|---|---|---|
| Lab 1 | Initial Setup & First Commits (Steps 1–7) | [Lab1-Initial-Setup-First-Commits.md](Lab1-Initial-Setup-First-Commits.md) |
| Lab 2 | Undoing Changes (Steps 8–11) | [Lab2-Undoing-Changes.md](Lab2-Undoing-Changes.md) |
| Lab 3 | GitHub Basics (Steps 12–15) | [Lab3-GitHub-Basics.md](Lab3-GitHub-Basics.md) |
| Lab 4 | Branching & Merging (Steps 16–21) | [Lab4-Branching-Merging.md](Lab4-Branching-Merging.md) |
| Lab 5 | Advanced Commands (Steps 22–24) | [Lab5-Advanced-Commands.md](Lab5-Advanced-Commands.md) |
| Lab 6 | Tags & Releases (Steps 25–27) | [Lab6-Tags-Releases.md](Lab6-Tags-Releases.md) |
| Lab 7 | Inspection & Utilities (Step 28) | [Lab7-Inspection-Utilities.md](Lab7-Inspection-Utilities.md) |

Each lab README contains the exact terminal commands and VSCode actions needed to complete its steps.
## .gitignore
.gitignore is a file that tells Git which files or folders not to track or upload to GitHub.

Think of it as a “Do Not Upload” list.

Example:
node_modules/
.env
*.log
dist/

Why use it ?

🔒 Protect secrets: .env may contain API keys and passwords.
📦 Avoid unnecessary files: node_modules/ can contain thousands of dependency files.
🧹 Keep the repository clean: Ignore logs, build files, and temporary files.

Example project:
project/
├── index.js       ✅ tracked
├── package.json   ✅ tracked
├── .env           ❌ ignored
├── node_modules/  ❌ ignored
└── error.log      ❌ ignored

Important : .gitignore only prevents untracked files from being added. It does not automatically stop tracking a file that was already committed

## Contributing

Found a typo or a step that doesn't work as written? Open an issue or a pull request — this is a training resource, and corrections make it better for the next learner.
Thank You !
