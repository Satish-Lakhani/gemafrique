---
date: "2026-09-02"
from: jarvis-stone-architect
to: fiona-vale-frontend
project: 20260902.01.gemafrique-maintenance
repo: /Volumes/Others/Work/c2b/ai/gemafrique
status: ready-to-build
---

# Handoff — build the Gem Afrique holding page

Daizy’s spec and Jarvis’s ADR are approved. Implement the static page in this repo. Do not change hosting, DNS, or visual tokens.

## Read in this order

1. [`docs/design-spec.md`](../docs/design-spec.md) — copy, tokens, breakpoints, states, a11y
2. [`plans/ADR-001-github-pages-project-site.md`](../plans/ADR-001-github-pages-project-site.md) — static HTML, relative URLs, 200 not 503
3. This note

## Build

At repo root (not under `_cursor/`):

- `index.html` — semantic one-pager
- `styles.css` — CSS variables from the spec; no leftover hex outside `:root`
- `404.html` — same composition so unknown paths still show the holding message
- `CNAME` — single line `gemafrique.com`
- `favicon.svg` — gem mark, surface + gold

No React, no bundler, no package.json. Google Fonts for Cormorant Garamond + Source Sans 3 with `preconnect`, system fallbacks as specified.

## Constraints

- Relative URLs only (`styles.css`, not `/styles.css`).
- WhatsApp: `https://wa.me/27620506479`
- Local-first: `python3 -m http.server` from the repo root and check 360 / 768 / 1024 before any GitHub push.
- Do not edit MX/DNS. Do not rename the repo to `*.github.io`.

## Done when

The spec’s implementer checklist is ticked, and a local preview shows the quiet-luxury page with a working WhatsApp link.
