# Contributing to Basic Git and GitHub Training

Thank you for considering contributing to this training resource! Whether you're fixing a typo, improving explanations, adding practical examples, or adding new lab steps, your contributions help make Git and GitHub concepts clearer for everyone.

---

## 🚀 How to Contribute (Step-by-Step)

For a complete walkthrough of the fork & PR flow, see our [Git Fork & PR Guide](GitForkGuide.md).

### 1. Fork & Clone
1. Click the **Fork** button at the top right of the repository page.
2. Clone your fork to your local machine:
   ```bash
   git clone https://github.com/<your-username>/Basic-Git-and-Github-Training.git
   cd Basic-Git-and-Github-Training
   ```

### 2. Set Up Upstream Remote
To keep your local `main` branch synchronized with the main repository:
```bash
git remote add upstream https://github.com/pr4shxnt/Basic-Git-and-Github-Training.git
```

### 3. Create a Feature Branch
Always create a new branch for your edits. Do not commit directly to `main`:
```bash
git checkout -b docs/describe-your-change
```

### 4. Make & Verify Your Edits
- Keep edits clear, concise, and beginner-friendly.
- Ensure links between lab files remain intact (`README.md`, `Lab1` to `Lab7`).
- Test all terminal commands in your local shell to verify accuracy.

### 5. Commit & Push
Follow clean commit message guidelines (e.g. using conventional commit prefixes like `docs:`, `fix:`, `feat:`):
```bash
git add .
git commit -m "docs: clarify git revert vs reset in Lab 2"
git push origin docs/describe-your-change
```

### 6. Submit a Pull Request (PR)
1. Navigate to your fork on GitHub.
2. Click **Compare & pull request**.
3. Provide a clear PR title and summary of what was changed and why.
4. Submit your PR for review!

---

## 📝 Guidelines for PRs

- **One Topic per PR**: Keep pull requests focused on a single typo fix, feature addition, or lab improvement.
- **Clear Commit Messages**: Use descriptive commit messages (e.g., `docs: fix typo in Lab 3 link`).
- **Be Welcoming**: This repo is designed for beginners. Keep explanations accessible and encouraging.

Happy coding and open-source contributing! 🎉
