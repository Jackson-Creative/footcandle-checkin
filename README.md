# Footcandle Film Society — Check-in App

This is the live check-in application for Footcandle Film Society, powered by Supabase.

## Files

- `index.html` — the check-in app (this is checkin-live.html)
- `vercel.json` — Vercel deployment config

## Deployment to Vercel

### Option A: From GitHub (Recommended)

1. **Create a GitHub repository** (or push this folder to an existing one)
   ```bash
   git init
   git add .
   git commit -m "Initial commit: Footcandle check-in app"
   git push -u origin main
   ```

2. **Connect to Vercel**
   - Go to vercel.com, sign in to your account
   - Click "Add New" → "Project"
   - Select the GitHub repo containing this folder
   - Vercel auto-detects it's a static site — no build needed
   - Click "Deploy"
   - Your app is live at `https://[project-name].vercel.app`

3. **Set a custom domain** (optional)
   - In Vercel project settings → Domains
   - Add `checkin.footcandle.org` or similar
   - Follow DNS instructions

### Option B: Direct Upload (Fastest)

1. Go to vercel.com, sign in
2. Click "Add New" → "Project"
3. Under "Create From Git" section, scroll down to "Don't want to use Git?"
4. Select "Upload" and drag this folder into Vercel
5. Deploy — live in seconds

## Configuration

The app comes pre-configured with Supabase credentials:
- `SUPABASE_URL`: `https://rcjvdvyaqfpbqjunmqjf.supabase.co`
- `SUPABASE_ANON_KEY`: `sb_publishable_DUPpA49gmzLkJzv4bGNv6A_adAwJXFl`

These are in the CONFIG block at the top of `index.html`. They're safe (anon key only has read/write access to check-ins per RLS policies).

## Using the App

1. Open on iPad and add to Home Screen
2. Tap 👥 to load members (or wait for nightly Eventive sync)
3. Tap "📅 + Event" to create a screening
4. Tap member names to check them in
5. 📊 shows attendance history across all events
6. Check-ins sync live across all devices (when in Live mode with Supabase)

## Questions?

See `SETUP-COMPLETE.md` and `SETUP-Going-Live.md` in the project folder for full documentation.
