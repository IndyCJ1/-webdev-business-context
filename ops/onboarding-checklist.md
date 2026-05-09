# Client Onboarding Checklist

What happens after they sign. One page, in order. Don't skip steps.

## Day 0 — Contract signed

- [ ] Counter-signed contract PDF emailed to client (BCC `projects@lanierweb.com`)
- [ ] Stripe invoice for 50% deposit sent
- [ ] Calendar event: 7 business days from now = "Send staging link to {Client}"
- [ ] Add client to spreadsheet (lead status → "active build")

## Day 0 — Once deposit clears

- [ ] Send the **client intake form** (templates/client-intake-form.md)
- [ ] Send the **shared content folder** link (Google Drive folder named `Lanier Web — {Client}`)
- [ ] Set their expectations in writing: "I'll have a staging link in 7 business days from when I have your intake form back. One round of revisions after that."

## Day 1–3 — Build prep

- [ ] Register domain on Cloudflare Registrar (in client's name, billed to your card, reimbursed)
- [ ] Create new GitHub repo: `lanier-{client-slug}` (private)
- [ ] Clone the appropriate template (cuesseler-web for Starter; future Plus/Pro templates)
- [ ] Replace placeholder content with intake form answers
- [ ] Create Cloudflare Pages project, point to the new repo, get a `.pages.dev` URL for staging
- [ ] Get a fresh Formspree form ID for this client (free tier — 50 submissions/mo)

## Day 3–7 — Build first draft

- [ ] Apply brand: logo, colors, photos
- [ ] Hero copy + CTA
- [ ] All pages from intake form
- [ ] Mobile pass — open in Chrome dev tools at iPhone SE width (375px)
- [ ] PageSpeed Insights — confirm 90+ on mobile
- [ ] Add Google Business / Maps embed if applicable
- [ ] Add JSON-LD LocalBusiness schema with their address

## Day 7 — Send staging link

- [ ] Email staging URL to client
- [ ] Include 3 specific things to check: "click the contact form, look at the menu page, view it on your phone"
- [ ] Set expectation: "One round of changes — please collect everything in one reply rather than dripping them"

## Day 8–14 — Revisions

- [ ] Apply revisions in one batch
- [ ] Re-test mobile + PageSpeed
- [ ] Send updated staging link
- [ ] Get **written** approval to launch ("looks good, please launch" in email — save it)

## Launch day

- [ ] Send Stripe invoice for remaining 50% — wait for it to clear before launching
- [ ] In Cloudflare Pages: add custom domain (their real domain)
- [ ] In Cloudflare DNS: point root + www to the Pages project (Cloudflare auto-handles)
- [ ] Verify SSL is live (green padlock)
- [ ] Submit `sitemap.xml` to Google Search Console
- [ ] Test the contact form on the live domain — submit a test entry, confirm it lands in the client's inbox
- [ ] Tap-to-call test on a real phone
- [ ] Take screenshots: homepage on desktop, homepage on phone — save to `Lanier Web — {Client}/launch/`
- [ ] Create the Stripe subscription for monthly hosting, anchor = today

## Day 1 post-launch

- [ ] Send launch email: "{Client}'s site is live at {url}. Here's what to expect on monthly hosting…"
- [ ] Set up Uptime Kuma monitor (or skip until you have homelab — for now use a free uptimerobot.com monitor)
- [ ] Calendar reminder: 30 days from launch = "Check in with {Client}, ask for a Google review"

## Day 30 post-launch

- [ ] 15-minute check-in call or email
- [ ] Ask: "Anything you'd like edited this month?" (use up the included monthly time)
- [ ] Ask for a Google review — send the direct review URL
- [ ] If they're happy, ask: "Anyone else you know who could use this?"
- [ ] Capture their feedback in case-study.md format
