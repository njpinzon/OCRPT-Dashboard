# OCRPT Case Explorer — standalone build

This is a self-contained, static copy of the OCRPT Case Explorer dashboard,
built to run outside claude.ai (for example on Render or GitHub Pages) so it
can be shared with your team as a plain link.

Everything needed is in this single file:

- `index.html` — the whole app (HTML/CSS/JS, all 30 synthetic cases, and
  all 182 case photos, embedded directly in the file as inline image data).
  There is no separate `sketches` folder to upload — just this one file.

There is nothing to build or install — it's a plain static site with one page.

## Deploy on Render

1. Push this one file to a GitHub repository (see below if you don't have
   one yet) — a single upload, no batching needed.
2. In the Render dashboard: **New +** → **Static Site**.
3. Connect the GitHub repo.
4. Build command: leave blank (nothing to build).
5. Publish directory: `.` (the repo root, since `index.html` is at the top
   level) — or the path to this folder if you put it inside a bigger repo.
6. Deploy. Render will give you a `https://<your-app>.onrender.com` URL —
   that's the link to share with your team.

If you'd rather use GitHub Pages instead of Render, the same folder works
there too: push it to a repo, then enable Pages on that repo pointing at the
branch/root containing `index.html`.

## Getting this folder into a GitHub repo

If you don't already have a repo for this:

1. Go to github.com → **New repository** (e.g. `ocrpt-dashboard`).
2. On your own machine (or wherever you have `git` and this folder), run:
   ```
   cd ocrpt-render-site-single
   git init
   git add .
   git commit -m "OCRPT dashboard — standalone build for Render"
   git branch -M main
   git remote add origin https://github.com/<your-username>/ocrpt-dashboard.git
   git push -u origin main
   ```
3. Then follow the Render steps above.

## What's different from the Claude version

This dashboard was originally built to run inside a Claude artifact, which
gives it two things a plain static site doesn't have automatically:

- **Shared persistence** — on claude.ai, added/edited/removed cases and
  starred addresses are saved to a small server-side store shared by anyone
  who opens the artifact. Outside Claude, this build instead saves that
  same data to **each browser's own localStorage** — it still survives a
  page reload, but it's local to whichever device made the change and
  won't show up for a teammate opening the link on their own computer. The
  page shows a note about this at the bottom of each case when it detects
  it's running outside Claude.
- **File downloads** — the "download attachment" button uses a normal
  browser download outside Claude (no change needed there; it just works).

Everything else — search, filters, add/edit/remove case, the address map,
the photo-metadata (EXIF GPS) prompt, etc. — works exactly the same as the
Claude-hosted version.
