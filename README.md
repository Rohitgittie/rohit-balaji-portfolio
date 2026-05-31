# Rohit Balaji — Portfolio

Single-page editorial portfolio for [Rohit Balaji](https://linkedin.com/in/rohitbalaji), a multimedia journalist at *The Irish News* in Belfast.

Designed in [Stitch](https://stitch.withgoogle.com/) around Apple's Liquid Glass design language. Built as a single self-contained HTML file — inline CSS, inline vanilla JS, Google Fonts via CDN. No build step, no dependencies.

## Quick start with Claude Code

> **New here?** Paste the line below into a fresh Claude Code session — your session will fork this repo to your GitHub, clone it locally, deploy it to Vercel, and then make customizations alongside you. You'll need the **GitHub** and **Vercel** connectors enabled.
>
> ```
> Fetch https://github.com/theodoreheroldrajan-sketch/rohit-balaji-portfolio, read CLAUDE.md, and follow the Bootstrap.
> ```

## View it

Open `index.html` in any modern browser. Or, for proper local-host behaviour:

```sh
npx serve .
# or
python -m http.server
```

## Edit it

Open this repo in Claude Code (or any LLM coding agent) and chat. The repo contains a `CLAUDE.md` that primes the agent with the design rules so it doesn't accidentally undo the Liquid Glass language.

Things you can ask for:
- "Swap the hero photo with `<file>`"
- "Update the hero copy"
- "Add/remove a work entry"
- "Replace the placeholder video URLs"
- "Add a Download CV button"
- "Tweak the amber accent colour"

## Deploy it

Static site, zero config. Works on Vercel, Netlify, Cloudflare Pages, or GitHub Pages out of the box — just point the host at this repo.

## Structure

```
.
├── index.html                     # whole site lives here
├── assets/
│   ├── hero-bg.jpeg               # background photograph
│   └── rohit-balaji-cv.pdf
├── CLAUDE.md                      # design rules for AI coding agents
└── README.md
```
