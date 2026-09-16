# Lab 6 — Tags & Releases

[← Back to index](README.md)

## Step 25 — Create a Tag

> **Use it when:** you've reached a version worth naming — `v1.0.0`, the build you shipped to the client, the state you might need to roll back to. A branch moves as you commit; a tag is a permanent bookmark on one exact commit.
> **Note:** `git push` does **not** push tags. You have to push them explicitly with `git push origin --tags`.

Terminal:

```bash
git tag                             # list existing tags
git tag -a v1.0.0 -m "first release"
git tag                             # v1.0.0 appears ✅
git push origin --tags              # push to GitHub
```

Go to GitHub → Tags — `v1.0.0` is visible ✅

## Step 26 — Create a GitHub Release

> **Use it when:** you want to hand a version to actual users, not just mark it in the log. A release wraps a tag with release notes and downloadable files — this is the page people land on to grab your software.

```
GitHub → your repo → Releases → Create a new release
→ Choose tag: v1.0.0
→ Title: First Release
→ Write description
→ Publish Release ✅
```

## Step 27 — Delete a Tag

> **Use it when:** you tagged the wrong commit or misspelled the version. Two separate deletes are needed — one for your machine, one for GitHub — because deleting locally does not touch the remote.
> **Careful:** if others have already pulled that tag, deleting it won't remove it from their machines. For a published release it's usually cleaner to tag a new version than to delete an old one.

Terminal:

```bash
git tag -d v1.0.0                       # delete locally
git push origin --delete v1.0.0        # delete from GitHub
```

---
git show v1.0.0                    # view tag details and the commit it points to

git tag -a v1.1.0 -m "second release"  # create the next version tag

git push origin v1.1.0             # push the new tag to GitHub

Next: [Lab 7 — Inspection & Utilities](Lab7-Inspection-Utilities.md)
