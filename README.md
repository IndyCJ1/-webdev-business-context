# Lanier Web — Business Context & Handoff

This is the source-of-truth context document for **Lanier Web**, a local web design business in Gainesville, Georgia. Clone this repo and paste the relevant sections into Claude (Claude Code or claude.ai) to continue work from any computer.

## Repo contents

```
README.md                                  ← you are here
templates/
  proposal.md                              ← 1-page proposal sent after discovery
  service-agreement.md                     ← contract template (have GA attorney review)
  client-intake-form.md                    ← post-signing questionnaire
  case-study.md                            ← format for shipping a client win
  portfolio-strategy.md                    ← when/how to swap demos for real work
outreach/
  cold-email-templates.md                  ← 5 cold email templates
  website-audit-template.md                ← free audit deliverable for prospects
  target-list-workflow.md                  ← how to find leads + cadence
ops/
  onboarding-checklist.md                  ← step-by-step from signed → launched
  stripe-and-billing-setup.md              ← invoicing + subscriptions
  monthly-operations.md                    ← weekly/monthly/quarterly tasks
  notion-crm-setup.md                      ← lead/client tracker setup (15 min)
```

---

## The Business

- **Name:** Lanier Web
- **Website:** lanierweb.com
- **Location:** Gainesville, Georgia
- **Operator:** Solo operator (Collier Uesseler)
- **Focus:** Modern websites for local businesses
- **Target clients:** restaurants, gyms, HVAC companies, contractors, barbers, dentists, local service businesses

### Emails
- `collier@lanierweb.com` — owner/personal
- `info@lanierweb.com` — general inbox / contact form recipient
- `billing@lanierweb.com` — invoices, Stripe receipts
- `projects@lanierweb.com` — client project comms

### Packages
- **Starter** — $1,500 + $50/mo — 5-page site, contact form, mobile, basic SEO
- **Plus** — $3,500 + $125/mo — adds blog/CMS, Google Business, monthly edits
- **Pro** — $6,000+ + $300/mo — adds booking/e-commerce, integrations, reports

### Client acquisition
- Walk into local businesses with bad/no websites; show before/after mockup
- Tap personal network for first 1–2 clients
- Pick a niche after 3 clients (restaurants, dentists, HVAC, etc.) for design reuse and referrals
- Cold outreach to outdated/broken sites

---

## Tech Stack

**Current setup (no homelab yet):**
- Sites: **Astro + Tailwind CSS v4** (`@import "tailwindcss"` + `@theme {}`)
- Hosting: **Cloudflare Pages** (free tier, auto-deploys from GitHub on push)
- DNS / SSL / CDN: **Cloudflare** (free tier)
- Forms: **Formspree** (current ID: `mzdojrav` — get a new one per client)
- Domain: lanierweb.com (Cloudflare Registrar)

**Future setup (when paying clients exist):**
```
Internet → Cloudflare (DNS + CDN + Tunnel) → Hetzner CX32 VPS ($7/mo)
                                                    ↓
                                             Ubuntu VM running Docker
                                             ↙    ↓    ↘
                                       Coolify  Gitea  Uptime Kuma
                                           ↓
                                     Client websites
```

**DO NOT use:** WordPress page builders, cPanel, WP Engine, Kinsta, GoDaddy hosting — kills margin and doesn't fit the static-site model.

---

## Design System

- **Primary accent:** `#FF4500` (orange-red)
- **Typography:** Plus Jakarta Sans (Google Fonts)
- **Style:** modern, minimal, clean, premium, mobile-first
- **Colors:** white background, near-black ink (`#0D0D0D`), muted grays for hierarchy
- **Tailwind v4** via `@import "tailwindcss"` + `@theme {}` token block in `global.css`
- **Reveal animations** via IntersectionObserver on `.reveal` class

---

## Copywriting Voice

**Use language that is:** clear · confident · concise · professional · modern · local-business friendly.

**Avoid:** "synergy" · "innovative solutions" · "digital transformation" · "leverage" · "world-class" · exaggerated startup language · corporate buzzwords.

The customer is a small-business owner who wants a website that works and looks professional — write to them like a person, not a Fortune 500 prospect.

---

## What's Already Built

