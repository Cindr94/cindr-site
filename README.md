# Cindr Group LLC — Marketing Site

A static, single-page marketing site for Cindr Group LLC, a procurement and supply
partner for government buyers. No build step, no backend, no dependencies.

## Structure

```
index.html              Single-page site (hero, capabilities, about, differentiators, contact)
404.html                Simple not-found page
robots.txt / sitemap.xml
assets/css/styles.css   All styling (design tokens at the top of the file)
assets/js/main.js       Mobile nav toggle + footer year
assets/img/favicon.svg  Favicon (abstract ember mark, no literal flame/imagery)
vercel.json             Vercel config (clean URLs, asset caching)
netlify.toml            Netlify config (publish dir, asset caching, 404 redirect)
```

## Local preview

No build step required. Serve the directory with any static file server, e.g.:

```
npx serve .
# or
python3 -m http.server 8080
```

Then open the printed local URL in a browser.

## Deploy

### Vercel
1. Import this repository in the Vercel dashboard, or run `vercel` from this
   directory with the Vercel CLI.
2. Framework preset: **Other** / static site. No build command, output
   directory is the repo root (`.`).
3. `vercel.json` is already configured for clean URLs and long-lived asset
   caching — no further setup needed.

### Netlify
1. Import this repository in the Netlify dashboard, or run `netlify deploy`
   from this directory with the Netlify CLI.
2. Build command: none. Publish directory: `.` (already set in `netlify.toml`).

### Any static host
The site is plain HTML/CSS/JS with root-relative asset paths (`/assets/...`).
It can be dropped onto any static host (S3 + CloudFront, GitHub Pages, etc.)
as-is.

## Design decisions made without explicit direction

A few calls were made to keep this moving without blocking on questions.
Documented here so they're easy to revisit:

- **Palette**: deep charcoal (`#14110f`/`#1b1613`) base, a single warm ember
  accent (`#d9642c`, lighter `#f0964f` for text-on-dark use), off-white body
  text. No literal flame or cheese imagery anywhere, including the favicon
  (an abstract gradient square).
- **Typography**: system font stack (`-apple-system, Segoe UI, Roboto, Inter,
  sans-serif`) rather than a hosted/embedded webfont, to keep the site
  dependency-free and fast (no external requests, no font-loading flash).
- **Copy for differentiators/capabilities**: written as reasonable placeholder
  copy consistent with the brief (single accountable contract partner,
  compliance/on-time delivery, vetted supplier network, responsive
  communication). Should be reviewed and refined with real Cindr Group
  positioning/proof points before this goes live to procurement contacts.
- **Contact/company facts shown**: email (`alex@cindrgroup.com`, as a `mailto:`
  link), UEI `Y7DQEFDR9S95`, "SAM.gov: Registered," and "Wyoming LLC." No
  phone number, physical address, or CAGE code was provided, so none is
  shown — add these to the contact section and structured data
  (`index.html`, the `Organization` JSON-LD block) once available.
- **No CMS/backend**: content lives directly in `index.html`. If this needs
  to be editable by non-developers later, the natural next step is a small
  static-site generator or a headless CMS feeding a build step — not needed
  at this stage.
- **Accessibility**: skip-to-content link, semantic landmarks, visible focus
  states, `aria-expanded`/`aria-controls` on the mobile nav toggle, and
  `prefers-reduced-motion` support are all included.
- **404 handling**: a plain `404.html` is included and wired up for Netlify;
  Vercel serves it automatically for unmatched routes on static deployments.

## Updating content

All copy lives in `index.html`. Section order and IDs (`#capabilities`,
`#about`, `#differentiators`, `#contact`) are referenced by the nav in both
the header and footer — keep IDs in sync if sections are renamed or reordered.
