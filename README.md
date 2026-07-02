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
- GitHub Pages does **not** require Jekyll. It only kicks in if you don't
  provide your own `index.html`. These are plain static files, served as-is.

## Homepage hero image

The homepage hero (`.hero-video` in `style.css`) is a full-bleed static
image with a dark overlay so light text stays readable — this is the one
dramatic moment on the site. Every other page stays in the plain paper
theme, on purpose: Projects and Freelance are pages people need to *read*,
and a heavy visual fights readability there.

**To add your image:**

1. Create an `assets/` folder in the repo root.
2. Add an image as `assets/hero-poster.jpg` — a good still frame from one
   of your black hole renders works well here.
3. That's it — the CSS already points at that path.

## Upgrading to a video background later

The class is named `.hero-video` because this is designed to become a
looping video hero later without restructuring anything. When you're ready:

1. Render a higher-res clip and compress it — GitHub's hard limit is
   100MB/file, but aim far smaller for load speed, ideally under ~8–10MB:

   ```bash
   # -an strips audio (not needed for a background loop, saves size).
   # crf 28–32 is a reasonable range for something mostly out of focus
   # behind text. Keep the loop itself short — 8–15 seconds is plenty.
   ffmpeg -i original.mp4 -vf "scale=1920:-2" -crf 30 -preset slow -an assets/hero-bg.mp4
   ```

2. In `index.html`, replace the hero's opening comment with:

   ```html
   <video class="hero-bg" autoplay muted loop playsinline poster="assets/hero-poster.jpg">
     <source src="assets/hero-bg.mp4" type="video/mp4">
   </video>
   ```

3. In `style.css`, add back a `.hero-bg` rule (`position: absolute; inset: 0;
   width: 100%; height: 100%; object-fit: cover; z-index: 0;`) and a
   `prefers-reduced-motion` override that hides `.hero-bg` — some visitors
   have that OS setting on and shouldn't be shown autoplaying video.

If the video file is large or you'd rather not commit binary video to the
repo, host it elsewhere (Cloudflare Stream, a Vercel blob, unlisted
YouTube embed) and point `<source>` at that URL instead.
