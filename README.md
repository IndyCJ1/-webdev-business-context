# Web Dev Business — Context & Handoff

This is a context document for picking up the web dev business plan from any computer. Clone this repo and paste the relevant sections into Claude (Claude Code or claude.ai) to continue where you left off.

---

## The Business

**Name:** Apex Web — local web design business in Gainesville, **GA**.

Build websites for local businesses and host them on a monthly retainer. Recurring revenue model.

**Packages:**
- **Starter** — $1,500 + $50/mo — 5-page site, contact form, mobile, basic SEO
- **Plus** — $3,500 + $125/mo — adds blog/CMS, Google Business, monthly edits
- **Pro** — $6,000+ + $300/mo — adds booking/e-commerce, integrations, reports

**Client acquisition:**
- Walk into local businesses with bad/no websites, show before/after mockup
- Tap personal network for first 1–2 clients
- Pick a niche after 3 clients (dentists, HVAC, gyms) for design reuse and referrals
- Cold outreach to outdated/broken sites

---

## Tech Stack

**Current setup (no homelab yet):**
- All sites: **Astro + Tailwind CSS v4** (`@import "tailwindcss"` + `@theme {}`)
- Hosting: **Cloudflare Pages** (free tier, auto-deploys from GitHub)
- Forms: **Formspree** (ID: `mzdojrav`)
- DNS/CDN/SSL: Cloudflare (free tier)

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

**DO NOT use:** cPanel, WP Engine, Kinsta, GoDaddy hosting — kills margin.

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

## What's Already Built

### Agency Site (Apex Web)
- **GitHub:** https://github.com/IndyCJ1/cuesseler-web
- **Live:** https://cuesseler-web.pages.dev
- **Local:** `C:\Users\Collier\repos\cuesseler-web`
- **Design:** White bg, Plus Jakarta Sans font, `#FF4500` orange-red accent, clean/modern
- **Sections:** Nav, Hero, Services (numbered cards), Pricing (3 tiers), Work (3 demo cards), About, Contact form, Footer
- **Contact form:** Formspree ID `mzdojrav`, `_gotcha` honeypot field included
- **Security:** `public/_headers` — CSP, HSTS, X-Frame-Options, X-Content-Type-Options, Referrer-Policy, Permissions-Policy, COOP

### Package Detail Pages (inside cuesseler-web)
Each package page has an iframe demo + tab navigation to sub-pages:
- `src/pages/packages/starter.astro` — Hogtown Smoke demo tabs: Home, Menu, Location
- `src/pages/packages/plus.astro` — Perch Coffee Co. demo tabs: Home, Menu, Blog
- `src/pages/packages/pro.astro` — Solé Wellness demo tabs: Home, Services, Book

### Demo Sites

**Starter Demo — Hogtown Smoke (BBQ restaurant)**
- GitHub: https://github.com/IndyCJ1/hogtown-smoke
- Live: https://hogtown-smoke.pages.dev
- Local: `C:\Users\Collier\repos\hogtown-smoke`
- Separate Astro project

**Plus Demo — The Perch Coffee Co.**
- Path: `src/pages/demos/plus/` inside cuesseler-web
- Pages: `index.astro` (home), `menu.astro`, `blog.astro`
- Layout: `src/layouts/PerchLayout.astro`
- Design: Warm cream bg (`#FAF8F5`), Playfair Display font, dark brown/gold palette, brutalist editorial

**Pro Demo — Solé Wellness Studio**
- Path: `src/pages/demos/pro/` inside cuesseler-web
- Pages: `index.astro` (home), `services.astro`, `book.astro`
- Layout: `src/layouts/SoleLayout.astro`
- Design: Sage green (`#EBF2EB`), Cormorant Garamond font, dark forest footer, Unsplash images

---

## Important Technical Notes

1. **No Node/npm locally** — edits go directly to source files; Cloudflare Pages builds automatically on each git push
2. **Astro scripts need `is:inline`** — `<script is:inline>` for any JS that uses onclick or global functions; plain `<script>` is ES module scoped and can't be called from HTML attributes
3. **No `gh` CLI** — use `WebFetch` with GitHub API or direct git commands
4. **Git config** — set locally in each repo: `git config user.email "collieruesseler23@gmail.com"` and `git config user.name "IndyCJ1"`
5. **Tailwind v4 syntax** — uses `@import "tailwindcss"` and `@theme {}`, NOT `@tailwind base/components/utilities`
6. **All addresses** — Gainesville, GA 30501 (NOT FL/32601)

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
13. Basic on-page SEO (title tags, meta descriptions, alt text)

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

## What to Do Next

1. ~~Deploy demo sites to Cloudflare Pages~~ ✓ Done
2. ~~Build Starter, Plus, Pro demo sites~~ ✓ Done (hogtown-smoke, Perch, Solé)
3. ~~Security hardening~~ ✓ Done (CSP headers, no inline handlers, honeypot)
4. **Get first client** — friend/family discounted, or local business cold outreach
5. **Build portfolio page** on agency site showing real before/afters once clients exist
6. **Set up homelab** when needed (Proxmox + Docker + Coolify + Cloudflare Tunnel)
7. **Spin up Hetzner** when first paying client signs

---

## Picking Up On Another Computer

In a new Claude Code session, paste this prompt:

```
I'm continuing work on my web dev business called Apex Web (Gainesville, GA). 
Context repo: https://github.com/IndyCJ1/-webdev-business-context

Key repos:
- Agency site: https://github.com/IndyCJ1/cuesseler-web (live: cuesseler-web.pages.dev)
- Starter demo: https://github.com/IndyCJ1/hogtown-smoke (live: hogtown-smoke.pages.dev)
- Plus/Pro demos are inside cuesseler-web at src/pages/demos/

Local paths on this machine: C:\Users\Collier\repos\cuesseler-web and hogtown-smoke

Tech: Astro + Tailwind CSS v4, deployed via Cloudflare Pages (no local Node/npm).
Design: white bg, Plus Jakarta Sans, #FF4500 orange accent on main agency site.

Read the README in the context repo and continue from where we left off.
```

Then tell Claude what you want to work on next.

---

## Asset Manager

Note: There's a separate `asset-manager-main` project with a SQL database. Needs a server — plan is to run in Docker on homelab via Coolify once infra is set up.
