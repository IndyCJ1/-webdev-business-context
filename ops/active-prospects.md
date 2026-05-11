# Active Prospects

Lightweight log of prospects with mockups in flight. The Notion CRM (`ops/notion-crm-setup.md`) is the source of truth for the full lead pipeline; this file just tracks the **mockups built and ready to show**.

When a prospect signs, move them out of this file and into `templates/case-study.md` once the project ships.

---

## Gainesville HVAC Services

- **Mockup URL:** https://lanierweb.com/mockups/gainesville-hvac/
- **Industry:** HVAC (heating, cooling, indoor air)
- **Tier pitched:** Starter ($1,500 + $50/mo)
- **Repo path:** `cuesseler-web/src/pages/mockups/gainesville-hvac/`
- **Layout:** `src/layouts/GHvacLayout.astro` (light theme, Big Shoulders Display + Manrope + JetBrains Mono)
- **Style direction:** heritage industrial / tradesman editorial — cool off-white background, warm copper + cool steel-blue dual accents, scroll-snap full-page sections on home, big sectional fade-in reveals
- **Pages built:** Home, Services, Service Area, About, Contact (5-page Starter)
- **Real reviews used:** 4 verified Google reviews from their actual GBP
- **Status:** Mockup ready to walk in / send link

**Before walking in, swap in `_business.ts`:** real phone, license number, founding year (currently `(770) 555-0142`, `GA CN006847`, `2014` placeholders).

---

## Fizzy (drinkfizzyga)

