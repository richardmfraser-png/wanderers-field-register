# Wanderers Field Register v2 — Update Guide

Brings the Wanderers app up to full parity with TGC v2.1. Your backend URL is already baked into `index.html`, and all existing data (roster, properties, sessions, PIN) carries over untouched.

## What's new

- **Install to phone (PWA):** members can Add to Home Screen (Android: Chrome menu → Install app; iPhone: Safari → Share → Add to Home Screen). Full-screen app with the Wanderers badge as its icon, instant cached loads, and it **opens offline** showing the last synced data — stand assignments and property maps included — with a red banner when disconnected.
- **Stats tab rebuilt as a Stats Explorer:** filters for Year → Weekend → Property → Stand → Shooter, adaptive charts (trend, property/stand leaderboards with maps one tap away, top shooters or a single shooter's log), a **Season log** (date, session, shooters, weather, birds per session), and filtered CSV export. It runs on the results logged in the app; the club's **historical seasons can be loaded in later** — send the spreadsheets whenever ready and they'll be baked in just like TGC's.
- **Live draw refresh:** the Draw and Results tabs re-check the selected session every 25 seconds, so stand claims and bag logs from other phones appear without reloading (pauses while you're mid-selection).
- **Hardened backend + nightly backups** (`Code_WGC_v2.gs`): changes to roster/properties/species/session-list/PIN and all deletions require the admin PIN server-side; member registration and bag logging are unaffected. Nightly backup of the whole store to dated hidden tabs in your Sheet (newest 14 kept).

## Deploy — frontend first, backend second

**Step 1.** Upload these six files to the repo root (Add file → Upload files → commit), replacing `index.html` and adding the rest:
`index.html · sw.js · manifest.webmanifest · icon-192.png · icon-512.png · icon-180.png`
The site works immediately, even before the backend update.

**Step 2.** Open your backend Google Sheet → Extensions → Apps Script. Select all, delete, paste the entire `Code_WGC_v2.gs`, save. Pick **setupBackups** in the function dropdown and press **Run** (authorize if asked). Then **Deploy → Manage deployments → pencil → Version: New version → Deploy** (URL stays the same; don't use "New deployment").
Check: your `/exec` URL in a browser should show `{"ok":true,"service":"WGC Field Register backend v2",...}`.

That's it — no data migration or name cleanup needed here, since Wanderers started with clean data.
