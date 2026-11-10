# CLAUDE.md — Personal Site Project

## What this project is
Single-file personal site for Fabio Marchianò (PhD health biology: genomics and bioinformatics, bioinformatician, freelance AI/automation).
Live at: https://fmarchiano.github.io/masterclass/
Single source of truth: `index.html` (~450 lines, all CSS + JS inline, zero build tools)

Minimalist dark/cream one-pager. No masterclass courses, no i18n, no Cal.com — that content was retired in the Sept 2026 redesign. Three pages: Home, Publications, Where I Am.

## Owner
- Name: Fabio Marchianò
- Email: fabio.marchiano.phd@gmail.com
- GitHub: fmarchiano
- LinkedIn: linkedin.com/in/fabiomarchiano/
- P.IVA: 02856570037 (freelance, IT sole proprietorship)

---

## Absolute rules — NEVER break these

1. **Single file** — everything stays in `index.html`. No separate CSS, JS or HTML files.
2. **Zero frameworks** — vanilla JS only.
3. **Google Fonts is the only CDN** — Jost only. Sole exception: jsDelivr with pinned versions, loaded on first open of the page that needs them: globe.gl, topojson-client, world-atlas for "Where I Am"; three.js for the Publications Viz view. Home loads nothing from it.
4. **Palette**: `--cyan:#00f5ff` · `--b:#0a0a0a` · `--b2:#111114` · `--w:#e8e4d8` · `--dim`/`--dim2` (translucent white). No per-page accents anymore — single page, single accent.
5. **No i18n** — copy is English only. Do not reintroduce `data-i18n` / `T.en` machinery.
6. **Canvas guards** — only canvases are the globe on `page-where` and the Viz object on `page-publications`; `showPage()` pauses each when leaving its page.
7. **Routing** — `showPage(id)` toggles `.active` on `.page` divs. Currently `page-home`, `page-publications` and `page-where`. New pages must follow this pattern and get a nav link.
8. **No lorem ipsum** — all copy must come from `memory/content-bank.md`.
9. **Email CTA** — use `<button onclick="copyEmail()">` (copies address, shows toast). No `mailto:` links, no Cal.com (removed).
10. **Tone** — direct, dry, minimal. No corporate filler ("passionate", "leverage", "cutting-edge").

---

## Architecture quick reference

```
Routing:         showPage(id) — toggles .active on .page divs, updates nav active state
Scroll reveal:   IntersectionObserver on .reveal, threshold 0.08 (see observeReveal())
Email copy:      copyEmail() — clipboard write + toast (#toast-copied)
Grain overlay:   body::before — SVG feTurbulence texture
```

## Key CSS classes

```
.hero                Home hero (name, subtitle)
.about-section        Bio block: photo + bio-body
.bio-grid             Two-col: photo (220px) + bio-body text
.pub-wrap / .pub-card   Publications page — year-grouped list of papers
footer                  Shared footer, LinkedIn/GitHub/Email
#globe / PLACES         "Where I Am" globe. Add a visited country = one entry in the PLACES array (JS)
#viz / VIZ              Publications Viz carousel (default view, toggle to List). Slides, short titles and spot assignments = VIZ array (JS); journal, year, first-author and link are read from the List cards
```

## Files that must exist alongside index.html

```
pic/about.gif        Profile GIF (About section)
pic/about.jpg        Still photo, shown instead when reduced motion is on
```

---

## Memory files (read before editing)

- `memory/design-rules.md` — visual rules, fonts, spacing, palette, tone
- `memory/content-bank.md` — bio, service pitch, publications, contacts
- `memory/site-structure.md` — full section map

## Commands (run with /command-name)

- `/deploy` — git add, commit, push to GitHub
- `/new-section` — scaffold a new section on the home page
