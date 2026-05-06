# Bird Watching

A single-file static web app for logging personal observations of a specific bird's nest. Mobile-first, offline-capable, no backend.

## What's in this folder

- `index.html` — the entire app (HTML + CSS + JS, no dependencies, no build step)

## Run locally

Just open `index.html` in a browser. Or serve it:

```bash
npx serve .
# or
python3 -m http.server 8000
```

## Deploy to Vercel via GitHub

1. Create a new GitHub repo and copy `index.html` (and this README) into the root.
2. Commit and push:
   ```bash
   git init
   git add index.html README.md
   git commit -m "Initial bird-watching app"
   git branch -M main
   git remote add origin git@github.com:YOUR_USER/bird-watching.git
   git push -u origin main
   ```
3. Go to [vercel.com](https://vercel.com) → **Add New… → Project** → import the repo.
4. Settings:
   - **Framework Preset:** Other
   - **Build Command:** *(leave blank)*
   - **Output Directory:** *(leave blank, or `.`)*
   - **Install Command:** *(leave blank)*
5. Click **Deploy**. Done — your URL appears in a few seconds.

## Features

- **One-tap logging** — four big buttons (Yes / No / Just arrived / Just leaving) record current timestamp + day-of-week to localStorage.
- **Smart suggestions** — at the top of the Now tab, 2–3 suggested check times based on bucketed (day-of-week × hour) gone-rate, under-observed slots, and transition zones, filtered to your preferred window.
- **Manual entry / edit** — Add tab, plus Edit/Delete on every history item.
- **Bulk import** — paste lines like `8:32pm friday april 24 - No` or `4:39-4:21pm thursday april 30 - No` and review parse results before committing. Lenient about am/pm, weekday names, time ranges, and status keywords (`yes`, `no`, `just got home` → arrived, `walked in` → arrived, `just leaving` → leaving).
- **Export backup** — copy all data as JSON to clipboard from the More tab.
- **Preferred window setting** — defaults to 11 am–6 pm; suggestions stay inside it.
- **First-run preload** — the seed observations load only if localStorage is empty on first load, then never again (a flag is set so re-clearing won't repopulate).

## Storage

Three localStorage keys:

- `birdwatching:entries:v1` — all observations (array of `{id, timestamp, status, note}`)
- `birdwatching:prefs:v1` — `{startHour, endHour}`
- `birdwatching:preloaded:v1` — flag so seed data only loads once

## Offline

The page is fully self-contained (no external requests), so once the browser caches it, it works without a network. For guaranteed offline behavior, install it to your home screen via your browser's "Add to Home Screen" option.
