# Contributing to Git & GitHub Training

Thank you for helping improve this training material! Whether you're fixing a typo, adding an exercise, or clarifying a confusing step, your contribution helps learners.

## How to Contribute

### 1. Fork and Clone
```bash
git clone https://github.com/<your-username>/Basic-Git-and-Github-Training.git
cd Basic-Git-and-Github-Training
```

### 2. Create a Branch
Always create a new branch — never work on `main`:
```bash
git checkout -b feature/your-feature-name
```

Use branch naming conventions:
- `fix/typo-in-lab2` — for typo fixes
- `improve/step-3-clarity` — for improving existing content
- `add/exercise-advanced-merge` — for adding new exercises
- `docs/add-cheatsheet` — for documentation updates

### 3. Make Your Changes

**For fixing typos or clarifying steps:**
- Edit the corresponding Lab file directly
- Keep explanations beginner-friendly
- Use clear terminal command examples

**For adding new content:**
- Follow the existing markdown structure
- Use the same heading and code block format as other labs
- Include "Use it when:" and "Real example:" sections for context

### 4. Commit with Clear Messages
```bash
git add .
git commit -m "fix: clarify git merge syntax in Lab 4"
git commit -m "docs: add troubleshooting guide"
git commit -m "add: new exercises for branching practice"
```

### 5. Push and Create a Pull Request
```bash
git push origin feature/your-feature-name
```

Then on GitHub:
1. Click **"Compare & pull request"**
2. Write a clear title and description of what you changed and why
3. Submit the PR

## Guidelines

### Content
- **Keep explanations simple** — this is for beginners
- **Use real examples** — show when and why to use each command
- **Test everything** — if you mention a command, run it and verify it works
- **Be consistent** — match the style and format of existing labs

### Commits
- **One logical change per commit** — this is actually good Git practice too!
- **Use clear messages** — future readers (including yourself) will thank you
- **Reference issues** — if fixing a reported problem, mention the issue number

### Issues & Requests
- **Found a bug?** Open an issue with the exact step that fails
- **Confused by a step?** Open an issue explaining what's unclear
- **Want a new topic?** Open an issue to discuss before writing

## What We're Looking For

✅ **Typo fixes** — spelling, grammar, formatting  
✅ **Clarity improvements** — better explanations, simpler wording  
✅ **New exercises** — practice problems that reinforce the labs  
✅ **Troubleshooting guides** — common errors and how to fix them  
✅ **Better examples** — more real-world scenarios  

## What We Don't Accept

❌ Removing existing labs or major restructuring (open an issue first!)  
❌ Advanced topics beyond what beginners need  
❌ Opinions on which Git workflow is "best"  
❌ Advertising other tools or tutorials  

## Questions?

- **Issues** — use GitHub Issues for bugs and suggestions
- **Discussions** — use GitHub Discussions for general questions

---

**Thank you for contributing!** Your improvements help thousands of learners. 🙌
