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
  notion-crm-setup.md                      ← lead/client tracker setup (15 min)
  active-prospects.md                      ← current mockups in flight (Gainesville HVAC, Fizzy, Canopy + the Roots)
  onboarding-checklist.md                  ← step-by-step from signed → launched
  stripe-and-billing-setup.md              ← invoicing + subscriptions
  monthly-operations.md                    ← weekly/monthly/quarterly tasks
  client-admin-pattern.md                  ← reusable Pages-Functions+KV admin pattern
  fizzy-admin-cloudflare-setup.md          ← Cloudflare bindings for the Fizzy demo admin
```

---

## The Business

- **Name:** Lanier Web
- **Website:** lanierweb.com (live)
- **Location:** Gainesville, Georgia
- **Operator:** Solo operator (Collier Uesseler)
- **Focus:** Modern websites for local businesses
- **Target clients:** restaurants, gyms, HVAC companies, contractors, barbers, dentists, food trucks, local service businesses

### Emails
- `collier@lanierweb.com` — owner/personal
- `info@lanierweb.com` — general inbox / contact form recipient
- `billing@lanierweb.com` — invoices, Stripe receipts
- `projects@lanierweb.com` — client project comms

**Sending email from `@lanierweb.com`:** Recommended path is **Google Workspace ($6/mo)** — best deliverability for cold outreach, real Gmail UI. Free path uses Cloudflare Email Routing for receiving + Brevo SMTP via Gmail "Send mail as" for sending (worse deliverability — fine for low-volume use, expect spam-folder hits on cold sends).

### Packages
- **Starter** — $1,500 + $50/mo — 5-page site, contact form, mobile, basic SEO
- **Plus** — $3,500 + $125/mo — adds blog/CMS, Google Business, monthly edits
- **Pro** — $6,000+ + $300/mo — adds booking/e-commerce, integrations, reports

### Add-ons (proven so far)
- **Client admin page** — $200–$500 one-time for a custom self-service editor on top of Starter (today's location, daily specials, schedule, bookings inbox). See `ops/client-admin-pattern.md`. **Founding-client gift** — include free if it closes the deal.

### Client acquisition
- Walk into local businesses with bad/no websites; show personalized mockup
- Tap personal network for first 1–2 clients
- Pick a niche after 3 clients (restaurants, dentists, HVAC, food trucks, etc.) for design reuse and referrals
- Cold outreach (email + IG DMs for social-only businesses) to outdated/broken sites

---

## Tech Stack

**Current setup (no homelab yet):**
- Sites: **Astro + Tailwind CSS v4** (`@import "tailwindcss"` + `@theme {}`)
- Hosting: **Cloudflare Pages** (free tier, auto-deploys from GitHub on push)
- DNS / SSL / CDN: **Cloudflare** (free tier)
- Forms: **Formspree** (current ID: `mzdojrav` — get a new one per client)
- Backend (when needed): **Cloudflare Pages Functions + KV** — see `ops/client-admin-pattern.md`
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

## Design System (Lanier Web house style)

- **Primary accent:** `#FF4500` (orange-red)
- **Typography:** Plus Jakarta Sans (Google Fonts)
- **Style:** modern, minimal, clean, premium, mobile-first
- **Colors:** white background, near-black ink (`#0D0D0D`), muted grays for hierarchy
- **Tailwind v4** via `@import "tailwindcss"` + `@theme {}` token block in `global.css`
- **Reveal animations** via IntersectionObserver on `.reveal` class

**House style applies to lanierweb.com only.** Each prospect mockup gets its OWN aesthetic matched to their brand — never impose Lanier's palette on a client. Personalized mockups close way faster than generic demos.

---

## Copywriting Voice

**Use language that is:** clear · confident · concise · professional · modern · local-business friendly.

**Avoid:** "synergy" · "innovative solutions" · "digital transformation" · "leverage" · "world-class" · exaggerated startup language · corporate buzzwords.

The customer is a small-business owner who wants a website that works and looks professional — write to them like a person, not a Fortune 500 prospect.

---

## What's Already Built

