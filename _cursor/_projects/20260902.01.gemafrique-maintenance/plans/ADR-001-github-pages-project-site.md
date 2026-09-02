---
adr: 001
title: Host the Gem Afrique holding page on a GitHub Pages project site
date: "2026-09-02"
status: accepted
deciders: satish, jarvis-stone-architect
---

# ADR-001: GitHub Pages project site for gemafrique.com

## Context

The WordPress host for gemafrique.com was cancelled. The domain remains at GoDaddy (`ns07`/`ns08.domaincontrol.com`). Apex `A` still pointed at `160.153.0.172` (2 Sep 2026). Microsoft 365 email is live (`MX` → `gemafrique-com.mail.protection.outlook.com`). There is no application server. Satish already has a personal GitHub Pages user site and must not lose it. Budget is zero.

## Options considered

- **A — GitHub Pages project repository** (`Satish-Lakhani/gemafrique`, not `Satish-Lakhani.github.io`) with custom domain `gemafrique.com`. DNS: apex `A`/`AAAA` to GitHub IPs, `www` CNAME to `Satish-Lakhani.github.io`. MX/TXT unchanged.
- **B — GitHub Organization site** — cleaner long-term ownership for a friend’s brand; extra account and transfer later.
- **C — Cloudflare Pages** — stronger ToS for a commercial brand and unmetered bandwidth; apex usually wants Cloudflare nameservers, which means recreating MX/SPF and a larger blast radius on email.

## Decision

**A.** User confirmed 2 Sep 2026.

GitHub’s published rule (docs fetched 2 Sep 2026): a custom domain on the *user* site prefixes all project URLs. A custom domain on **this** project repo only binds gemafrique.com. The user site stays at `https://satish-lakhani.github.io`.

Stack is a single static `index.html` — no framework. GitHub Pages cannot emit HTTP 503; the holding page is a 200.

## Consequences

- **Cost:** $0 now and at 10× this traffic. Soft Pages limit 100 GB/month / 1 GB site size — irrelevant for a one-pager.
- **Email:** safe if GoDaddy MX/TXT are not edited.
- **ToS:** Pages is not for ecommerce. A static notice + WhatsApp link is not checkout; revisit if the next site is a shop.
- **Exit:** change `A` records; HTML is portable to any static host.
- **Order:** add the custom domain in the repo Pages settings **before** DNS, to reduce domain-takeover risk. Then Enforce HTTPS (certificate can take up to 24h).
- **Preview until DNS:** `https://satish-lakhani.github.io/gemafrique/` — once the custom domain is attached, GitHub may redirect this URL to gemafrique.com, so DNS should follow immediately.

## Revisit trigger

Revisit if the next site is ecommerce, if GitHub flags the commercial-use policy, or if the friend wants the repo under their own account/org.

## Sources

- [About custom domains and GitHub Pages](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages) — fetched 2026-09-02
- [Managing a custom domain](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site) — fetched 2026-09-02
- [GitHub Pages limits](https://docs.github.com/en/pages/getting-started-with-github-pages/github-pages-limits) — fetched 2026-09-02
