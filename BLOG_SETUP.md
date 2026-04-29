# Blog Setup Guide

This is a static blog powered by GitHub Pages. All your markdown files in this repo can become blog posts — you control which ones are visible from the admin panel.

---

## Step 1 — Push these files to your repo

Copy all of these files into the root of `Work_small`:

```
index.html        ← blog homepage
post.html         ← individual post viewer
setup.html        ← one-time config generator (not a public page)
config.json       ← blog configuration (you'll replace this)
visibility.json   ← list of published posts (managed by admin panel)
posts/            ← sample post folder (optional structure)
```

---

## Step 2 — Enable GitHub Pages

1. Go to your repo on GitHub → **Settings** → **Pages**
2. Under **Build and deployment**, set **Source** → `Deploy from a branch`
3. Set **Branch** → `main` → `/ (root)` → **Save**

Your blog will be live at:
```
https://indefatigable816.github.io/Work_small/
```

---

## Step 3 — Create a GitHub Personal Access Token

The admin panel needs a token to save visibility changes back to the repo.

1. Go to **GitHub → Settings → Developer settings → Personal access tokens → Fine-grained tokens**
2. Click **Generate new token**
3. Set:
   - **Resource owner**: your account
   - **Repository access**: Only selected → `Work_small`
   - **Permissions → Repository permissions → Contents**: `Read and write`
4. Copy the token (starts with `ghp_` or `github_pat_`)

---

## Step 4 — Generate your config.json

1. Open `setup.html` in any browser (double-click it — `file://` works fine)
2. Fill in:
   - Your blog title and description
   - Repo: `indefatigable816/Work_small`
   - Admin password (choose any password — remember it!)
   - The GitHub PAT from Step 3
   - Giscus settings (optional, see Step 5)
3. Click **Generate config.json**
4. Copy the output and replace the contents of `config.json` in your repo
5. Push to GitHub

Your token is encrypted with your password using AES-256-GCM before being stored in config.json. It cannot be decrypted without your password.

---

## Step 5 — Set up Giscus comments (optional)

Giscus turns GitHub Discussions into a comment system.

1. Go to your repo → **Settings** → **General** → scroll to **Features** → enable **Discussions**
2. Go to [giscus.app](https://giscus.app)
3. Enter your repo name (`indefatigable816/Work_small`)
4. Choose a discussion category (e.g. `General`)
5. Copy the `data-repo-id` and `data-category-id` from the generated script
6. Go back to `setup.html`, paste those values into Step 4, and regenerate `config.json`

---

## Step 6 — Publish your first post

1. Open your live blog: `https://indefatigable816.github.io/Work_small/`
2. Click the **⚙** icon (top right of the header)
3. Enter your admin password
4. Toggle the post(s) you want visible → click **Save changes**
5. Wait ~60 seconds for GitHub Pages to rebuild

---

## Writing posts

Any `.md` file in the repo can be a post. Recommended structure:

```
posts/
  2026-04-29-my-first-post.md
  2026-05-01-another-post.md
```

Add a YAML frontmatter block at the top for title and date:

```markdown
---
title: My Post Title
date: 2026-04-29
---

Post content here…
```

Without frontmatter, the title is derived from the filename and sorted by filename.

---

## How visibility works

- `visibility.json` contains an array of file paths that are **publicly visible**
- Files not in this list are not shown on the blog (they still exist in the repo)
- Only you (with the admin password) can change what's in this list
- Visitors can view posts, leave Giscus comments, and copy the share link — nothing else

---

## Troubleshooting

| Problem | Fix |
|---|---|
| Blog shows "config.json not found" | Push `config.json` to the repo root |
| Admin panel says "Incorrect password" | Re-run `setup.html` with the correct password |
| GitHub API error 401 | Your PAT expired or lacks `Contents: write` permission |
| GitHub API error 403 | The PAT doesn't have access to this repo |
| Comments not showing | Ensure Discussions is enabled and Giscus IDs are correct in config.json |
| Changes take a while | GitHub Pages can take up to 2 minutes to rebuild |
