# Working on this site

This is Rohit Balaji's portfolio — a single-page editorial site built around Apple's **Liquid Glass** design language, with a fixed black-and-white photograph (a rower on the Lagan in Belfast) as the background.

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

## Deployment

The site is static. Drop the repo into Vercel, Netlify, Cloudflare Pages, or GitHub Pages — no config needed. Just point the host at the repo root.
