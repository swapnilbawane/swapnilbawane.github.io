# How to Publish a New Post

Quick reference for adding posts to this blog. No local git/Hugo setup needed — everything below works through github.com directly.

## 1. Create the file

Go to `content/posts/` in this repo → **Add file** → **Create new file** → name it `your-post-slug.md` (lowercase, hyphens instead of spaces, no special characters).

## 2. Front matter template

Paste this at the top of the file, then write your post below the closing `---`:

```yaml
---
title: "Your Post Title"
date: 2026-09-06
draft: false
summary: "One or two sentences in your own voice, written to end cleanly — this is what shows on the homepage and in social share previews instead of an auto-truncated excerpt."
cover:
  image: "/images/your-image.jpg"
  alt: "Short description of the image"
---
```

Notes:
- The `cover` block is optional — skip it entirely if the post has no image.
- `date` controls sort order on the homepage (newest first). The single newest post also gets a larger "featured" layout on the homepage — this is automatic, not something you set.
- Always keep `draft: false`, or the post won't build or publish at all.
- Watch YAML indentation under `cover:` — `image:` and `alt:` need to be indented two spaces under it, each on its own line. Don't squeeze them onto one line.

## 3. Adding a photo

- Go to `static/images/` in this repo → **Add file** → **Upload files** (not "Create new file" — that one's for typing text, not uploading binaries).
- Rename the photo to something clean before uploading (`lantern-walkway.jpg`, not the camera's auto filename like `photo_2026-09-06_22-46-30.jpg`).
- Reference it with a leading `/images/...` path in markdown or front matter — Hugo serves everything under `static/` from the site root, so you never write `/static/` in the path.
- **Inline in the post body:** `![alt text](/images/your-image.jpg)` on its own line.
- **As a banner at the top of the post:** use the `cover:` block in front matter instead (see template above).

## 4. Commit

Scroll down on the GitHub edit page, write a short commit message, and commit directly to `main`.

## 5. Check the build

Go to the **Actions** tab and confirm the latest run went green. If it fails, the error log will usually point to a YAML formatting issue (bad indentation, a missing closing quote) or a referenced image file that wasn't actually uploaded — the deeper site config (Hugo version, theme, author field) is already fixed and shouldn't need touching again unless you deliberately change themes or Hugo versions.

---

## What's already fixed (for reference, don't touch unless something breaks)

- **`.github/workflows/hugo.yml`** — uses `peaceiris/actions-hugo@v3`, pinned to Hugo `0.147.0`.
- **`hugo.toml`** — `author = "Swapnil Bawane"` lives as a flat string inside `[params]` (not a nested table, not a separate top-level `[author]` block) — this is the format the PaperMod theme expects for the byline to display correctly.
