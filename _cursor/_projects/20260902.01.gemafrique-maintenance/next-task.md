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
- **Goal**: `https://gemafrique.com` serves the quiet-luxury page with WhatsApp CTA; Microsoft 365 email still works; personal `satish-lakhani.github.io` untouched.
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
- **Last Activity**: 2026-09-02 (Session 1, jarvis-stone-architect + daizy-bloom-designer + fiona-vale-frontend in one chat) — Page is built and pushed. GitHub Pages is live with the custom domain *configured* but GoDaddy still points at the cancelled host, so gemafrique.com is still dead until Satish updates A/AAAA/www.
- **Status**: Active 🟢

**Current step:**
- ✅ Project initialized (2026-09-02)
- ✅ Design spec + ADR-001 + Fiona handoff
- ✅ Static page (index, styles, 404, CNAME) — local 200 on :4173; contrast computed
- ✅ Public repo + Pages from `main` / root + CNAME `gemafrique.com`
- ✅ Personal GitHub Pages still 200
- 🔴 GoDaddy DNS not changed — unblock: Satish logs into GoDaddy and applies the runbook table (A/AAAA/www only)
- 🔵 Next: Satish runs GoDaddy DNS from `docs/github-pages-and-dns-runbook.md`, then Enforce HTTPS in repo Settings → Pages

### ✅ COMPLETED: Holding page build + GitHub Pages (2026-09-02)

**Delivered:** Quiet-luxury one-pager at `/Volumes/Others/Work/c2b/ai/gemafrique`; public repo; Pages built.  
**Decisions:** Project repo (not user site); quiet luxury; spelling “Maintenance”.  
**Validation:** `curl` local 200; `gh` Pages `status=built`; personal site 200; MX unchanged. gemafrique.com HTTPS **not** verified — DNS still old.  
**Files:** `index.html` `styles.css` `404.html` `CNAME` `favicon.svg` + `_cursor/` docs.  
**Changelog:** `changelogs/001-holding-page-build.md`

## Objectives for Next Session

- **A (Recommended):** Apply the GoDaddy table, wait for propagation, tick Enforce HTTPS, confirm `https://gemafrique.com` and WhatsApp.
- **B:** Hand the live page to Reva Hawke for a design/a11y review before DNS.
- **C:** Transfer the repo to the friend’s GitHub account after DNS is stable.
