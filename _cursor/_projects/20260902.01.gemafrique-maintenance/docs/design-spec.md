---
title: Gem Afrique maintenance holding page — design spec
author: daizy-bloom-designer
date: "2026-09-02"
status: approved-direction
---

# Design spec — Maintenance Alert

Fiona builds from this. Do not invent palette, type, or layout. Tokens are CSS custom properties in `styles.css`.

## Problem

A visitor hitting gemafrique.com currently gets a dead host. They need to know the brand is alive, that a new site is coming, and how to reach the jeweller **now**. One action: WhatsApp.

## Research (dated 2026-09-02)

| Finding | Source + date | Verdict | Why here |
|---|---|---|---|
| High-ticket jewelry sites put a human line (WhatsApp / “talk to an expert”) ahead of forms | [H&CO Lead Bridge](https://www.itshco.com/blog/high-end-lead-bridge-luxury-website-conversion), read 2026-09-02 | **Adopt** | Matches the brief; we have no backend |
| Quiet-luxury jewelry: dark surface, gold type, restraint | Current jewelry waitlist/coming-soon patterns, read 2026-09-02 | **Adopt** | Brand sells tanzanite/diamonds (archived gemafrique.com copy) |
| WCAG 2.2 AA: 4.5:1 normal text, 3:1 large text and UI | [W3C 1.4.3](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum), 2026-09-02 | **Adopt** | Floor, not a stretch |
| Full-bleed video, waitlist email capture, maximalist neon | 2026 jewelry landing templates | **Ignore** | No assets, no backend, wrong brand |
| WhatsApp-green as the only cue on the button | Common chat-widget fashion | **Ignore** | Meaning must not be hue-only; icon + words |

Direction **A (quiet luxury)** chosen by Satish 2026-09-02. Rejected: daylight boutique; system-minimal.

## Copy

Spelling fix approved in the plan: “Maintanance” → “Maintenance”. Meaning otherwise unchanged.

| Role | Text |
|---|---|
| `<title>` / `og:title` | Maintenance Alert · Gem Afrique |
| Brand | Gem Afrique |
| `h1` | Maintenance Alert |
| Subtitle | We are updating our website, we will soon be back with the new look and feel. |
| CTA | Message on WhatsApp |
| Body | If you need any urgent assistance, please reach out on WhatsApp, on this number — +27 62 050 6479 |
| `href` | `https://wa.me/27620506479` (opens in a new tab, `rel="noopener noreferrer"`) |

No store address. No extra marketing. Long translated strings wrap; they do not truncate.

## Tokens

Named by role. Computed contrast vs `--color-surface` unless noted. Formula: WCAG relative luminance, Python 3.13, 2026-09-02.

| Token | Value | Pairing | Ratio | Bar |
|---|---|---|---|---|
| `--color-surface` | `#12100E` | — | — | page background |
| `--color-surface-raised` | `#1C1A17` | champagne text | 14.91:1 | unused on v1 except if a card is needed |
| `--color-text` | `#F4EDE0` | surface | **16.31:1** | AA AAA body |
| `--color-text-muted` | `#C9BBA8` | surface | **10.09:1** | AA AAA body |
| `--color-accent` | `#C4A574` | surface | **8.12:1** | wordmark, rule, focus ring |
| `--color-cta-fill` | `#C4A574` | `--color-cta-text` `#12100E` | **8.12:1** | default CTA |
| `--color-cta-hover` | `#4A3D6B` | `--color-text` `#F4EDE0` | **8.31:1** | hover/active/focus fill |
| `--font-display` | Cormorant Garamond 600 | Palatino, serif fallback | — | h1 + brand |
| `--font-body` | Source Sans 3 400/600 | system-ui fallback | — | subtitle, contact, CTA |
| `--space-*` | 8px base: 4 / 8 / 16 / 24 / 32 / 48 / 64 / 96 | — | — | all padding/gap |
| `--radius-cta` | 999px | — | — | pill |
| `--focus-ring` | 2px solid accent, 4px offset | 8.12:1 vs surface | — | keyboard only via `:focus-visible` |

Tanzanite `#6B5B95` from the plan sketch **fails as a fill for champagne at ~5:1 on a small control when darkened poorly**; hover uses `#4A3D6B` so champagne stays 8.31:1. Do not use `#6B5B95` as a text color on surface (3.21:1 — fails body).

No dark-mode toggle. The page **is** the dark theme.

## Type scale (mobile-first)

| Step | Size | Weight | Line-height | Use |
|---|---|---|---|---|
| brand | 0.8125rem (13px) | 600 | 1.3 | tracked uppercase wordmark |
| title | `clamp(2.25rem, 8vw, 3.5rem)` | 600 | 1.15 | h1, large text (≥24px) so 3:1 would suffice; we far exceed it |
| lede | `clamp(1.125rem, 2.4vw, 1.25rem)` | 400 | 1.6 | subtitle |
| contact | 1rem (16px) | 400 | 1.6 | body — 16px floor |
| cta | 1.0625rem (17px) | 600 | 1 | button label |

Brand letter-spacing: `0.28em`. Title: `-0.02em`.

## Layout

Breakpoints (project standard): **360 base / 768 / 1024**. Fluid between them. No max-width jail under 20rem.

### 360px (primary)

- `min-height: 100dvh`, column, centered, padding `32px 24px`.
- Content stack max-width `36rem`, horizontally centered.
- Order: skip link → gem mark → brand → gold hairline (64px wide) → h1 → lede → CTA → contact.
- CTA full width of the stack up to `20rem`, then centered as a block. Min height **48px**, horizontal padding 24px, gap 8px to the WhatsApp glyph.
- Contact sits in the lower half of the viewport on typical phones (thumb).
- Worst-case copy (1.5× length): wrap; page may scroll; no overflow-x.

### 768px

- Padding `48px 32px`.
- CTA shrinks to intrinsic width (not full-bleed), still ≥48px tall.
- Hairline 96px.

### 1024px+

- Same structure, more air: padding `64px 48px`.
- Title sits at the clamp max. Do not add a second column.

## States

This page has no data fetch. States that still exist:

| State | Treatment |
|---|---|
| Default | Gold-fill CTA, ink label, WhatsApp glyph currentColor |
| Hover (pointer: fine) | Tanzanite fill `#4A3D6B`, champagne label |
| `:focus-visible` | Same as hover plus 2px gold ring, 4px offset |
| `:active` | Hover colors, `translateY(1px)` — **not** if `prefers-reduced-motion: reduce` |
| Visited | Same as default (do not purple the CTA) |
| 404 | Identical message (same page composition in `404.html`) so stray paths do not look like GitHub’s 404 |

No loading, empty, or error UI.

## Motion

Default: none except the 1px active press. `prefers-reduced-motion: reduce` → no transform.

## Accessibility

- `html lang="en"`
- One `h1`. Brand is a paragraph, not a second heading.
- CTA is an `<a>`, not a `<div>`. Accessible name = visible “Message on WhatsApp”.
- Phone number in the body is the same `wa.me` link (copy-pasteable text).
- Skip link “Skip to WhatsApp” becomes visible on focus.
- Focus order: skip → CTA → phone link. No positive `tabindex`.
- Touch targets ≥48×48px, ≥8px gap.
- `prefers-reduced-motion` honored.
- Decorative gem SVG: `aria-hidden="true"`.
- New-tab links: `rel="noopener noreferrer"` and the accessible name already says WhatsApp (no “opens in new window” required if the destination is named).

## Out of scope

Logo file (none supplied — type lockup only). Store address. Email capture. Analytics. 503 status (GitHub Pages cannot).

## Implementer checklist

- [ ] 360 / 768 / 1024 at real widths, no horizontal scroll
- [ ] Keyboard-only: skip link, CTA, phone link, visible focus
- [ ] `prefers-reduced-motion: reduce` kills the press translate
- [ ] Relative asset URLs (no leading `/`) so project Pages and custom domain both work
- [ ] Contrast tokens unchanged unless a pairing fails — if it fails, change the token here first
