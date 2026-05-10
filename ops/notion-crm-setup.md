# Notion CRM Setup

A simple lead + client tracker in Notion. ~15 min to set up. Free forever for one user.

## Step 1 — Create the account (2 min)

1. Go to **notion.so** → **Sign up**
2. Use `collier@lanierweb.com` once that mailbox is live, otherwise your Gmail
3. When asked, choose **For personal use** (free plan, no time limit, unlimited pages for one user)
4. Skip the team invite step
5. Install the **Notion mobile app** (iOS / Android) — same login. This is how you'll log walk-ins from your phone.

## Step 2 — Create the database (5 min)

1. In the left sidebar, click **+ Add a page**
2. Title it **Lanier Web — CRM**
3. Inside that page, type `/database` and pick **Database — Full page**
4. Title the database **Leads & Clients**

Now add these properties (the column headers). Click **+** at the right end of the table row, choose the type, and name it.

| Property name | Type | Options (for Select/Multi-select) |
|---|---|---|
| **Business Name** | (already exists as Title) | — |
| **Status** | Select | New · Contacted · Replied · Meeting · Mockup Sent · Proposal Sent · Won · Lost |
| **Industry** | Select | Restaurant · Gym · HVAC · Contractor · Barber · Dentist · Salon · Auto · Other |
| **Owner Name** | Text | — |
| **Phone** | Phone | — |
| **Email** | Email | — |
| **Address** | Text | — |
| **Current Website** | URL | — |
| **First Contact** | Date | — |
| **Last Touch** | Date | — |
| **Next Action** | Text | — |
| **Channel** | Select | Email · Walk-in · Referral · Cold call · Other |
| **Touches** | Number | — |
| **Plan Quoted** | Select | Starter · Plus · Pro · — |
| **Site Issues** | Multi-select | Slow · No mobile · No SEO · Outdated · No site · Bad design · Hard to read |

**Color the Status options** (click each → choose color):
- New = gray · Contacted = yellow · Replied = blue · Meeting = purple · Mockup Sent = orange · Proposal Sent = orange · Won = green · Lost = red

## Step 3 — Create the views (5 min)

Default view is "Table." Add 4 more by clicking **+ Add view** at the top:

### View 1: 🟢 Active Pipeline (Board)
- Type: **Board**
- Group by: **Status**
- Filter: **Status is not** Won, Lost
- Hide property: Address, Site Issues (keep the card clean)

### View 2: 📋 All Leads (Table)
- Type: **Table**
- No filter
- Sort by: **Last Touch** descending

### View 3: ⏰ Needs Follow-up (Table)
- Type: **Table**
- Filter:
  - **Status is not** Won, Lost
  - **AND Last Touch is on or before** "5 days ago" (use the relative-date option)
- Sort by: **Last Touch** ascending (oldest first — these are the most urgent)

### View 4: 🎉 Active Clients (Table)
- Type: **Table**
- Filter: **Status is** Won
- Sort by: **First Contact** descending

### View 5 (optional): 🗓 Calendar
- Type: **Calendar**
- Calendar by: **First Contact**

## Step 4 — Seed it (2 min)

Add 1–3 fake rows so the views aren't empty. Example:

| Business Name | Status | Industry | Owner | Phone | First Contact | Channel |
|---|---|---|---|---|---|---|
| Hogtown Smoke (test) | New | Restaurant | Test User | (770) 555-0199 | today | Cold call |

Delete after the first real lead.

## Step 5 — Daily use

**When you find a new lead** (Google Maps walk, drive-by, referral):
- Open Notion mobile app or web
- Add a new row in **All Leads**
- Set **Status = New**, **First Contact = today**, **Channel** = how you found them
- Click into the row to open the page — paste any notes, screenshots, audit notes here

**When you send a cold email:**
- Bump **Touches** by 1
- Update **Last Touch** to today
- Update **Status** to **Contacted** (if it was New)
- Inside the row's page, paste the email you sent (so you remember which template — copy/paste counts)

**When they reply:**
- **Status** → **Replied**
- Inside the page, paste their reply
- Update **Next Action** ("Send mockup by Friday")

**When you book a meeting:**
- **Status** → **Meeting**
- Inside the page, paste meeting notes after the call

**When they sign:**
- **Status** → **Won**
- They now show up in the **Active Clients** view
- Time to start the onboarding-checklist.md flow

**When they ghost or pass:**
- **Status** → **Lost**
- Add a note inside the page about why (so you can spot patterns later)

## Step 6 — Email logging shortcut (optional, do later)

To stop pasting emails manually, you can:
- Forward sent emails to Notion via email-to-page (paid feature, $8/mo) — **skip until 5+ active leads**
- Or use a free Zapier zap: Gmail → Notion (filter by sender = `collier@lanierweb.com`)

For now, manual paste is fine. You won't have hundreds of leads on day one.

## Step 7 — Mobile habits

- Pin **Active Pipeline** as your default view
- On the phone, open Notion → Lanier Web — CRM → Active Pipeline. Add walk-ins immediately while you're standing outside the business.

## What this replaces

This single Notion database replaces:
- The spreadsheet mentioned in `outreach/target-list-workflow.md` (✅ done — use this instead)
- A formal CRM (Pipedrive, HubSpot) until you're at 20+ active leads
- Sticky notes / phone notes / "I'll remember"

## When to upgrade past Notion

Stay on Notion until **at least one** of these is true:
- You have 50+ leads and the database starts feeling slow
- You're sending 100+ emails per month and need real automation
- You hire a second person who needs collaborative access (Notion's free plan limits guests)

At that point look at: **HubSpot Free CRM** (free forever, real CRM features) or **Pipedrive** ($15/mo per user, sales-focused).

But honestly — most local web design agencies could run on a Notion table their entire life.
