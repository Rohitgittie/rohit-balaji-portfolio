# Working on this site

This is Rohit Balaji's portfolio — a single-page editorial site built around Apple's **Liquid Glass** design language, with a fixed black-and-white photograph (a rower on the Lagan in Belfast) as the background.

## Bootstrap (read first if you're a fresh session)

> **AI agent reading this:** if this is the first message in a new session and Rohit dropped this repo's URL or said something like "set this up", "deploy this", or "walk me through this" — run the four steps below in order. Pause and confirm with Rohit between each step. He has the **GitHub** and **Vercel** connectors linked in Claude Code; use them.

### Step 1 — Fork the repo to Rohit's GitHub, then clone it

The canonical source is `theodoreheroldrajan-sketch/rohit-balaji-portfolio`. Rohit needs his own fork so he can push changes.

```sh
gh repo fork theodoreheroldrajan-sketch/rohit-balaji-portfolio --clone --remote
cd rohit-balaji-portfolio
```

`gh repo fork` forks AND clones in one go (the `--clone --remote` flags). If `gh` isn't authenticated yet, run `gh auth login` first and pick GitHub.com → HTTPS → "Login with a web browser". After the clone lands, `cd` into the folder before doing anything else.

### Step 2 — Preview locally

Open `index.html` in Rohit's default browser so he can see what we're starting from:

```sh
# macOS
open index.html
# Windows
start index.html
# Linux
xdg-open index.html
```

Confirm with Rohit: hero photo loaded, glass cards refracting, five sections visible (Hero / Work / Skills & Education / Videos / About & Contact), no broken images. If anything looks wrong, debug before moving on.

### Step 3 — Deploy to Vercel using the Vercel connector

Use the Vercel connector to import the **forked** GitHub repo as a new Vercel project named `rohit-balaji-portfolio`. It's a static site — leave the framework preset as "Other", no build command, no output directory, no install command. Vercel will auto-detect and serve files from the repo root.

Once the first deployment finishes:
- Report the live URL to Rohit (it'll be something like `https://rohit-balaji-portfolio.vercel.app` or a hash-prefixed preview URL).
- Tell him that from now on every `git push` to `main` triggers an automatic redeploy — he never has to redeploy manually.

If he later asks for a custom domain (e.g. `rohitbalaji.com`), it's added in Vercel's project → Settings → Domains; offer to walk him through it.

### Step 4 — Start customizing

The site is live. Ask Rohit what he wants to change first. Common starting points (full details in **Common edits** below):

1. Swap in real video URLs (three placeholders in the Videos section)
2. Update the hero copy (name, role line, statement)
3. Swap the hero photograph
4. Tweak the amber accent colour

After each change: commit on `main`, push, Vercel redeploys automatically (~30s). Confirm the wording of each commit with Rohit before pushing.

---

## File map

- `index.html` — the entire site. Single self-contained file: inline CSS, inline vanilla JS, Google Fonts via CDN, SVG turbulence/displacement filter inline. **All edits stay in this one file.** Don't split into separate CSS/JS files unless explicitly asked.
- `assets/hero-bg.jpeg` — the background photograph. Referenced by `body { background: url(...) }` in the CSS.
- `assets/rohit-balaji-cv.pdf` — Rohit's CV. Not currently linked from the page; can be wired into a "Download CV" button if asked.

## No build step

Open `index.html` directly in a modern browser (Chrome, Safari, Firefox) to see changes. There's nothing to install, no `npm`, no bundler. For local-host testing with proper file:// behavior, `python -m http.server` or `npx serve` works.

## Design rules — do NOT break these

These are lifted from the original design brief. Most "small" visual tweaks risk undoing the Liquid Glass language. Stay inside these lines:

- **Don't replace or alter the hero photograph.** Don't desaturate, colour-grade, regenerate, or substitute it. It's intentionally monochrome 35mm film.
- **Don't apply `saturate()` inside `backdrop-filter`** — the background is greyscale, so saturation does nothing useful and reads as a tell.
- **Don't use solid white cards on a light background.** That's paper, not glass. Glass fill stays at ~10–20% opacity with backdrop blur.
- **Don't fake the glass** with a frosted PNG overlay, inner glow, neon edges, or rainbow gradients.
- **Only one accent colour:** muted amber `#d4a574` (with hover `#e8c79a`). Used for the primary CTA, the link underline, the pulse dot, the story numbers. Don't introduce other accents.
- **No emoji icons.** Use inline SVG (the file already uses Lucide-style stroke SVGs).
- **No other photography.** The hero is the only image on the page.
- **Don't centre-align large blocks of body copy.** Editorial pacing.
- **Section order is fixed:** Hero → Work → Skills & Education → Videos → About & Contact. Don't reorder.
- **Typography is fixed:** Fraunces (serif, headers) + Inter (sans, body). White text on glass.

## Common edits Rohit will ask for

- **Swap the hero photo** → replace `assets/hero-bg.jpeg` with a new file of the same name (or update the `url(...)` in CSS if renaming). Re-check it works behind the glass — if the new photo is high-contrast or colourful, you may need to tweak the bottom-of-viewport overlay opacity in CSS.
- **Change the hero copy** → edit `<h1 class="hero-name">`, `.hero-role`, `.hero-statement` inside `<section class="hero">`.
- **Add/remove a work entry** → `<article class="exp ...">` blocks inside `<div class="exp-list">`. Keep reverse-chronological order. The featured (current-role) one gets `.featured` and the `<div class="stories">` sub-block.
- **Swap in video URLs** → find `<!-- VIDEO 1 URL -->`, `<!-- VIDEO 2 URL -->`, `<!-- VIDEO 3 URL -->` inside `<section id="videos">`. Replace each `<div class="vframe">…</div>` body with a real `<iframe>` (YouTube, Vimeo) or `<video>` element. Keep the `aspect-ratio: 16/9` wrapper.
- **Tweak colours** → the only colour worth tweaking is `--amber: #d4a574` in the `:root` block. Change it once there; it cascades.
- **Add a "Download CV" button** → file is already at `assets/rohit-balaji-cv.pdf`. Add an `<a class="btn" href="assets/rohit-balaji-cv.pdf" download>` next to the existing CTA(s).

## Deployment alternatives

Step 3 of the Bootstrap covers Vercel. The site is also a clean fit for Netlify, Cloudflare Pages, or GitHub Pages — same drill, no build config needed.
