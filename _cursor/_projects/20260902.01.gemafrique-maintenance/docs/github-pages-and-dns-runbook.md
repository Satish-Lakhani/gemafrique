# Runbook — GitHub Pages + GoDaddy DNS

GitHub username (verified 2026-09-02 via `gh auth status`): **Satish-Lakhani**

Cloud mutations on GoDaddy are **yours to click**. GitHub repo create / Pages enable may already have been done from this session; if not, use the commands below.

## 0. Safety

- Do **not** create or rename anything to `Satish-Lakhani.github.io` — that is the personal site.
- Do **not** edit MX, TXT, or SPF records. Microsoft 365 mail uses `gemafrique-com.mail.protection.outlook.com`.
- Add the custom domain in GitHub **before** changing DNS (takeover hardening). Then change DNS promptly — once the CNAME is attached, `https://satish-lakhani.github.io/gemafrique/` may redirect to gemafrique.com.

## 1. Create the public repo (if it does not exist)

From `/Volumes/Others/Work/c2b/ai/gemafrique`:

```bash
gh repo create Satish-Lakhani/gemafrique --public --source=. --remote=origin --push
```

**Impact:** creates a public repository under your personal account and pushes `main`. Does not change DNS. Does not touch `Satish-Lakhani.github.io`.

## 2. Enable Pages from `main` / root

```bash
gh api repos/Satish-Lakhani/gemafrique/pages -X POST \
  -H "Accept: application/vnd.github+json" \
  -f "build_type=legacy" \
  -f "source[branch]=main" \
  -f "source[path]=/"
```

If that returns 409 (already enabled), skip. Then set the custom domain:

```bash
gh api repos/Satish-Lakhani/gemafrique/pages -X PUT \
  -H "Accept: application/vnd.github+json" \
  -f cname=gemafrique.com
```

**Impact:** GitHub will serve this repo at gemafrique.com once DNS matches. HTTPS “Enforce” often stays grey until DNS + certificate (up to 24h). Tick it in the UI when it unlocks: Repo → Settings → Pages → Enforce HTTPS.

UI equivalent: Settings → Pages → Deploy from a branch → `main` / `/ (root)` → Custom domain `gemafrique.com` → Save.

## 3. GoDaddy DNS (you run this)

Log in at GoDaddy → gemafrique.com → DNS.

**Remove** the existing apex `A` that points at `160.153.0.172` (old host). Remove any `www` record that currently CNAMEs to `gemafrique.com` if it would conflict.

**Add:**

| Type | Name | Value | TTL |
|---|---|---|---|
| A | @ | 185.199.108.153 | 600 |
| A | @ | 185.199.109.153 | 600 |
| A | @ | 185.199.110.153 | 600 |
| A | @ | 185.199.111.153 | 600 |
| AAAA | @ | 2606:50c0:8000::153 | 600 |
| AAAA | @ | 2606:50c0:8001::153 | 600 |
| AAAA | @ | 2606:50c0:8002::153 | 600 |
| AAAA | @ | 2606:50c0:8003::153 | 600 |
| CNAME | www | Satish-Lakhani.github.io | 600 |

Leave MX, TXT, SPF, `MS=`, Google site verification, Outlook records **exactly as they are**.

Sources: GitHub “Managing a custom domain”, fetched 2026-09-02.

## 4. Verify

```bash
dig gemafrique.com +noall +answer -t A
dig www.gemafrique.com +nostats +nocomments +nocmd
dig gemafrique.com MX
curl -sI https://gemafrique.com | head
curl -sI https://satish-lakhani.github.io | head
```

Expect: apex A records = GitHub IPs; `www` CNAME → `Satish-Lakhani.github.io`; MX still Outlook; personal GitHub Pages still 200.
