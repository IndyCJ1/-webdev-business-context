# Fizzy Admin — Cloudflare Setup (5 min)

The Fizzy mockup at `lanierweb.com/mockups/fizzy/` has a working admin page at `/mockups/fizzy/admin` for editing today's location. It uses Cloudflare Pages Functions + a KV namespace for storage. Both need a one-time setup before the admin can save.

## What you do (one-time, in Cloudflare dashboard)

### 1. Create the KV namespace

1. Cloudflare dashboard → **Workers & Pages** (left sidebar) → **KV** tab
2. **+ Create instance** → name it `FIZZY_KV` → **Add**
3. Done. The namespace is empty for now — that's expected.

### 2. Bind the KV namespace to your Pages project

1. Cloudflare dashboard → **Workers & Pages** → your `cuesseler-web` (or `apex-web`) project
2. **Settings → Bindings** → **Add binding** → choose **KV namespace**
3. Variable name: `FIZZY_KV` (must match exactly)
4. KV namespace: select the `FIZZY_KV` namespace you just created
5. **Save**

### 3. Set the admin password

1. Same project → **Settings → Variables and Secrets**
2. **+ Add** → **Type: Secret** → **Variable name: `FIZZY_PASSWORD`**
3. Value: pick a password you'll remember (e.g. `fizzy-admin-2026`). **Don't use anything you use elsewhere.**
4. **Save**

### 4. Trigger a redeploy so the bindings take effect

1. Same project → **Deployments** tab
2. On the latest production deployment → **⋯** menu → **Retry deployment**
3. Wait ~1 minute for it to rebuild

## How to use it

1. Visit `https://lanierweb.com/mockups/fizzy/admin`
2. Enter the password you set above
3. Update today's location, hours, optional note, open/closed toggle
4. **Save changes**
5. Open `https://lanierweb.com/mockups/fizzy/` in another tab → the yellow banner reflects the change within 60 seconds (CDN cache TTL)

## What the admin can edit

- **Where are you today?** (the location text)
- **Hours** (e.g. "11am – 8pm")
- **Open / Closed today** toggle (closed shows a different banner state)
- **Optional note** (e.g. "Cash only" or "Free for kids")

That's it. Menu items, schedule, photos — those still go through Lanier Web monthly edits in the Starter package, OR upgrade to Plus for full content control.

## Troubleshooting

**Admin page shows "Almost there — admin backend isn't fully configured":**
The `FIZZY_PASSWORD` env var isn't set. Re-do step 3 and redeploy.

**Login works but Save fails with "FIZZY_KV namespace not bound":**
KV binding missing. Re-do step 2 and redeploy.

**Banner on public site doesn't update after saving:**
- Wait 60 seconds (CDN cache TTL)
- Hard refresh (Ctrl+Shift+R) to bypass browser cache
- If still not changing, open browser dev tools → Network tab → reload → check the `location` request returned the new data

## When Fizzy actually signs

Move this admin to their own Cloudflare Pages project under their own domain:
1. Clone the cuesseler-web repo to a new fizzy-specific repo
2. Strip everything except `src/pages/mockups/fizzy/` (rename to `src/pages/`) and `functions/api/fizzy/` (rename to `functions/api/`)
3. Update internal links to remove `/mockups/fizzy/` prefix
4. Deploy as a new Pages project on Fizzy's domain
5. Repeat the KV namespace + env var setup in the new project
6. Their `FIZZY_PASSWORD` is theirs — never share it with anyone

## When to expand the admin

Right now the admin only edits today's location. As Fizzy gets comfortable, easy to add:
- This-week schedule editor (5 days × location/time)
- Menu price toggles (mark items sold-out)
- Closed dates / vacation block

Each addition is roughly 1–2 hours of work. Bill as add-ons or include in the next renewal.