### Agency Site (currently branded "Apex Web" — needs rebrand to Lanier Web)
- **GitHub:** https://github.com/IndyCJ1/cuesseler-web (also reachable as `apex-web` after rename)
- **Live:** https://cuesseler-web.pages.dev
- **Local:** `C:\Users\Collier\repos\cuesseler-web`
- **Sections:** Nav · Hero · Services (numbered cards) · Pricing (3 tiers) · Work (3 demo cards) · About · Contact form · Footer
- **Contact form:** Formspree `mzdojrav`, `_gotcha` honeypot, autocomplete + maxlength on all inputs
- **Security:** `public/_headers` — CSP, HSTS, X-Frame-Options, X-Content-Type-Options, Referrer-Policy, Permissions-Policy, COOP

### Package Detail Pages (inside cuesseler-web)
Each package page embeds an iframe demo with tab navigation to sub-pages:
- `src/pages/packages/starter.astro` — Hogtown Smoke tabs: Home · Menu · Location
- `src/pages/packages/plus.astro` — Perch Coffee Co. tabs: Home · Menu · Blog
- `src/pages/packages/pro.astro` — Solé Wellness tabs: Home · Services · Book

### Demo Sites

**Starter demo — Hogtown Smoke (BBQ restaurant)**
- GitHub: https://github.com/IndyCJ1/hogtown-smoke
- Live: https://hogtown-smoke.pages.dev
- Local: `C:\Users\Collier\repos\hogtown-smoke`
- Separate Astro project. Has its own `public/_headers` with `frame-ancestors` allowing embed from cuesseler-web/apex-web
- Bebas Neue + Inter typography, dark stone palette, Unsplash imagery

**Plus demo — The Perch Coffee Co.**
- Path: `src/pages/demos/plus/` inside cuesseler-web
- Pages: `index.astro` (home) · `menu.astro` · `blog.astro`
- Layout: `src/layouts/PerchLayout.astro`
- Warm cream bg (`#FAF8F5`), Playfair Display, brutalist editorial layout

**Pro demo — Solé Wellness Studio**
- Path: `src/pages/demos/pro/` inside cuesseler-web
- Pages: `index.astro` (home) · `services.astro` · `book.astro`
- Layout: `src/layouts/SoleLayout.astro`
- Sage green (`#EBF2EB`), Cormorant Garamond, dark forest footer, Unsplash images
- Both forms (contact + booking) have honeypot, full label associations, autocomplete, maxlength, preventDefault submit handler

### Mobile Nav
All three layouts now have hamburger mobile nav (PerchLayout, SoleLayout, hogtown-smoke). Toggle via `<script is:inline>` + addEventListener.

---

## Important Technical Rules

1. **No Node/npm locally** — edit source files directly; Cloudflare Pages builds on every git push
2. **Astro scripts need `is:inline`** — `<script is:inline>` for any JS that registers global handlers via addEventListener; default `<script>` is ES module scoped and can't reach inline DOM
3. **No inline event handlers** (`onclick`, `onsubmit`, etc.) — they violate strict CSP and have been removed everywhere
4. **No `gh` CLI** — use direct git commands or `WebFetch` against the GitHub API
5. **Git config per repo:** `git config user.email "collieruesseler23@gmail.com"` and `git config user.name "IndyCJ1"`
6. **Tailwind v4 syntax** — `@import "tailwindcss"` and `@theme {}`; NOT the old `@tailwind base/components/utilities`
7. **All addresses say Gainesville, GA 30501** (not FL/32601)
8. **Static-first architecture** — every site is Astro generating static HTML; no SSR unless absolutely required

---

## Priority Task Status (as of 2026-05-09)

1. ✅ **Rebrand to Lanier Web** — code-side find/replace done; nav, footer, titles, demo attribution all say Lanier Web
2. ✅ **Homepage copy + CTAs** — hero, services, pricing, work, about, contact all rewritten with the voice rules
3. ✅ **SEO + metadata** — full Open Graph, Twitter cards, canonical URLs, JSON-LD LocalBusiness schema, robots.txt, sitemap.xml, favicon, noindex on demos
4. ✅ **Demo realism** — Hogtown phone fixed to (770) area code, address fixed to real Gainesville GA street; Solé booking phone updated
5. ✅ **Proposal + contract templates** — see `templates/proposal.md` and `templates/service-agreement.md`
6. ✅ **Outreach systems** — see `outreach/` (5 cold email templates, free audit deliverable, lead workflow)
7. ✅ **Portfolio presentation** — see `templates/portfolio-strategy.md` (3-stage plan from demos → real case studies)
8. ✅ **First-client prep** — see `ops/` (onboarding checklist, Stripe setup, monthly operations) + `templates/client-intake-form.md`

