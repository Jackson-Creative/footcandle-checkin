# Footcandle Film Society — Check-in App

The door check-in app for Footcandle Film Society screenings. It runs on iPads, syncs
live across devices through Supabase, and shares its member data with the
[members portal](https://github.com/Jackson-Creative/footcandle-members-portal).

## Files

- `index.html` — the entire app (HTML, CSS and JavaScript in one file)
- `vercel.json` — static-site config for Vercel
- `VERCEL-DEPLOY.md` — first-time Vercel setup walkthrough
- `CLAUDE.md` — technical notes for Claude Code sessions

## Using the app

1. Open the site on an iPad and **Add to Home Screen**.
2. Members load automatically from the shared database (kept current by the nightly
   Eventive sync). Tap 👥 to import an Eventive CSV export as a backup — check-in history
   is preserved.
3. Tap **📅 + Event** to create a screening, or pick one from the dropdown.
4. Tap a member's name to check them in (tap again to undo). Use search, the A–Z bar
   and the status filters to find people quickly.
5. Tap 📊 for attendance history across all events.

Check-ins appear on every iPad in real time.

## Configuration

The Supabase connection is in the `CONFIG` block at the top of `index.html`:

- `SUPABASE_URL`: `https://rcjvdvyaqfpbqjunmqjf.supabase.co`
- `SUPABASE_ANON_KEY`: the project's publishable key

The publishable key is safe in the browser; access is limited by Supabase row-level
security. If Supabase isn't configured, the app falls back to storing data on that
device only (`localStorage`).

Tables used: `members`, `events`, `checkins` (shared with the members portal).

## Deployment

The app is a static site on Vercel, connected to this GitHub repo. **Pushing to `main`
deploys to production** — there's no build step. See `VERCEL-DEPLOY.md` for first-time
setup and custom-domain instructions.

## Making changes

There are no automated tests. Before merging, open `index.html` in a browser and check
loading members, creating an event, checking someone in and out, the CSV import, and the
iPad layout. Note that it connects to the **live** database.
