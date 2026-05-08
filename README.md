# Web Dev Business — Context & Handoff

This is a context document for picking up the web dev business plan from any computer. Clone this repo and paste the relevant sections into Claude (Claude Code or claude.ai) to continue where you left off.

---

## The Business

Build websites for local businesses (Gainesville, FL) and host them on a monthly retainer. Recurring revenue model.

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

```
Internet → Cloudflare (DNS + CDN + Tunnel) → Homelab / Hetzner
                                                    ↓
                                             Proxmox (bare metal, future)
                                                    ↓
                                          Ubuntu VM running Docker
                                             ↙    ↓    ↘
                                       Coolify  Gitea  Uptime Kuma
                                           ↓
                                     Client websites
```

**Production hosting (when paying clients exist):** Hetzner CX32 VPS ($7/mo) running Coolify
**Until first paying client:** All on homelab, free
**DNS / SSL / CDN:** Cloudflare (free tier)
**Domains:** Cloudflare Registrar (at-cost, registered in client's name)
**Site framework:** Astro + Tailwind CSS for static sites, WordPress for clients who need easy editing
**Free hosting for static sites:** Cloudflare Pages
**Git:** Gitea on homelab (private GitHub clone)
**Staging URLs:** Cloudflare Tunnel from homelab — no port forwarding needed
**Monitoring:** Uptime Kuma (free, self-hosted)
**Backups:** rclone cron → Backblaze B2 ($1–2/mo)
**Payments:** Stripe (2.9% + $0.30/charge)

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
- Cloudflare (DNS, CDN, SSL, Tunnel, Pages, Email Routing)
- Let's Encrypt SSL
- Gitea, Uptime Kuma, Coolify (self-hosted)

**Optional / scale-dependent:**
- LLC formation: $50–500 one-time (skip until 3+ clients)
- E&O insurance: $30–60/mo (skip until ~5 clients)
- Business email (Workspace/Fastmail): $6–7/mo
- Bigger Hetzner box: $13–25/mo (after ~20 clients)

---

## Legal

- **No LLC needed yet** — sole proprietor until 3+ paying clients or one demands it
- **DBA at county clerk** ($20–50) is enough to open a business bank account
- **Written contract for every client** — Bonsai has free templates
- **50% upfront, 50% on launch** — non-negotiable

---

## What's Already Built

Two demo sites built with Astro + Tailwind, pushed to GitHub:

1. **Agency site** — https://github.com/IndyCJ1/cuesseler-web
   - Local: `C:\Users\cuesseler\source\repos\cuesseler-web`
   - Dark themed landing page with hero, services, packages, about, contact form
   - Contact form uses Formspree ID `mzdojrav`

2. **Hogtown Smoke (fake Gainesville BBQ)** — https://github.com/IndyCJ1/hogtown-smoke
   - Local: `C:\Users\cuesseler\source\repos\hogtown-smoke`
   - Restaurant demo with hero, full menu, about, hours/location
   - Order Online buttons link to Uber Eats / DoorDash placeholder URLs

Both run locally with `npm run dev` (agency on port 4321, restaurant on 4322).

---

## Roadmap — Build Process for Each Client

### Phase 1 — Sales & Scoping
1. Identify target client (bad/no website, local business)
2. Mock up before/after concept to show them
3. Meet/call — ask what they need, who visits, what action they want
4. Send 1-page proposal with package + price
5. Get signed contract + 50% deposit before touching anything

### Phase 2 — Setup
6. Register domain in client's name (Cloudflare Registrar)
7. Create client folder in Gitea repo
8. Spin up staging subdomain via Cloudflare Tunnel
9. Scaffold project (clone Astro/WP starter)
10. Create shared content checklist (logo, photos, copy, colors, hours, contact info)

### Phase 3 — Build
11. Build layout with placeholder content first — get structure approved
12. Swap in real copy, photos, branding
13. Add contact form (Formspree)
14. Mobile responsiveness check
15. Basic on-page SEO (title tags, meta descriptions, alt text)
16. Connect Google Analytics + Google Search Console

### Phase 4 — Review
17. Send staging link
18. One round of revisions
19. Final approval in writing
20. Collect final 50% before launch

### Phase 5 — Launch
21. Deploy to Hetzner via Coolify (production branch)
22. Point Cloudflare DNS to VPS, enable proxy
23. Verify SSL is live
24. Submit sitemap to Google Search Console
25. Verify contact form works on live domain
26. Set up Uptime Kuma monitor
27. Set up nightly backup to Backblaze B2
28. Start monthly billing

### Phase 6 — Ongoing
29. Check Uptime Kuma + backup logs weekly
30. Apply WP/dependency updates monthly
31. Respond to edit requests (1hr/mo included)
32. Quarterly check-in calls

---

## What to Do Next

1. **Deploy both demo sites to Cloudflare Pages** (free hosting from GitHub)
2. **Build portfolio** — add 1-2 more demo sites in different industries
3. **Set up homelab** — Proxmox + Ubuntu VM + Docker + Coolify + Gitea + Cloudflare Tunnel
4. **Get first client** — friend/family discounted, or local business cold outreach
5. **Spin up Hetzner** when first paying client signs

---

## Picking Up On Another Computer

In a new Claude Code session or claude.ai conversation, paste this:

```
I'm continuing work on my web dev business. Context is in https://github.com/IndyCJ1/webdev-business-context. The two demo sites are at https://github.com/IndyCJ1/cuesseler-web (agency landing page) and https://github.com/IndyCJ1/hogtown-smoke (fake Gainesville BBQ restaurant). Read the README in the context repo and we'll continue from where we left off.
```

Then tell Claude what you want to work on next.

---

## Asset Manager

Note: There's a separate `asset-manager-main` project with a SQL database. It needs a server (not Cloudflare Pages). Plan is to run it in Docker on the homelab via Coolify, exposed via Cloudflare Tunnel — once homelab infra is set up.
