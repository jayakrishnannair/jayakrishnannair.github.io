# How to Write and Publish a New Blog Post

This guide is for internal reference only — it is NOT built or published
by Hugo since it lives at the repo root, outside `content/`.

## 1. Create a new post file

Posts live in `content/posts/`. Name the file with today's date and a
slug, e.g.:

    content/posts/2026-08-16-my-new-post.md

You can create it manually, or use Hugo's helper:

    hugo new posts/2026-08-16-my-new-post.md

## 2. Front matter format

This repo uses TOML front matter (`+++`), matching recent posts:

    +++
    title="My New Post Title"
    author="jayakrishnan"
    date= 2026-08-16T00:00:00+00:00
    categories=["Technology"]
    tags=["tag1","tag2"]

    +++
    <p class="has-drop-cap">
      Your opening paragraph goes here — the drop-cap class gives it
      the large first-letter styling used on other posts.
    </p>

    Regular paragraphs after that need no special markup — just plain
    Markdown.

## 3. Where to upload images

Two options — pick one and stay consistent:

### Option A (matches existing posts): content/wp-content/uploads/
Drop the image file directly into:

    content/wp-content/uploads/your-image.png

Reference it in the post with an ABSOLUTE path from site root:

    ![Alt text](/wp-content/uploads/your-image.png)

This is the pattern "Best Books 2025" and older posts use.

### Option B (Hugo-standard, cleaner going forward): static/images/
Drop the image into:

    static/images/your-image.png

Reference it the same way:

    ![Alt text](/images/your-image.png)

Either works — Hugo copies both `content/wp-content/` and `static/`
contents to the site root on build. Stick with Option A for
consistency with old posts, or start using Option B for new ones if
you want a cleaner folder structure going forward.

## 4. Preview locally before publishing

    hugo server -D

Open http://localhost:1313 in a browser. `-D` includes draft posts
(if you set `draft = true` in front matter) so you can preview before
going live. Stop the server with Ctrl+C when done.

## 5. Publish

Once you're happy with the preview:

    git add content/posts/2026-08-16-my-new-post.md
    git add content/wp-content/uploads/your-image.png   # if you added an image
    git commit -m "Add post: My New Post Title"
    git push origin main

GitHub Actions will automatically:
  1. Build the site with Hugo (hugo --minify)
  2. Deploy it to GitHub Pages

No need to run `hugo --minify` locally or commit the `public/` folder
— that's all handled in CI now.

## 6. Verify it's live

Check the Actions tab to confirm the workflow succeeded:

    https://github.com/jayakrishnannair/jayakrishnannair.github.io/actions

Then visit:

    https://shooonya.org/posts/2026-08-16-my-new-post/

(Deployment usually takes under a minute after a successful push.)

## Quick reference: draft posts

Add `draft=true` (or `draft: true` for YAML front matter) to hold a
post back — `hugo --minify` (used in CI) skips drafts by default, so
it won't be published until you remove that line and push again.
