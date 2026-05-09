# Portfolio Strategy

How the Work section on lanierweb.com evolves from "demos" to "real client wins."

## Current state (no clients yet)

The Work section shows three demo sites — Hogtown Smoke, The Perch, Solé Wellness. Each card is honest about being a live, interactive demo. This is fine for now and signals "this is what each plan actually builds."

## Stage 1 — first paying client signs

Don't replace the demos yet. Add a fourth card on top:

- **First card:** the real client (case study, real domain, "{Client} · {Industry}")
- **Cards 2–4:** existing demos, labelled "Sample build — {Tier}"

The mix of real + demo is honest and prevents looking emptier than before.

## Stage 2 — three paying clients

Replace each demo with the corresponding real client at the same tier. Layout stays the same.

If you have two Pro clients but no Starter, leave the Hogtown demo in the Starter slot. Don't fake it.

## Stage 3 — six+ paying clients

The homepage Work section can only fit ~3 cards cleanly. Move to:

- Homepage: 3 strongest case studies (one per tier ideally)
- New page `/work` lists everything with industry filter chips
- Each case study gets its own page at `/work/{slug}`

## What makes a real case study work

Look at how cards in `index.astro` are structured today (`name`, `industry`, `tier`, `price`, `href`). A real case study card shows:

- **Industry** (matters more than business name to someone scanning)
- **Tier built** (anchors them to pricing)
- **Headline result** — replace the demo's "View demo & details →" with something specific: "2× call volume in 30 days" or "Launched in 18 days"

## Photo standards

When a client launches, capture in this order:

1. Live homepage screenshot — desktop, 1440×900
2. Live homepage screenshot — phone, 390×844
3. Before/after if you have access to the old site (use Wayback Machine if not)
4. One detail shot — the feature that mattered most (booking widget, menu, etc.)

Save originals + 1200×800 web versions in `/public/work/{slug}/` in the cuesseler-web repo.

## What not to do

- **Don't pad with friends-and-family work** unless it's genuinely good. One bad portfolio piece kills three good ones.
- **Don't show every page of a client site.** One hero shot per case study. The full site is one click away.
- **Don't write copy in the case study that the client wouldn't repeat aloud.** If they wouldn't say it, don't quote them saying it.