### Agency Site — Lanier Web
- **GitHub:** https://github.com/IndyCJ1/apex-web (renamed from `cuesseler-web` 2026-05-10; old URL still redirects)
- **Live:** https://lanierweb.com (also still resolves at `cuesseler-web.pages.dev` and `apex-web.pages.dev`)
- **Local:** `C:\Users\Collier\repos\cuesseler-web` (folder kept its original name even after GitHub rename)
- **Sections:** Nav · Hero · Services · Pricing (3 tiers) · Work (3 demo cards) · About · Contact form · Footer
- **Contact form:** Formspree `mzdojrav`, `_gotcha` honeypot, autocomplete + maxlength on all inputs
- **SEO:** JSON-LD LocalBusiness schema on home, OG/Twitter cards, canonical URLs, robots.txt, sitemap.xml, favicon
- **Security:** `public/_headers` — CSP, HSTS, X-Frame-Options, X-Content-Type-Options, Referrer-Policy, Permissions-Policy, COOP

### Package Detail Pages (inside cuesseler-web)
Each package page embeds an iframe demo with tab navigation to sub-pages:
- `src/pages/packages/starter.astro` — Hogtown Smoke tabs: Home · Menu · Location
- `src/pages/packages/plus.astro` — Perch Coffee Co. tabs: Home · Menu · Blog
- `src/pages/packages/pro.astro` — Solé Wellness tabs: Home · Services · Book

### Demo Sites (used in package detail iframes)

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

### Prospect Mockups (real businesses we're pitching)

All under `cuesseler-web/src/pages/mockups/`. Each one matches the prospect's existing brand aesthetic, not Lanier's house style. All `noindex,follow` so they don't compete with the real businesses in search.

**Gainesville HVAC Services** (Starter pitch)
- Path: `src/pages/mockups/gainesville-hvac/` (5 pages: index, services, service-area, about, contact)
- Layout: `src/layouts/GHvacLayout.astro`
- Style: heritage industrial / tradesman editorial, light cool theme, warm copper + cool steel-blue dual accents, Big Shoulders Display + Manrope + JetBrains Mono
- Real Google reviews from their actual GBP
- Live: https://lanierweb.com/mockups/gainesville-hvac/

**Fizzy** (Starter + admin add-on pitch)
- Path: `src/pages/mockups/fizzy/` (single `index.astro` + `admin.astro`)
- Style: matches their Instagram exactly — soft pink, bold black FIZZY logomark, yellow smileys, Polaroid cards, Archivo Black + Caveat + Manrope
- **Backend:** Cloudflare Pages Functions in `functions/api/fizzy/` (login, check-auth, location, menu, bookings) backed by `FIZZY_KV` namespace
- **Admin** at `/mockups/fizzy/admin` — three tabs: Today (location), Menu (full editor), Bookings (inbox of submissions)
- **Time-aware banner** (added 2026-05-10) — parses today's hours and the schedule on the client and flips OPENS LATER / OPEN NOW / CLOSED based on the visitor's clock. Past close, surfaces the next non-booked pop-up from the schedule. Re-checks every minute.
- Live: https://lanierweb.com/mockups/fizzy/
- **Status:** ready to walk in / DM. See `ops/active-prospects.md` for details.

