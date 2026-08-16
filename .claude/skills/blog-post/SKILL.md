---
name: blog-post
description: Use this skill when the user asks to write, draft, create, or publish a new blog post for shooonya.org (this Hugo repo). Covers front matter format, image handling, local preview, and the git commit/push flow that triggers GitHub Actions deployment.
---

# Writing and Publishing a Blog Post on shooonya.org

This repo is a Hugo static site (theme: PaperMod) deployed to
shooonya.org via GitHub Pages. Deployment is fully automated through
GitHub Actions — pushing to `main` triggers a build and deploy. There
is no manual build or upload step.

## Step 1: Gather the post content

If the user provides the content directly (pasted text, a doc, a
LinkedIn post, etc.), use it as-is with light cleanup (fix
straight-quote/smart-quote issues, remove platform-specific UI text
like "Edit article" or share-button labels).

If the user asks you to write the post from a topic/outline, draft it
in a similar voice to existing posts in `content/posts/` — check 2-3
recent ones for tone before writing.

Before writing anything, check whether a very similar post already
exists in `content/posts/` (search titles and key phrases). Do not
create a near-duplicate post — if similar content already exists,
tell the user and ask whether they want to update the existing post
instead.

## Step 2: Create the post file

Path: `content/posts/YYYY-MM-DD-slug.md`, where the date is today's
date (or the date the user specifies) and the slug is a short
lowercase-hyphenated version of the title.

Use TOML front matter (matches the rest of this repo):

```
+++
title="Post Title Here"
author="jayakrishnan"
date= YYYY-MM-DDT00:00:00+00:00
categories=["Category"]
tags=["tag1","tag2"]

+++
<p class="has-drop-cap">
  Opening paragraph text goes here.
</p>

Rest of the post in plain Markdown. Use ### for section headers if
the post has multiple distinct topics/sections (see
content/posts/best-books-2025.md for an example of this pattern).
```

Pick 1-3 tags and one category that fit the content. Look at existing
posts for the category vocabulary already in use (e.g. "Technology",
"Self Improvement", "Conferences") rather than inventing new ones.

## Step 3: Handle images

If the user provides an image (upload, URL, or asks you to generate
one):

1. Save/download it into `content/wp-content/uploads/<filename>.png`
   (this matches the existing convention used by other posts — do not
   use `static/images/` unless the user asks for that specifically).
2. Reference it in the post with an ABSOLUTE path from site root:
   `![Alt text](/wp-content/uploads/<filename>.png)`
3. Never use a relative path like `../../content/...` — this breaks
   because Hugo's page bundle URL structure doesn't resolve relative
   paths the way you'd expect. Always use the absolute `/wp-content/...`
   form.
4. If reusing an image already hosted elsewhere (e.g. a CDN URL from
   an old post), you can link directly to that external URL instead
   of re-hosting, as long as it's confirmed reachable
   (`curl -sI <url>` should return 200).

## Step 4: Preview locally (if a local Hugo environment is available)

```bash
hugo server -D
```
Visit http://localhost:1313 and check the post renders correctly,
especially the image and any links. Stop with Ctrl+C.

If no local Hugo is available in the current environment, skip
preview and rely on the GitHub Actions build to catch errors (check
step 6).

## Step 5: Commit and push

Do NOT run `hugo --minify` or commit the `public/` folder — GitHub
Actions builds the site in CI on every push. Only commit source
files:

```bash
git add content/posts/YYYY-MM-DD-slug.md
git add content/wp-content/uploads/<filename>.png   # if an image was added
git commit -m "Add post: <Post Title>"
git push origin main
```

## Step 6: Verify deployment

Check the Actions run succeeded:
```
https://github.com/jayakrishnannair/jayakrishnannair.github.io/actions
```

Once green, confirm the post is live:
```bash
curl -sI "https://shooonya.org/posts/YYYY-MM-DD-slug/"
```
Should return `HTTP/2 200`. If it 404s, wait ~30-60s for propagation
and retry before troubleshooting further.

## Notes / gotchas learned from this repo's history

- `baseURL` in `config.toml` must be `https://shooonya.org/` — do not
  let it drift back to `jayakrishnannair.github.io` (both domains
  work, but shooonya.org is canonical).
- `.nojekyll` must exist at repo root — without it, GitHub Pages runs
  Jekyll and serves the wrong content entirely.
- To hold a post back from publishing, add `draft=true` to the front
  matter — the CI build skips drafts automatically.
