# Deploy to Vercel — Step by Step

## Quick Facts

- **Cost**: Free (Vercel's hobby plan covers this)
- **Time to live**: 5 minutes
- **Domain**: Can use `checkin.footcandle.org` if you own footcandle.org

---

## Fastest Path: Direct Upload (No GitHub)

### 1. Download These Files
You now have a folder `footcandle-checkin/` with:
- `index.html` (the check-in app)
- `vercel.json` (deployment config)
- `README.md` (documentation)

### 2. Go to Vercel
- Sign into vercel.com with your account
- Click **"Add New"** → **"Project"**

### 3. Upload the Folder
- You'll see "Create From Git" options
- **Scroll down** to **"Don't want to use Git?"**
- Click **"Upload"**
- Drag the `footcandle-checkin` folder into the upload box
- Click **"Deploy"**

### 4. Done!
Your app is live at:
```
https://footcandle-checkin.vercel.app
```

Wait 30 seconds, then open it. You should see the check-in interface.

---

## Add a Custom Domain (Optional but Recommended)

If you own `footcandle.org`:

1. In Vercel dashboard, open the project
2. Go to **Settings** → **Domains**
3. Add **`checkin.footcandle.org`**
4. Follow the DNS instructions (update your domain registrar)
5. Takes 5-10 minutes to propagate

Then your URL becomes: `https://checkin.footcandle.org`

---

## Recommended Path: Use GitHub (For Future Updates)

If you want to make changes later without re-uploading:

### 1. Create a GitHub Repo
```bash
# In your footcandle-checkin folder:
git init
git add .
git commit -m "Initial: Footcandle check-in app"
git branch -M main
git remote add origin https://github.com/YOUR-GITHUB-USERNAME/footcandle-checkin.git
git push -u origin main
```

### 2. Connect to Vercel
- vercel.com → "Add New" → "Project"
- Select the GitHub repo
- Vercel auto-deploys — nothing to configure
- Live in 30 seconds

### 3. Future Updates
Just push to GitHub:
```bash
# Make changes to index.html
git add .
git commit -m "Update check-in UI"
git push
```
Vercel auto-redeploys automatically.

---

## Testing After Deploy

1. **Desktop browser**: Visit your Vercel URL
2. **iPad**: Email yourself the URL, tap it, add to Home Screen
3. **Test the app**:
   - Tap 👥 to load members
   - Create a test event (tap 📅)
   - Check someone in
   - Confirm it shows "🎟 1" next to their name

---

## Troubleshooting

**"Blank page" or 404?**
- Wait 30 seconds for the deploy to finish
- Refresh the page
- Check Vercel dashboard for build errors (there shouldn't be any)

**"Members not loading"?**
- The nightly cron hasn't run yet
- Go to Supabase → Edge Functions → eventive-sync → Test
- Send a request to populate members manually
- Refresh the check-in app

**Want to make changes?**
- Edit `index.html` locally
- If using GitHub: git commit and push (auto-redeploys)
- If using upload: re-upload the folder to Vercel

---

## Your URLs After Deploy

- **Vercel preview**: `https://footcandle-checkin.vercel.app`
- **Custom domain** (if set up): `https://checkin.footcandle.org`
- **Use the custom domain on iPads** (easier to remember)

---

**Once deployed, your check-in app is live and ready to use on iPad at any screening!**
