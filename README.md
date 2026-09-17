# Git & GitHub — Complete Step by Step (VSCode + Terminal)

![Last Commit](https://img.shields.io/github/last-commit/pr4shxnt/Basic-Git-and-Github-Training)
![Repo Size](https://img.shields.io/github/repo-size/pr4shxnt/Basic-Git-and-Github-Training)
![Issues](https://img.shields.io/github/issues/pr4shxnt/Basic-Git-and-Github-Training)
![Stars](https://img.shields.io/github/stars/pr4shxnt/Basic-Git-and-Github-Training?style=flat)
![Made with Markdown](https://img.shields.io/badge/made%20with-Markdown-1f425f.svg)

A hands-on, step-by-step training for learning Git and GitHub using VSCode and the terminal side by side. No prior Git experience required — just follow the labs in order.

## Prerequisites

Before starting, make sure you have:

- **Git** installed — check with `git --version`
- **VSCode** installed, with the integrated terminal enabled
- A **GitHub account**, and Git configured with your identity:
  ```bash
  git config --global user.name "Your Name"
  git config --global user.email "you@example.com"
  ```
- Basic comfort typing commands in a terminal (no scripting knowledge needed)

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

## Contributing

Found a typo or a step that doesn't work as written? Contributions are welcome — and going through the flow below is itself good practice for everything taught in these labs.

1. **Fork** this repo (button, top right of the GitHub page).
2. **Clone** your fork locally:
   ```bash
   git clone https://github.com/<your-username>/Basic-Git-and-Github-Training.git
   cd Basic-Git-and-Github-Training
   ```
3. **Create a branch** for your change:
   ```bash
   git checkout -b fix/short-description
   ```
4. Make your edits, then **stage and commit**:
   ```bash
   git add .
   git commit -m "docs: describe your change here"
   ```
5. **Push** the branch to your fork:
   ```bash
   git push origin fix/short-description
   ```
6. Open a **pull request** from your branch into this repo's `main` branch, with a short description of what you changed and why.