- **Mockup URL:** https://lanierweb.com/mockups/fizzy/
- **Admin URL:** https://lanierweb.com/mockups/fizzy/admin
- **Industry:** Drink truck — dirty sodas + fizzy refreshers; private events & pop-ups
- **Region:** Jackson County, GA (just east of Hall)
- **Tier pitched:** Starter + custom admin add-on
  - **$1,500 build + $50/mo + $300 one-time** for the admin (today's location, menu editor, bookings inbox)
- **Repo path:** `cuesseler-web/src/pages/mockups/fizzy/` (single `index.astro` + `admin.astro`)
- **Style direction:** matched their Instagram exactly — soft pink (`#FCE0E5`), bold black FIZZY logomark, yellow smiley accents, coral pop, mint section variation, Polaroid photo cards, Caveat handwritten script + Archivo Black display
- **Real contact info:** (615) 961-7732 · drinkfizzyga@gmail.com (from their IG bio)
- **Real Instagram:** @drinkfizzyga
- **Status:** Mockup ready. **Email/IG DM template sent (or queued).**

### What makes this one special

This is the first mockup with a working backend admin. Three Cloudflare Pages Functions (`functions/api/fizzy/`):
- `login.ts` — password auth, sets HttpOnly cookie
- `location.ts` — today's banner (GET public, POST auth)
- `menu.ts` — menu editor (GET public, POST auth)
- `bookings.ts` — booking submissions (GET auth lists, POST public submits, DELETE auth removes)
- `check-auth.ts` — admin uses on load to decide login vs editor

KV namespace `FIZZY_KV` holds the data. Setup steps in `ops/fizzy-admin-cloudflare-setup.md`.

### Pitch for Fizzy

> "$1,500 build + $50/mo + $300 one-time for the admin. You get three things you can update yourself from your phone: today's location, the menu, and a booking inbox where every catering request lands instantly. No more digging through DMs to find who asked about that wedding."

### Move to production when they sign

1. Clone cuesseler-web → new repo `lanier-fizzy`
2. Strip everything except `src/pages/mockups/fizzy/` (rename to `src/pages/`) and `functions/api/fizzy/` (rename to `functions/api/`)
3. Strip `/mockups/fizzy/` prefix from all internal links
4. Deploy as new Pages project under their domain (e.g. `drinkfizzy.com`)
5. Re-create the `FIZZY_KV` binding and `FIZZY_PASSWORD` secret in the new project
6. Hand over the admin URL + their fresh password

---

## Canopy + the Roots (canopyandtheroots.com)

- **Mockup URL:** https://lanierweb.com/mockups/canopy-and-the-roots/
- **Existing site:** https://canopyandtheroots.com/
- **Industry:** Coffee shop + yoga studio (upstairs) + underground music & comedy listening room (downstairs); membership-driven community space
- **Location:** 53 W Main Street, Dahlonega, GA 30533
- **Established:** 2020
- **Owner(s):** Not listed publicly — need to find on first visit
- **Tier pitched:** **Plus** ($3,500 build + $75/mo) — multi-revenue-stream business; needs proper booking + ticketing + membership funnel. Could grow into Pro with admin add-on for event management.
- **Repo path:** `cuesseler-web/src/pages/mockups/canopy-and-the-roots/` (single `index.astro` for v1)
- **Real contact info:**
  - Email: events@canopyandtheroots.com
  - Instagram: @canopyandtherootsdahlonega
  - Facebook: canopyandtheroots
  - **No phone number** anywhere on their site — verify on walk-in
- **Tagline:** "Where the hustle slows and the rhythm is heard."
- **Concept descriptor:** "coffee | yoga UPstairs · comedy | music UNDERground"

### Style direction

Dual-zone aesthetic that mirrors their physical split:
- **Upstairs (coffee/yoga):** cream base, sage/moss greens, warm clay, soft natural light, organic foliage motifs
- **Underground (music/comedy):** deep forest near-black, ember/gold accents, "sultry moss and star-lit" feel they describe themselves
- Type: Fraunces (display serif, has personality without being precious) + Manrope (body) + Caveat (occasional handwritten accent)

### Their existing site (for the pitch)

**Strengths:** strong brand identity, beautiful photography, polished aesthetic, clear voice ("Without the clinking of bar glasses, chatter or cell phones"). This is NOT a "your site is ugly" pitch.

**Functional gaps (the actual pitch):**
- **No phone number** — email-only contact
- **No hours of operation** listed anywhere
- **No pricing** — membership mentioned but rates hidden
- **No online class booking** for yoga
- **No ticket purchase flow** for music/comedy nights
- **No testimonials / social proof**
- **No teacher/staff bios**
- **No clear CTAs** — every section ends without a next action
- **Newsletter form appears incomplete**

### Pitch angle

> "Your brand identity is already gorgeous — I'm not going to touch that. What I built is the conversion layer on top: yoga class booking, ticket purchase for shows, membership tiers with visible pricing, and a hours-and-phone block that actually appears on the page. Right now someone has to DM you to find out what time you open. That's a leak."

### Membership tiers (mocked — confirm with them)

The real site lists perks (bottomless coffee, member merch, special-event discounts, VIP lounge) but no rates. In the demo I sketched out three tiers — they'll tell us what's actually right.

### Status

Mockup built — ready to walk in. Dahlonega is ~45 min from Gainesville (easy drop-in). Best time: weekday late morning when the coffee crowd thins but before yoga.

**Before walking in, swap in `_business.ts` (or inline in index.astro):**
- Real phone (currently placeholder `(706) 555-0184`)
- Real hours (currently best-guess)
- Real membership pricing
- Real upcoming shows from their actual calendar

---

## Mockup workflow (general)

For any future prospect, the proven pattern is:

1. **Find them** — Google Maps, IG, walk-by, referral
2. **Pull their public assets** — Google Business Profile photos, Instagram bio (phone, email, region), recent posts (real menu items, real reviews)
3. **Build at `lanierweb.com/mockups/{slug}/`** — single index.astro for Starter, layout + multiple files for Plus/Pro
4. **Match their existing aesthetic** — copy palette and type direction from their IG/menu, don't impose Lanier Web's house style. **Personalized > generic.**
5. **noindex,follow** — don't compete with their real listings in search
6. **Walk in or DM** — *"I built this for you yesterday — what do you think?"*
7. **Don't talk while they scroll** — watch where they linger, that's what to discuss
8. **Quote after the demo, not before**

Time budget per mockup: ~2 hours for a clean Starter, ~6–8 for Plus/Pro tier with real-feeling content.