**Canopy + the Roots** (Starter or Plus pitch — build-around approach)
- Path: `src/pages/mockups/canopy-and-the-roots/` (single `index.astro`)
- Style: dual-zone aesthetic — cream/sage upstairs (coffee + yoga), deep forest + ember gold underground (music + comedy), Fraunces (variable serif with italic/soft axes) + Manrope + Caveat
- Sections: hero with upstairs/underground door split, this-week strip, yoga schedule with reserve buttons, underground shows (real upcoming lineup from `/events`), 3-tier membership pricing (aspirational), coffee beans, testimonials, private events, about (story + stat strip), visit with full hours grid (today's row auto-highlights via JS), newsletter, footer
- **Owner:** Hollie Lytle (Founder & CEO). Team named on their About page.
- **Pitch shape (revised 2026-05-10):** v1 is a redesign that wraps around her existing Eventbrite/Google Forms/in-store-membership flows; integrated Stripe + custom admin is Phase 2 upsell. See `ops/active-prospects.md` for the full gap analysis verified across 8 of their pages.
- Live: https://lanierweb.com/mockups/canopy-and-the-roots/
- **Status:** mockup ready, email draft prepared. Dahlonega is 45 min from Gainesville — walk-in feasible.

### Mobile Nav
All three demo layouts and the agency site have hamburger mobile nav. Toggle via `<script is:inline>` + addEventListener.

---

## Important Technical Rules

1. **No Node/npm locally** — edit source files directly; Cloudflare Pages builds on every git push
2. **Astro `<style is:global>`** required for any layout-level CSS that needs to apply to slot-rendered content (page files). Default `<style>` is component-scoped. Verified gotcha: scroll reveals were broken on the HVAC mockup until the layout's style block was made global.
3. **Astro scripts need `is:inline`** — `<script is:inline>` for any JS that registers global handlers via addEventListener; default `<script>` is ES module scoped and can't reach inline DOM
4. **No inline event handlers** (`onclick`, `onsubmit`, etc.) — they violate strict CSP and have been removed everywhere
5. **No `gh` CLI** — use direct git commands or `WebFetch` against the GitHub API
6. **Git config per repo:** `git config user.email "collieruesseler23@gmail.com"` and `git config user.name "IndyCJ1"`
7. **Tailwind v4 syntax** — `@import "tailwindcss"` and `@theme {}`; NOT the old `@tailwind base/components/utilities`
8. **All addresses say Gainesville, GA 30501** (not FL/32601)
9. **Static-first architecture** — every site is Astro generating static HTML. When a client needs editable content, layer **Cloudflare Pages Functions + KV** on top (see `ops/client-admin-pattern.md`).
10. **Cloudflare zone gotcha** — every new domain added to Cloudflare needs Bot Fight Mode OFF and Security Level set to Essentially Off, otherwise Googlebot gets 403'd (see Gotchas section below).

---

## Priority Task Status

### Done (initial agency build, 2026-05-09 to 2026-05-10)
- ✅ Rebrand Apex Web → Lanier Web across codebase
- ✅ Homepage copy + CTAs (voice rules applied)
- ✅ SEO + metadata: full Open Graph, Twitter cards, canonical URLs, JSON-LD LocalBusiness, robots.txt, sitemap.xml, favicon, noindex on demos
- ✅ Demo realism: Hogtown phone/address fixed, Solé booking placeholder updated
- ✅ Proposal + contract templates
- ✅ Outreach systems (cold email templates, audit deliverable, target list workflow)
- ✅ Portfolio strategy + case-study template
- ✅ First-client prep: Stripe + billing setup, onboarding checklist, monthly ops, Notion CRM
- ✅ DNS pointed at Cloudflare Pages — site live at lanierweb.com
- ✅ Cloudflare Bot Fight Mode + Security Level disabled (so Googlebot can crawl)
- ✅ Sitemap submitted to Google Search Console
- ✅ Lanier Web hero responsive fix for laptops (giant "01" no longer overlaps content)
- ✅ Built **Gainesville HVAC** mockup (5-page Starter — heritage industrial style)
- ✅ Built **Fizzy** mockup (Starter + custom admin) with working Pages Functions backend
- ✅ Established the **client-admin pattern** (Pages Functions + KV) — documented for reuse
- ✅ Renamed GitHub repo `cuesseler-web` → `apex-web` (local folder name unchanged; old URL still redirects)
- ✅ Added **time-aware banner** to Fizzy mockup — flips OPENS LATER / OPEN NOW / CLOSED automatically based on visitor's clock, re-checks every minute
- ✅ Built **Canopy + the Roots** mockup (Dahlonega coffee/yoga/music venue) — earthy upstairs + dark underground dual-zone aesthetic, verified gap analysis across 8 of their pages, owner name found (Hollie Lytle), email draft prepared

### Still to do (manual / external)
- Set up Cloudflare Email Routing for the 4 `lanierweb.com` addresses (5 min) — OR sign up for Google Workspace ($6/mo, recommended)
- Set up the FIZZY_KV namespace + FIZZY_PASSWORD secret in Cloudflare so the Fizzy admin can save (5 min — see `ops/fizzy-admin-cloudflare-setup.md`)
- Claim **Google Business Profile** for Lanier Web (highest local-SEO impact)
- Set up Stripe account + connect business bank account
- File DBA at Hall County clerk (~$50)
- Create OG image (1200×630 PNG at `/public/og.png`) — referenced in meta but missing
- GA attorney review of `templates/service-agreement.md` before first use
- **Send the Fizzy email/IG DM and walk into Gainesville HVAC**
- Land the first paying client

---

## Cloudflare zone gotchas (for any domain you add to Cloudflare)

When adding a domain to Cloudflare, two settings default ON that block Googlebot:

1. **Security → Bots → Bot Fight Mode** — must be **OFF**
2. **Security → Settings → Security Level** — must be **Essentially Off**
3. **Security → Settings → Browser Integrity Check** — should be **OFF**

Symptom if any are on: 403 response with `Cf-Mitigated: challenge` header. Google Search Console will report "invalid sitemap" or "couldn't fetch." Apply this same fix to any future client domain pointed at Cloudflare.

---

## Roadmap — Build Process for Each Client

### Phase 1 — Sales & Scoping
1. Identify target client (bad/no website, local business)
2. Build a **personalized mockup** at `lanierweb.com/mockups/<slug>/` matching their existing brand
3. Walk in, hand them your phone, *"I built this for you"*
4. Don't talk while they scroll
5. Quote after they've seen it. Send 1-page proposal
6. Get signed contract + 50% deposit before touching production

### Phase 2 — Setup
7. Register domain in client's name (Cloudflare Registrar)
8. Clone the mockup repo to a fresh `lanier-<slug>` repo
9. Strip the `/mockups/<slug>/` prefix from internal links
10. Create new Cloudflare Pages project from GitHub
11. **Disable Bot Fight Mode + Security Level** on the new zone (see Gotchas)

### Phase 3 — Build
12. Polish layout with the real intake-form data
13. Add contact form (Formspree — get new form ID per client)
14. If admin add-on sold, copy the Functions + KV pattern (see `ops/client-admin-pattern.md`)
15. Mobile responsiveness check
16. Basic on-page SEO (title tags, meta descriptions, alt text, JSON-LD LocalBusiness)

### Phase 4 — Review
17. Send staging link
18. One round of revisions
19. Final approval in writing
20. Collect final 50% before launch

### Phase 5 — Launch
21. Point custom domain in Cloudflare Pages settings
22. Verify SSL is live
23. Submit sitemap to Google Search Console
24. Verify contact form works on live domain
25. Hand over admin URL + password if applicable
26. Start monthly billing

---

## Cost Breakdown

**Fixed monthly (yours):**
- Hetzner CX32 VPS: $7/mo (after first paying client)
- Backblaze B2: ~$1–2/mo
- Total: **~$9/mo** at most
- Optional: Google Workspace $6/mo for `@lanierweb.com` email

**Per-client (reimbursed):**
- Domain: $10–12/yr via Cloudflare Registrar

**Free at this scale:**
- Cloudflare (DNS, CDN, SSL, Pages, Pages Functions, KV, Email Routing)
- Let's Encrypt SSL

---

## Legal

- **No LLC needed yet** — sole proprietor until 3+ paying clients or one demands it
- **DBA at county clerk** ($20–50) is enough to open a business bank account
- **Written contract for every client** — Bonsai has free templates, OR use `templates/service-agreement.md` (have GA attorney review first)
- **50% upfront, 50% on launch** — non-negotiable

---

## Picking Up On Another Computer

In a new Claude Code session, paste this prompt:

```
I'm continuing work on my web design business, Lanier Web (Gainesville, GA).
Site is live at lanierweb.com.

Context repo: https://github.com/IndyCJ1/-webdev-business-context
Read the README first — it's the source of truth for everything.

Key code repos:
- Agency site (apex-web on GitHub, lanierweb.com live, local folder still cuesseler-web):
  https://github.com/IndyCJ1/apex-web
- Starter demo (Hogtown Smoke):
  https://github.com/IndyCJ1/hogtown-smoke

The agency repo also contains:
- Plus + Pro demos at src/pages/demos/
- Active prospect mockups at src/pages/mockups/ (Gainesville HVAC, Fizzy, Canopy + the Roots)
- Cloudflare Pages Functions for client admins at functions/api/

Local paths: C:\Users\Collier\repos\cuesseler-web and hogtown-smoke

Tech: Astro + Tailwind v4, deployed via Cloudflare Pages (no local Node/npm).
Per-client admin pattern uses Cloudflare Pages Functions + KV.

Design house style for lanierweb.com itself: white bg, Plus Jakarta Sans,
#FF4500 accent. Per-prospect mockups get their OWN aesthetic matched to
the prospect's brand — see ops/active-prospects.md.

Copy voice: clear, confident, concise — no startup buzzwords.

Tell Claude what you want to work on.
```

---

## Asset Manager

Note: There's a separate `asset-manager-main` project with a SQL database. Needs a server — plan is to run in Docker on homelab via Coolify once that infra is set up.
