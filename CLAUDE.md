# CLAUDE.md — Footcandle Check-in App

Project notes for Claude Code sessions. Keep this file current when behavior changes.

## What this is

The door check-in app for **Footcandle Film Society** screenings, used on iPads
(added to the Home Screen). Owned by Jackson Creative (`Jackson-Creative/footcandle-checkin`).
Companion app: `Jackson-Creative/footcandle-members-portal` (members.footcandle.org),
which shares the same Supabase project.

## Stack

- **One static file: `index.html`** (~780 lines of HTML + CSS + vanilla JS). No build,
  no framework, no package.json, no tests.
- Supabase JS loaded from a CDN at runtime (`loadScript`).
- Hosted on **Vercel** as a static site (`vercel.json`: no build command, output `.`).
  Vercel deploys from GitHub `main`.

## How it works

- `CONFIG` block at the top of `index.html` holds `SUPABASE_URL` and
  `SUPABASE_ANON_KEY` (publishable key — safe in the browser, RLS-protected).
- `buildStore()` picks a backend:
  - **Supabase backend** (live): shared across all iPads. Reads `members`, `events`,
    `checkins`; inserts/deletes `checkins`; inserts `events`; upserts `members`.
  - **Local backend**: `localStorage` only (fallback when Supabase isn't configured).
  Both expose the same `store` interface (`members`, `events`, `checkins`,
  `upsertMembers`, `addEvent`, `setActiveEvent`, `setCheckin`).
- The active event is remembered per device in `localStorage` (`ffs_active_event`).
- **Members** come from Eventive: a server-side Eventive sync (a Supabase Edge
  Function, `eventive-sync`, which is **not in this repo**) and/or a CSV export
  imported via the 👥 button. `membersFromEventiveCsv()` mirrors the sync's mapping.
  Upserts match on `full_name` (Eventive appends numbers to duplicate names).
- UI: A–Z sidebar, search, status filters (active/expired/canceled), 📅 + Event,
  📊 attendance history.

## Gotchas

- Avoid global function names that collide with DOM APIs (a past bug: a global
  `createEvent()` conflicted with `document.createEvent`; it's now `addNewEvent()`).
- The `members` table is also written by the members portal (Stripe webhook, admin).
  A CSV import here overwrites `status` / renewal dates from Eventive data — keep that
  in mind when changing the import or the upsert key.
- No schema in this repo; tables are managed in the Supabase dashboard.

## Testing changes

No automated tests. Open `index.html` in a browser (or `npx serve .`) and check:
loading members, creating an event, toggling check-ins, the CSV import, and
iPad-width layout. Remember it talks to the **live** Supabase database.

## Workflow

- Claude sessions work on a `claude/*` branch and push there; open a PR only when asked.
- Pushing to `main` deploys to production via Vercel.
