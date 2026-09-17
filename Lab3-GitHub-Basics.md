# Lab 3 — GitHub Basics

[← Back to index](README.md)

## Step 12 — Connect to GitHub

> **Use it when:** your project so far only exists on your laptop and you now want a backup, a place to share it, or to work on it from another machine. `git remote add origin` tells your local repo *where* on GitHub it belongs — it does not upload anything yet.
> **Already have a remote?** Then you don't need this — `git remote -v` will show it. To point at a different repo instead, use `git remote set-url origin <new-url>`.

Go to GitHub.com → New Repository → name it `my-project` → Create (no README)

Terminal:

```bash
git remote add origin https://github.com/username/my-project.git
git remote -v
```

## Step 13 — Push to GitHub

> **Use it when:** you have commits on your machine that GitHub doesn't have yet. Push = upload.
> **Why `-u`:** it links your local `main` to `origin/main` once, so from then on plain `git push` and `git pull` work without naming the branch.

Terminal:

```bash
git push -u origin main
```

Refresh GitHub in browser — your files are live ✅

## Step 14 — Clone a Repo

> **Use it when:** the project already exists on GitHub and you want a copy on this machine — joining a team's project, setting up a second laptop, or grabbing someone's open-source code.
> **Clone vs init:** clone for a project that already exists remotely; `git init` (Step 2) for one you're starting yourself. Clone also sets up `origin` for you, so no Step 12 needed.

Terminal:

```bash
cd Desktop
git clone https://github.com/username/my-project.git
cd my-project
```

In VSCode:

```
File → Open Folder → select cloned my-project
```

## Step 15 — Pull Changes from GitHub

> **Use it when:** someone else pushed changes and your copy is out of date. Pull = download + merge into your branch.
> **Habit worth building:** pull *before* you start working each day, and again before you push. If you push without pulling, Git rejects it with "rejected — non-fast-forward" — that just means the remote has commits you don't; pull first, then push.

In VSCode — open `hello.txt`, add a line:

```
Hello Git
I am learning Git
Git is a version control system
this line added by teammate
```

Save — `Ctrl + S`

Terminal:

```bash
git add .
git commit -m "teammate added a line"
git push origin main
```

Now on the original machine:

```bash
git pull origin main
```

Open `hello.txt` in VSCode — teammate's line is now here ✅

## SSH Authentication Setup for GitHub

> **Use it when:** every push and pull is asking you for a username and password/token and you're tired of it, or you're setting up a machine you'll use regularly. One-time setup per machine.
> **Which path:** on Windows, stick with HTTPS + Git Credential Manager (it's already installed and just works). On macOS and Linux, generate an SSH key. Either way you only do it once.

HTTPS asks for a username/password (or token) every time you push. SSH uses a key pair instead — set it up once per machine.

### Windows — use HTTPS 

On Windows, authenticate over HTTPS using **Git Credential Manager (GCM)** — it comes bundled with Git for Windows and is the default/recommended way to sign in.

```powershell
# 1. Clone (or set an existing repo's remote) using the HTTPS URL
git clone https://github.com/username/my-project.git
```

```powershell
# or, for a repo you already have locally:
git remote set-url origin https://github.com/username/my-project.git
git remote -v
```

The first time you `push`/`pull`/`clone`, a browser window pops up asking you to log in to GitHub — sign in once and Git Credential Manager caches it for every future command, no key generation needed.

> **Fallback (only if GCM's browser popup doesn't appear):** GitHub no longer accepts your account password over HTTPS, so generate a **Personal Access Token** and use it as the password instead:
> ```
> GitHub.com → profile picture → Settings → Developer settings
> → Personal access tokens → Tokens (classic) → Generate new token
> → check "repo" scope → Generate → copy the token
> ```
> Where to put it — a terminal/Git prompt appears (in PowerShell, or a small Git popup window) asking for:
> ```
> Username for 'https://github.com': your-github-username
> Password for 'https://your-github-username@github.com': <paste the token here>
> ```
> Type your GitHub username as usual, and paste the **token** in place of the password (right-click to paste in PowerShell, since Ctrl+V may not work). It's cached after the first use, so you won't be asked again on that machine.

### macOS (Terminal)

```bash
# 1. Check for an existing key
ls -al ~/.ssh

# 2. Generate a new key
ssh-keygen -t ed25519 -C "your_email@example.com"

# 3. Start the ssh-agent
eval "$(ssh-agent -s)"

# 4. (Recommended) create/update ~/.ssh/config to auto-load the key from Keychain
cat >> ~/.ssh/config << 'EOF'
Host github.com
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
EOF

# 5. Add the key to the agent and Keychain
ssh-add --apple-use-keychain ~/.ssh/id_ed25519

# 6. Copy the public key
pbcopy < ~/.ssh/id_ed25519.pub
```

### Linux (Terminal)

```bash
# 1. Check for an existing key
ls -al ~/.ssh

# 2. Generate a new key
ssh-keygen -t ed25519 -C "your_email@example.com"

# 3. Start the ssh-agent
eval "$(ssh-agent -s)"

# 4. Add the key to the agent
ssh-add ~/.ssh/id_ed25519

# 5. Copy the public key (install xclip if needed: sudo apt install xclip)
xclip -sel clip < ~/.ssh/id_ed25519.pub

# or just print it and copy manually
cat ~/.ssh/id_ed25519.pub
```

### Add the key to GitHub (macOS & Linux)

```
GitHub.com → click profile picture → Settings
→ SSH and GPG keys → New SSH key
→ Title: e.g. "My Laptop" → Key: paste (Ctrl+V) → Add SSH key
```

### Test the connection (macOS & Linux)

```bash
ssh -T git@github.com
```

Type `yes` if asked to trust the host. You should see:

```
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

### Switch a repo from HTTPS to SSH (macOS & Linux)

```bash
git remote set-url origin git@github.com:username/my-project.git
git remote -v
```

Now `git push` / `git pull` will use SSH — no more username/password prompts ✅

---
Next: [Lab 4 — Branching & Merging](Lab4-Branching-Merging.md)
