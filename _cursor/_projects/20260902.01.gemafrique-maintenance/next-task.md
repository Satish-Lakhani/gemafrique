# Next Task: 20260902.01.gemafrique-maintenance

> **Drag this file into any AI chat to resume this project.**
> Owner: jarvis-stone-architect

## Rules of Engagement — read first

1. **Become the owner.** Activate Jarvis via `Full-AI-Skills/agents/jarvis-stone-architect/hello.md`.
2. **Gather context silently.** Read ALL files in `changelogs/`, this file, `plans/README.md`.
3. **Present status as the owner.** Overall objective → what's completed → what's pending → what you propose now.
4. **Present options** as `A (Recommended): … / B: … / C: …`.
5. **Wait for direction.** Never auto-execute cloud/DNS.
6. **Plans are a reference, not a script.** Re-derive against live DNS each session.

## Project

- **Description**: Temporary maintenance holding page for gemafrique.com on a GitHub Pages project repo.
- **Goal**: `https://gemafrique.com` serves the **approved royal jewelry-box** holding page with WhatsApp CTA; Microsoft 365 email still works; personal `satish-lakhani.github.io` untouched.
- **Tech stack**: static HTML/CSS, GitHub Pages, GoDaddy DNS
- **Components**: `/Volumes/Others/Work/c2b/ai/gemafrique`

## Key Project Knowledge

- GitHub user: `Satish-Lakhani`. Repo: https://github.com/Satish-Lakhani/gemafrique (public). Must **not** be named `*.github.io`.
- Pages is **built** (2026-09-02) with `cname=gemafrique.com`, `custom_404=true`, `https_enforced=false` until DNS + cert.
- `https://satish-lakhani.github.io/gemafrique/` **301s to** `http://gemafrique.com/` (GitHub custom-domain redirect). Preview that URL only after DNS, or use local `python3 -m http.server 4173`.
- Personal site `https://satish-lakhani.github.io/` still **HTTP 200** after Pages enable (verified 2026-09-02).
- Apex `A` still `160.153.0.172` (old host). MX still Outlook — **do not touch MX/TXT**.
- DNS runbook: [`docs/github-pages-and-dns-runbook.md`](docs/github-pages-and-dns-runbook.md)
- Design spec: [`docs/design-spec.md`](docs/design-spec.md) · ADR: [`plans/ADR-001-github-pages-project-site.md`](plans/ADR-001-github-pages-project-site.md)
- Contrast (2026-09-02): champagne/surface 16.31:1; muted/surface 10.09:1; CTA ink-on-gold 8.12:1; hover champagne-on-tanzanite `#4A3D6B` 8.31:1.

## Current Status

- **Created**: 2026-09-02
- **Last Activity**: 2026-09-02 16:51 SAST (Session 1 checkpoint) — Royal jewelry-box page is approved and pushed (`66a23aa`). Custom domain is already set on GitHub Pages. **Next chat is DNS only:** point gemafrique.com at GitHub at GoDaddy, then Enforce HTTPS. Do not restyle.
- **Status**: Active 🟢

**Current step:**
- ✅ Project initialized (2026-09-02)
- ✅ Design spec + ADR-001 + Fiona handoff
- ✅ Static page on GitHub Pages project repo `Satish-Lakhani/gemafrique` (not the user site)
- ✅ Satish approved royal jewelry-box restyle (larger gem, WhatsApp green `#25D366` + dark label, copy reorder, gem-block animation)
- ✅ Personal GitHub Pages still 200 (`https://satish-lakhani.github.io/`)
- 🔴 GoDaddy DNS not changed — apex `A` still `160.153.0.172`; MX still Outlook
- 🔵 Next: walk Satish through GoDaddy A/AAAA/www from the runbook; then Enforce HTTPS; verify `https://gemafrique.com`

### ⏸ CHECKPOINT (2026-09-02 16:51 SAST)

- **Exactly where work stopped:** design approved. GitHub Pages `cname=gemafrique.com`, `https_enforced=false`. No GoDaddy clicks yet.
- **In-flight:** uncommitted local edit in `styles.css` — `.jewel-card { border-radius: 1.5rem; }` plus formatting. Ask Satish whether to commit/push before DNS.
- **Rejected:** v1 quiet-luxury (too flat, gem too small). White type on WhatsApp green (1.98:1).
- **Do not:** touch MX/TXT/SPF; rename anything to `*.github.io`; redesign the page.
- **First action for the next chat:** Read `docs/github-pages-and-dns-runbook.md`, confirm live `dig gemafrique.com A` still shows `160.153.0.172`, then hand Satish the GoDaddy table to apply.

### ✅ COMPLETED: Royal restyle (2026-09-02)

**Delivered:** Velvet burgundy jewelry-box page; faceted `mark.svg`; WhatsApp-green CTA; assistance line above the button; “revamping” copy.  
**HEAD:** `66a23aa`  
**Changelog:** `changelogs/001-holding-page-build.md` (build) · `changelogs/002-checkpoint-dns-handoff.md` (this hop)

## Objectives for Next Session

- **A (Recommended):** Apply GoDaddy A/AAAA/www from the runbook, wait for propagation, tick Enforce HTTPS, confirm `https://gemafrique.com` and that `https://satish-lakhani.github.io/` is still 200.
- **B:** Commit/push the uncommitted `border-radius` first, then do A.
- **C:** After HTTPS is live, optional Reva review.
