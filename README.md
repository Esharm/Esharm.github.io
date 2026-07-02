# Personal site

Plain HTML/CSS, no build step, no JS framework. 4 files total.

```
index.html      Home page (bio + hero)
projects.html   Project writeups (MCM, black hole imaging)
freelance.html  Services + contact
style.css       All styling — colors, fonts, spacing
```

## Deploying with GitHub Pages

1. Create a repo named `yourusername.github.io` (this exact name enables
   free hosting at that URL automatically), or use any repo name and enable
   Pages in Settings → Pages → deploy from a branch.
2. Put these 4 files in the repo root.
3. Push to `main`. The site goes live at `https://yourusername.github.io`
   within a minute or two.
4. Optional custom domain: buy a domain, add a `CNAME` file to the repo
   containing just the domain name, and point your domain's DNS to GitHub
   Pages (GitHub's docs walk through the exact records to add).

## Editing content

Every place you need to fill in real content is marked `[Edit: ...]` in the
HTML. Search each file for `[Edit` to find them all.

## Editing style

Everything visual is controlled from the top of `style.css`, in the
`:root { ... }` block:

- **Colors** — `--bg`, `--ink`, `--muted`, `--accent`, `--signal` etc.
  Change a hex value, it updates everywhere that variable is used.
- **Fonts** — `--font-display` (headings), `--font-body` (paragraphs),
  `--font-mono` (labels, nav, tags). Currently Fraunces / IBM Plex Sans /
  IBM Plex Mono, loaded via Google Fonts in each HTML file's `<head>`. To
  swap fonts: change the Google Fonts `<link>` in all three HTML files,
  and update the variable names in `style.css` to match.
- **Layout width** — `--max-width` controls how wide the content column is.

The rest of the CSS is organized in labeled sections (NAV, HERO, PROJECT
CARDS, etc.) matching the parts of the page they style, so you can jump to
the relevant block instead of reading top to bottom.

## Notes

- No JavaScript — nothing to break, nothing to debug. If you want a mobile
  nav toggle or any interactivity later, it can be added as a small
  `script.js` without touching the rest.
- The faint concentric-ring pattern in the homepage hero is pure CSS
  (`background-image` in the `.hero` rule) — a quiet nod to contour plots /
  iso-lines. Delete that block if you'd rather have a plain background.
