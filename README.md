# TDog Taekwondo — website

Static website for TDog Taekwondo. Plain HTML, no build step, no framework.
Hosted on GitHub Pages (or Cloudflare Pages) at tdogtaekwondo.com.

## Structure
- `index.html` and the other `*.html` files are the pages.
- `assets/media/` — shared images and the two short video clips.
- `assets/gallery/` — the full gallery photo set.
- `TDog-Schools-*.pdf` — the two school info packs (linked from the For Schools page).
- `CNAME` — the custom domain. `.nojekyll` — tells the host to serve files as-is.

## How to edit

**Change text (a price, a headline, results):**
Open the page's `.html` file here on GitHub, click the pencil (Edit) icon,
change the words between the tags, then "Commit changes". The live site
updates in a minute or two.

**Swap a photo:**
Upload the new image into `assets/media/` (or `assets/gallery/`), then either
give it the same filename as the one you're replacing, or update the filename
in the relevant `.html` file.

**Bigger changes:**
Send them over and you'll get updated files to drop in.

Nothing here needs to be "compiled" — what you see in the files is what the
site serves.
