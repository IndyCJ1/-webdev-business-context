# Stripe & Billing Setup

How to take money from clients without overthinking it. One-time setup, then runs on autopilot.

## What you need before the first invoice

- [ ] Stripe account (free to open — stripe.com)
- [ ] Federal EIN (free, takes 5 min at irs.gov/ein)
- [ ] Business bank account (separate from personal — required for legitimacy)
- [ ] DBA filed at Hall County clerk's office (~$50, lets the bank account be in "Lanier Web")

## Stripe setup walkthrough

1. **Create Stripe account** with `billing@lanierweb.com`
2. **Activate payments** — Stripe asks for: business address, EIN, bank account for payouts (use the new business account), and your SSN as the responsible party (sole prop). Approval is usually same-day.
3. **In Stripe Dashboard:**
   - Brand: upload Lanier Web logo, set accent color `#FF4500`
   - Public details: name, support email `billing@lanierweb.com`, support phone
   - Statement descriptor: "LANIER WEB" — this is what shows on the client's bank statement
4. **Tax setup** — turn on Stripe Tax once you have 3+ clients. Skip for now.

## Two products to create in Stripe

### Product 1: One-time build fees

Three prices on one product called "Website Build":
- Starter — $1,500 (one-time)
- Plus — $3,500 (one-time)
- Pro — $6,000 (one-time, custom-priced from here)

Set each as a one-time price. When you send an invoice, pick the right price.

### Product 2: Monthly hosting + maintenance

Three prices on one product called "Hosting & Maintenance":
- Starter Monthly — $50/month, recurring
- Plus Monthly — $125/month, recurring
- Pro Monthly — $300/month, recurring

When a client signs, create a **subscription** in Stripe — start date = launch day. Stripe charges them automatically each month.

## Invoicing flow per client

| Step | When | What |
|---|---|---|
| 1 | Contract signed | Send 50% deposit invoice via Stripe Invoice → "Send invoice" with `due upon receipt` |
| 2 | Pre-launch approval | Send 50% balance invoice |
| 3 | Launch day | Create the subscription with anchor date = today |
| 4 | Day 1 of next month | Stripe auto-charges, sends receipt |
| 5 | Failed charge | Stripe retries 3× and emails the client. After 7 days, you get a notification — pause the site if not resolved per the contract. |

## Failed payments

Stripe handles retries automatically. After 7 days unpaid:
1. Email the client (not the same as the Stripe dunning email): one paragraph, "Hey — the card on file declined. Want to update it: {link}"
2. Day 14 unpaid: pause the site (Cloudflare Pages → set deployment to "off"). Email them explaining.
3. Day 30 unpaid: end the engagement per the contract's 30-day cancellation clause. Hand off the domain.

## Bookkeeping

Until 5 clients, this is enough:
- One spreadsheet: Date · Client · Amount In · Notes
- Stripe → Reports → exports a CSV monthly
- File income with Schedule C on personal taxes (sole prop)

After 5+ clients: open QuickBooks Solo or Wave (both free for basic).

## What the client sees

- A Stripe-hosted invoice link in their email
- They click "Pay" → enter card or ACH → done in 30 seconds
- Their card stays on file for the monthly subscription
- They get a receipt email after every charge

No signup, no Stripe account, no friction. This is the cheapest way to look professional.
