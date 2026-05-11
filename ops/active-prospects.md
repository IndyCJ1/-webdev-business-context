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
- **Established:** 2020 (confirmed by owner)
- **Owner:** **Hollie Lytle** (Founder & CEO) — on the About page
- **Team named on About page:** Ansley Walker (fiber artist), Danny Wilson (interior design), Akeeme Martin (manager + sound), **Franchesca Spittler** (manager + fitness instructor — likely a yoga teacher), Diana, Kerri, Augie (events/social house)
- **Tier pitched (revised approach — 2026-05-10):** **Starter or Plus ($1,500–$3,500 build + $50–$75/mo)** for **Phase 1**. Build *around* her existing tools (Eventbrite/external ticketing, Google Forms, in-store membership) — make them feel native instead of replacing them. **Phase 2 upsell** down the line: integrated Stripe payments + admin dashboard + recurring membership billing (~$400–500 add-on like the Fizzy admin). Reasoning: her brand is already polished, so v1 is navigation + clarity + missing details (hours/phone/address), not full custom infrastructure. Faster yes, lower risk, natural Phase 2 conversation in 6 months.
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

**Functional gaps (the actual pitch — verified across Home, Yoga, Memberships, Events, About, Privateevent, For-artists pages):**
- **No phone number anywhere** on the site
- **No hours of operation** listed on any page
- **Membership: explicitly no online sales.** `/memberships` literally says: *"Please inquire in-store; at this time, we do not offer online membership sales."* No tiers, no prices. Strongest pitch point — they're leaving money on the floor every day. Real perks they list: bottomless coffee, merch, discounted show tickets, VIP performance access, premium WiFi, balcony seating, copy services, charging station, exclusive member events. There's also a **"Director's Guild"** add-on (name engraved on director's chairs).
- **No online class booking** for yoga. `/yoga` lists styles but links out to events page for schedule. Drop-in shown ($12 guest / $8 member) but no per-class reserve flow.
- **Ticket purchase routes to external platform** — `/events` lists shows but ticket prices aren't shown and "Get TICKETS HERE" links out (probably Eventbrite). No in-page checkout.
- **Private events use a Google Form.** `/privateevent` describes the offering nicely ("Yoga Workshops • Celebrations • Art Exhibitions + Galleries • Company Events + Training") but the inquiry CTA is *"SUBMIT YOUR EVENT SPACE RENTAL INQUIRY HERE"* → Google Form. No pricing or capacity info shown. Same pattern.
- **Artist booking uses a Google Form too.** `/for-artists` has a strong positioning line — *"all shows headline original work only (no cover bands here)"* and *"a for-the-artist venue"* — but the booking CTA is *"SUBMIT Booking inquiry HERE"* → Google Form.
- **No teacher/staff bios** — even though the About page names the full team
- **No testimonials / social proof**
- **Homepage hero readability is poor** — large marquee-letter background bleeds into white body text, especially rough on mobile. (Don't lead with this in cold outreach — let the mockup demonstrate the difference. Bring it up in person if asked.)

### Pitch angle

> "Your brand identity is already gorgeous — I'm not going to touch that. What I built is the navigation layer on top: a yoga schedule that lives on the yoga page, a shows section that surfaces your upcoming nights on the homepage, hours and phone visible everywhere, and inquiry forms that don't feel like a side trip. Right now someone has to DM you to find out what time you open. That's a leak. For v1 we keep your existing booking and ticketing flows running behind the scenes — Eventbrite, Google Forms, in-store membership. Phase 2 we can talk about wrapping them in proper checkout if you ever want to bring those in-house."

### Membership tiers (mocked — confirm with them)

The real site lists perks (bottomless coffee, member merch, special-event discounts, VIP lounge) but no rates. In the demo I sketched out three tiers — they'll tell us what's actually right.

### Real upcoming shows (from /events — pulled May 2026)

- May 23 · Luke Morgan: "Whiskey Jam" country
- May 30 · Tony & Yve Brook: Blues from Alabama + British Isles Folk
- May 31 · Coffee Cupping + "Meet the Roaster" (Tan Brown Coffee Roasters)
- Jun 12 · ZG Smith x Madison Hughes: indie-folk
- Jun 27 · Caleb Tokarski: Soulful Sounds from NOLA

### Real yoga pricing (from /yoga)

- $12 / guest, $8 / member per class. No class packs, no schedule, no booking.

### Email/DM draft (final, build-around framing)

**Subject:** Quick website mockup for Canopy + the Roots

> Hi Hollie,
>
> I'm Collier with Lanier Web, a local web design business here in Gainesville. I came across Canopy + the Roots online a while back and built a quick website mockup for you because I really liked the concept and thought your site could do a little more for you.
>
> Preview:
> https://lanierweb.com/mockups/canopy-and-the-roots/
>
> Your branding is already really strong. The mockup is mostly about making the site easier to navigate, so people can find class times, show dates, hours, and the right inquiry form without having to dig around.
>
> A few things it could help with:
>
> A weekly yoga schedule that lives on the yoga page itself, so people aren't bouncing between pages to find class times
>
> An upcoming shows section right on the homepage with clear ticket links going to your existing setup
>
> Hours, phone number, and address easy to find from any section (right now those don't really show up anywhere on the site)
>
> A membership page that actually lays out the perks clearly, so more people are curious enough to come in and ask
>
> A cleaner private events section with the inquiry form built right in, instead of feeling like a separate page to go find
>
> No pressure at all. I just thought Canopy had a really cool concept and wanted to show you what it could look like with everything pulled together a little tighter.
>
> Thanks,
> Collier Uesseler
> Founder · Lanier Web
> lanierweb.com · collier@lanierweb.com
> Modern Websites. Real Results.

### Status

Mockup built, email drafted — ready to send (events@canopyandtheroots.com) or walk in. Dahlonega is ~45 min from Gainesville (easy drop-in). Best time: weekday late morning when the coffee crowd thins but before evening yoga.

**Before walking in, still need:**
- Real phone (placeholder `(706) 555-0184` in the mockup)
- Real hours (best-guess in the mockup)
- Real membership pricing — owner-only conversation since they don't publish it

**Note for in-person conversation:** the mockup shows three aspirational membership tiers and per-class reserve buttons. Be ready to say *"this is the full vision — for v1 we'd start with the redesign and keep your booking flows running behind the scenes."* Otherwise Hollie may expect the build to match the mockup exactly.

---

## Gainesville Coffee Shop at Lawrence Pharmacy (gainesvillecoffeeshop.com)

- **Mockup URL:** https://lanierweb.com/mockups/gainesville-coffee-shop/
- **Existing site:** https://gainesvillecoffeeshop.com/ (WordPress, 4/10 design, content only fills half the viewport — visible layout bug)
- **Industry:** Vintage pharmacy-counter luncheonette — breakfast + lunch + free local delivery. NOT an artisan coffee shop. Diner menu (chili dogs, burgers, English muffin sandwiches, omelets, breakfast plates).
- **Host pharmacy:** **Lawrence Pharmacy** — opened **January 29, 1958** — ~70 years on Broad Street. Owner of pharmacy: **Stephen Adams, RPh**.
- **Location:** 631 Broad Street SE, Gainesville, GA 30501
- **Phone:** 770-534-3231
- **Email:** Info@GainesvilleCoffeeShop.com
- **Hours:** Monday – Friday, 8am – 2pm. Closed weekends.
- **Tagline they currently use:** "We Deliver Breakfast & Lunch. FREE delivery in Gainesville — No minimum order!"
- **Online ordering:** ChowNow → https://ordering.chownow.com/order/3192/locations
- **Sister business:** Skogie's on Lake Lanier (same operators likely)
- **Tier pitched:** **Starter** ($1,500 + $50/mo). Single page is plenty — limited hours, focused menu, one location. Could grow with an admin add-on later if they want a daily-specials editor (Fizzy admin pattern).
- **Repo path:** `cuesseler-web/src/pages/mockups/gainesville-coffee-shop/`

### Style direction

Vintage Americana / 1950s pharmacy-counter / soda-fountain aesthetic. NOT modern indie coffee, NOT rustic farmhouse — this is a specific lane that matches their actual identity (a diner counter inside a 1958 pharmacy).
- **Palette:** warm cream base, deep pharmacy red, forest/apothecary green, mustard accent, charcoal ink
- **Type:** DM Serif Display (or similar vintage editorial serif) + Inter (clean body) + Caveat (handwritten daily-special touch)
- **Visual cues:** counter signage feel, breakfast plate photography, soft 1958 nostalgia without going theme-park kitsch

### Their existing site (for the pitch)

**Strengths:** has hours, phone, address, ChowNow ordering, email contact. Bones are there.

**Functional + visual gaps (the actual pitch):**
- **Layout fills only half the page** — visible bug on desktop. Content doesn't span the viewport. This is the single most obvious thing to fix.
- **WordPress template, "Proudly powered by WordPress" footer** — `/wp/` directories in image paths suggest an older install
- **No menu actually visible on the homepage** — menu is gated behind a separate `/menus/` page when their entire business is the menu
- **No photos of the space** — the pharmacy-counter setting is their biggest differentiator and it's invisible on the site
- **No mention of the 1958 heritage** — 70 years of history is the strongest brand story they have, and it's not on the site
- **Limited mobile signals** — basic WordPress responsive at best
- **No social media links** — only Yelp gets mentioned
- **Free delivery is buried** — their tagline is "We Deliver Breakfast & Lunch · FREE delivery, no minimum" but the homepage doesn't lead with it

### Pitch angle

> "Your site has all the right pieces — hours, phone, ChowNow, the address. But the layout is broken on desktop (literally fills half the page), you don't show photos of the counter, and the fact that you've been at the corner of Broad Street since 1958 isn't anywhere on the homepage. That 70-year history is your strongest brand story. I rebuilt it around that — kept your ChowNow ordering, kept your delivery promise out front, made it work on a phone."

### Status

Mockup ready — direct walk-in target (right in downtown Gainesville). Easiest of all the prospects to drop in on since it's local.

**Menu is now real** — pulled directly from their 2024 PDF (gainesvillecoffeeshop.com/wp/wp-content/uploads/2024/06/Menu-2024.pdf). All 12 breakfast items, 23 sandwich items, soups, salads, drinks, sides, combos baked into the mockup with exact prices. Specific items worth noting in conversation: **Cathead biscuit**, **Tot's Eggs in a Blanket**, **Kai Kai Special**, **Hot Sicilian on a Kaiser**, **Cuban Sandwich**, **Grilled Crabcake BLT**, **Thai Steak on a Kaiser**.

**Catering is a real revenue lane** — their PDF explicitly promotes "we cater & offer breakfast, danish & sandwich trays for all events." Highlighted on the mockup delivery card.

**Location landmark:** They're right next to **Northeast Georgia Medical Center** — added to the mockup. NGMC is the dominant employer in Gainesville so this is huge context for the office-breakfast / hospital-staff delivery angle.

**Before walking in, still need:**
- Real photos of the space + the counter (their gallery page has 12 photos at /wp/wp-content/uploads/photo-gallery/thumb/ — could swap in)
- Confirm whether Stephen Adams runs the coffee shop too, or if it's a separate operator inside his pharmacy
- Confirm hours haven't shifted since the 2024 PDF

---

## Farmhouse Coffee

- **Mockup URL:** https://lanierweb.com/mockups/farmhouse-coffee/
- **Industry:** Specialty coffee shop — signature lattes, breakfast, rentable coffee trailer, FAM Club loyalty program
- **Location:** 118 Jesse Jewell Pkwy SE, Suite 100, Gainesville, GA 30501
- **Phone:** 706-291-0001
- **Contact:** No public email found — Instagram DM or walk-in is the primary approach
- **Website:** linktr.ee/farmhousecoffee — Linktree only, no real website
- **Instagram:** @farmhousecoffee.co (8,100+ followers)
- **Rating:** 4.8 stars, 183 reviews. Opened September 2023.
- **Tier pitched:** Starter ($1,500 + $50/mo)
- **Repo path:** `cuesseler-web/src/pages/mockups/farmhouse-coffee/` (single `index.astro`)
- **Style direction:** Warm cream (#FAF6F0), Playfair Display serif + Manrope + Caveat handwritten accents, rust accent (#C4622D), dark coffee-brown footer. Matches their Instagram aesthetic exactly — cozy, minimalistic, farmhouse warmth.
- **Status:** Mockup live. Walk-in or Instagram DM to pitch.

### What makes this one special

Three revenue streams with no web support:

1. **Coffee trailer** — bookings buried as one Linktree button. No page, no inquiry form, no pricing. Events prospects have no way to start the process without DMing.
2. **FAM Club loyalty program** — no landing page. People can't understand the perks or sign up online. The club exists but the web presence for it doesn't.
3. **8,100+ Instagram followers** — all driving traffic to a Linktree. Every one of those followers could be a subscriber, a trailer inquiry, or a loyalty member. Right now they land on four buttons.

### Pitch angle

> "You've built a 4.8-star brand with 8,000 Instagram followers and a coffee trailer people love — and all of that is backed by a Linktree. People googling 'coffee Gainesville' find scraped listing sites with your wrong hours. Your trailer bookings come in through DMs. Your FAM Club has no home. I built a site that fixes all three."

### DM / Email draft

**Instagram DM (primary — no public email):**

> Hey! I'm Collier with Lanier Web, a local web design business in Gainesville. Big fan of what you've built — I stopped in a few weeks back. I put together a quick website mockup for you:
>
> lanierweb.com/mockups/farmhouse-coffee/
>
> Your Instagram is doing a lot of heavy lifting. The mockup gives it a real home: a trailer booking page so people can check availability without DMing you, a FAM Club signup that works online, and your hours + menu in one place.
>
> No pressure — just wanted to show you what it could look like. Happy to stop by and walk you through it if you're curious.
>
> Collier Uesseler · Lanier Web · lanierweb.com

**Email version (if email is found):**

Subject: Website mockup for Farmhouse Coffee

> Hi,
>
> I'm Collier with Lanier Web, a web design business based here in Gainesville. I came in a few weeks back — the s'mores latte is genuinely excellent — and noticed you're running everything off a Linktree. I built a quick mockup to show you what a real site could look like:
>
> lanierweb.com/mockups/farmhouse-coffee/
>
> Three things the mockup addresses that the Linktree can't:
>
> Your coffee trailer has no booking page right now. People who want to book it for a wedding or event have to DM you to even start the conversation. The mockup has a dedicated trailer section with an availability form.
>
> The FAM Club is a real competitive advantage for a coffee shop, but there's no page that explains the perks or lets people sign up online. The mockup has that built in.
>
> Most people who Google "coffee Gainesville" land on third-party sites with outdated info. Your own site fixes that and gives your Instagram followers somewhere real to send people.
>
> No pressure at all. I just thought what you've built deserved a better online home. If you want to chat, I'm happy to stop by or send over pricing.
>
> Collier Uesseler
> Founder · Lanier Web
> collier@lanierweb.com · lanierweb.com

### Before walking in

- **Confirm current hours** — sources conflict (some say 6am–7pm, some say 7am–4pm). Verify in person or via Google Maps.
- **Find owner's name** — not publicly listed anywhere. Ask on walk-in.
- **Menu items are researched, not confirmed** — be ready to say "we'd swap in your real current menu, these are based on what I found online."
- The mockup menu has speculative items and prices. Don't lead with specifics on the menu — let them discover it and correct anything that's off.

### Other Gainesville coffee shops ranked (discovery run 2026-05-11)

| Rank | Business | Web presence | Verdict |
|---|---|---|---|
| 1 | Farmhouse Coffee | Linktree only | **Build next** |
| 2 | Gainesville Coffee Shop @ Lawrence Pharmacy | WordPress 4/10, half-page bug | **Mockup built** |
| 3 | Meadowlark Coffee (meadowlarkcoffee.shop) | Squarespace 5.5/10, no hours/phone | Possible Starter |
| 4 | Inman Perk Coffee (inmanperkcoffee.com) | WordPress 6/10, mid-2010s | Harder sell, 20-year biz |
| Skip | Boarding Pass Coffee (boardingpasscoffee.com) | Shopify 7.5/10, fully set up | Multi-location, skip |

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