### What's still to do (post-MVP)

- Point lanierweb.com DNS at Cloudflare Pages (currently still on `cuesseler-web.pages.dev`)
- Set up `info@lanierweb.com` email routing in Cloudflare
- Set up Stripe account + connect business bank account
- File DBA at Hall County clerk
- Create OG image (1200×630 PNG at `/public/og.png`)
- Get the first paying client

---

## Roadmap — Build Process for Each Client

### Phase 1 — Sales & Scoping
1. Identify target client (bad/no website, local business)
2. Mock up before/after concept using one of the existing demo styles
3. Meet/call — ask what they need, who visits, what action they want
4. Send 1-page proposal with package + price
5. Get signed contract + 50% deposit before touching anything

### Phase 2 — Setup
6. Register domain in client's name (Cloudflare Registrar)
7. Scaffold new Astro project from cuesseler-web as template
8. Create staging Cloudflare Pages project from GitHub

### Phase 3 — Build
9. Build layout with placeholder content first — get structure approved
10. Swap in real copy, photos, branding
11. Add contact form (Formspree — get new form ID per client)
12. Mobile responsiveness check
13. Basic on-page SEO (title tags, meta descriptions, alt text, JSON-LD LocalBusiness)

### Phase 4 — Review
14. Send staging link
15. One round of revisions
16. Final approval in writing
17. Collect final 50% before launch

### Phase 5 — Launch
18. Point custom domain in Cloudflare Pages settings
19. Verify SSL is live
20. Submit sitemap to Google Search Console
21. Verify contact form works on live domain
22. Start monthly billing

---

## Cost Breakdown

**Fixed monthly (yours):**
- Hetzner CX32 VPS: $7/mo (after first paying client)
- Backblaze B2: ~$1–2/mo
- Total: **~$9/mo** at most

**Per-client (reimbursed):**
- Domain: $10–12/yr via Cloudflare Registrar

**Free at this scale:**
- Cloudflare (DNS, CDN, SSL, Pages, Email Routing)
- Let's Encrypt SSL

---

## Legal

- **No LLC needed yet** — sole proprietor until 3+ paying clients or one demands it
- **DBA at county clerk** ($20–50) is enough to open a business bank account
- **Written contract for every client** — Bonsai has free templates
- **50% upfront, 50% on launch** — non-negotiable

---

## Picking Up On Another Computer

In a new Claude Code session, paste this prompt:

```
I'm continuing work on my web design business, Lanier Web (Gainesville, GA).
Context repo: https://github.com/IndyCJ1/-webdev-business-context

Key repos:
- Agency site (still named cuesseler-web in GitHub, branded Apex Web in code,
  rebranding to Lanier Web): https://github.com/IndyCJ1/cuesseler-web
  Live: cuesseler-web.pages.dev
- Starter demo (Hogtown Smoke): https://github.com/IndyCJ1/hogtown-smoke
  Live: hogtown-smoke.pages.dev
- Plus demo (Perch) + Pro demo (Solé) live inside cuesseler-web at src/pages/demos/

Local paths: C:\Users\Collier\repos\cuesseler-web and hogtown-smoke

Tech: Astro + Tailwind CSS v4, deployed via Cloudflare Pages (no local Node/npm
on this machine — edits go to source files, Cloudflare builds on push).
Design system: white bg, Plus Jakarta Sans, #FF4500 orange-red accent.
Copy voice: clear, confident, concise — no corporate buzzwords.

Read the README in the context repo for full context, then continue from
where we left off.
```

Then tell Claude what you want to work on.

---

## Asset Manager

Note: There's a separate `asset-manager-main` project with a SQL database. Needs a server — plan is to run in Docker on homelab via Coolify once that infra is set up.
