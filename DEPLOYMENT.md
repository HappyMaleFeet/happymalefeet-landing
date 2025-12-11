# Deployment Guide: GitHub + Namecheap

## Setup GitHub Repository

### Step 1: Create Repository
1. Go to https://github.com/new
2. Name it (e.g., "happymalefeet-landing")
3. Keep it Public or Private (your choice)
4. **Don't** initialize with README (we have one)
5. Click "Create repository"

### Step 2: Push Your Files
Open terminal/command prompt in the folder with your files and run:

```bash
git init
git add .
git commit -m "Initial commit: Landing page with logo and links"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
git push -u origin main
```

Replace `YOUR_USERNAME` and `YOUR_REPO_NAME` with your actual GitHub details.

---

## Deploy to Namecheap (Choose One Method)

### **OPTION 1: Direct Upload to Namecheap (Simplest)**

**Best for:** Quick setup, full control of hosting

1. **Log into Namecheap**
   - Go to your Namecheap account
   - Navigate to Hosting → Manage

2. **Access cPanel**
   - Click "Go to cPanel" button

3. **Upload Files**
   - Find "File Manager" in cPanel
   - Navigate to `public_html` folder
   - Click "Upload"
   - Upload both:
     - `index.html`
     - `HMF_Logo_transparent.png`

4. **Done!**
   - Visit your domain - it should be live immediately

**To Update Later:**
- Make changes locally
- Push to GitHub (for version control)
- Re-upload changed files via cPanel File Manager

---

### **OPTION 2: GitHub Pages + Custom Domain (More Automated)**

**Best for:** Automatic deployments when you push to GitHub

#### A. Enable GitHub Pages

1. **In your GitHub repository:**
   - Go to Settings → Pages
   - Source: Deploy from a branch
   - Branch: `main` → `/root` → Save

2. **Wait 1-2 minutes**
   - GitHub will build your site
   - You'll get a URL like: `https://YOUR_USERNAME.github.io/YOUR_REPO_NAME`

#### B. Connect Your Namecheap Domain

1. **In GitHub Repository Settings → Pages:**
   - Enter your custom domain (e.g., `happymalefeet.com`)
   - Click "Save"
   - Enable "Enforce HTTPS" (after DNS propagates)

2. **In Namecheap Domain Settings:**
   - Go to Domain List → Manage → Advanced DNS
   - Delete existing A Records and CNAME Records for `@` and `www`
   
   **Add these records:**
   
   | Type | Host | Value | TTL |
   |------|------|-------|-----|
   | A Record | @ | 185.199.108.153 | Automatic |
   | A Record | @ | 185.199.109.153 | Automatic |
   | A Record | @ | 185.199.110.153 | Automatic |
   | A Record | @ | 185.199.111.153 | Automatic |
   | CNAME Record | www | YOUR_USERNAME.github.io | Automatic |

3. **Wait for DNS Propagation** (5 minutes - 24 hours)
   - Check status: https://dnschecker.org

4. **Verify in GitHub**
   - Go back to Settings → Pages
   - Should show green checkmark: "DNS check successful"

---

## Which Option Should You Choose?

### Choose Option 1 (Direct Upload) if:
- ✅ You want the simplest setup
- ✅ You have Namecheap hosting already
- ✅ You don't mind manual uploads for updates
- ✅ You want full control

### Choose Option 2 (GitHub Pages) if:
- ✅ You want automatic deployments
- ✅ You're comfortable with GitHub
- ✅ You want free hosting
- ✅ You update frequently and want to just push changes

---

## Making Updates (After Setup)

### If Using Option 1:
1. Edit your files locally
2. Commit to GitHub: `git add . && git commit -m "Updated XYZ" && git push`
3. Upload changed files to Namecheap cPanel

### If Using Option 2:
1. Edit your files locally
2. Commit and push: `git add . && git commit -m "Updated XYZ" && git push`
3. Wait 1-2 minutes - changes are live automatically! ✨

---

## Troubleshooting

**Site not loading?**
- Option 1: Check files are in `public_html`, not a subfolder
- Option 2: DNS can take up to 24 hours to propagate

**Images not showing?**
- Make sure `HMF_Logo_transparent.png` is in the same folder as `index.html`

**Need help?**
- Namecheap Support: https://www.namecheap.com/support/
- GitHub Pages Docs: https://docs.github.com/en/pages
