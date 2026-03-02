# CoverStitch — Deployment Guide
## From Zero to Live Website (Step-by-Step)

---

## Phase 1: Buy the Domain

### Step 1 — Choose a registrar
Go to **Namecheap** (https://namecheap.com) — affordable, good UI, free WHOIS privacy.

### Step 2 — Search for your domain
Search for `coverstitch.io` (or alternatives like `coverstitch.com`, `coverstitch.net`).

**Pricing reference:**
- `.io` domains: ~$30–40/year
- `.com` domains: ~$10–15/year (if available)
- `.net` / `.co`: ~$10–15/year as fallback

### Step 3 — Purchase
- Add to cart → Checkout
- **Enable "WhoisGuard"** (free on Namecheap) — hides your personal info
- **Turn OFF auto-renew addons** they try to upsell (PremiumDNS, etc.)
- You only need the domain registration itself

### Step 4 — Verify your email
Check your inbox for a verification email from Namecheap/ICANN and confirm it. If you don't verify within ~15 days, the domain gets suspended.

---

## Phase 2: Set Up the Project in VS Code

### Step 5 — Create your project folder
Open your file explorer and create a folder:
```
📁 coverstitch/
   📄 index.html    ← (the file I made for you)
```

That's it. The entire site is one file. Copy the `index.html` I created into this folder.

### Step 6 — Open in VS Code
- Open VS Code
- **File → Open Folder** → select your `coverstitch/` folder
- You should see `index.html` in the sidebar

### Step 7 — Preview locally (optional but recommended)
Install the **"Live Server"** extension in VS Code:
1. Click the **Extensions** icon (left sidebar, looks like 4 squares)
2. Search **"Live Server"** by Ritwick Dey
3. Click **Install**
4. Right-click `index.html` → **"Open with Live Server"**
5. Your site opens at `http://localhost:5500` — test everything works

---

## Phase 3: Set Up Git & GitHub

### Step 8 — Install Git (if you don't have it)
- **Windows:** Download from https://git-scm.com/download/win → run installer with defaults
- **Mac:** Open Terminal, type `git --version` — if not installed, it will prompt you to install Xcode tools

### Step 9 — Create a GitHub account (if needed)
Go to https://github.com and sign up. Free tier is all you need.

### Step 10 — Create a new repository
1. Go to https://github.com/new
2. **Repository name:** `coverstitch`
3. **Description:** `Free online game & movie cover stitching tool`
4. Set it to **Public** (required for free Netlify hosting)
5. **DON'T** check "Add a README" (we already have files)
6. Click **Create repository**

### Step 11 — Push your code to GitHub
GitHub will show you setup commands. Open **Terminal** in VS Code (`Ctrl+`` or `View → Terminal`) and run these one at a time:

```bash
cd path/to/coverstitch

git init

git add .

git commit -m "Initial commit - CoverStitch v1.0"

git branch -M main

git remote add origin https://github.com/YOUR_USERNAME/coverstitch.git

git push -u origin main
```

Replace `YOUR_USERNAME` with your actual GitHub username.

**If Git asks for credentials:**
- GitHub no longer accepts passwords — you'll need a **Personal Access Token**
- Go to: GitHub → Settings → Developer Settings → Personal Access Tokens → Tokens (classic)
- Click "Generate new token" → check `repo` scope → Generate
- Use this token as your password when Git prompts you

---

## Phase 4: Deploy on Netlify

### Step 12 — Create a Netlify account
Go to https://netlify.com → **Sign up with GitHub** (easiest option).

### Step 13 — Connect your repo
1. Once logged in, click **"Add new site"** → **"Import an existing project"**
2. Choose **GitHub**
3. Authorize Netlify to access your repos
4. Select your **coverstitch** repository

### Step 14 — Configure build settings
Netlify will show a build configuration screen:
- **Branch to deploy:** `main`
- **Build command:** *(leave blank — no build needed)*
- **Publish directory:** *(leave blank or type `.`)*
- Click **Deploy site**

### Step 15 — Wait ~30 seconds
Netlify builds and deploys. You'll get a random URL like:
`https://magical-pixie-abc123.netlify.app`

**Visit it. Your site is now LIVE on the internet with free HTTPS.**

---

## Phase 5: Connect Your Custom Domain

### Step 16 — Add domain in Netlify
1. In Netlify, go to **Site settings → Domain management**
2. Click **"Add custom domain"**
3. Type your domain: `coverstitch.io` (or whatever you bought)
4. Click **Verify** → **Add domain**
5. Netlify will also suggest adding `www.coverstitch.io` — add that too

### Step 17 — Update DNS at Namecheap
1. Log into **Namecheap** → **Domain List** → click **Manage** next to your domain
2. Under **Nameservers**, select **"Custom DNS"**
3. Enter Netlify's nameservers (Netlify will show you these, typically):
   ```
   dns1.p03.nsone.net
   dns2.p03.nsone.net
   dns3.p03.nsone.net
   dns4.p03.nsone.net
   ```
4. Click the **green checkmark** to save

**Alternative: Use DNS records instead of nameservers:**
If you prefer to keep Namecheap's nameservers, go to **Advanced DNS** and add:
- **A Record:** Host = `@`, Value = Netlify's load balancer IP (shown in their dashboard)
- **CNAME Record:** Host = `www`, Value = `your-site-name.netlify.app`

### Step 18 — Wait for DNS propagation
DNS changes take **5 minutes to 48 hours** (usually under 30 minutes). You can check progress at https://dnschecker.org

### Step 19 — Enable HTTPS
1. Back in **Netlify → Domain management → HTTPS**
2. Click **"Verify DNS configuration"**
3. Once verified, click **"Provision certificate"**
4. Netlify auto-provisions a free Let's Encrypt SSL certificate
5. Enable **"Force HTTPS"** so all traffic is secure

---

## You're Live! 🎉

Your site is now running at `https://coverstitch.io` (or your domain) with:
- ✅ Free hosting (Netlify free tier = 100GB bandwidth/month)
- ✅ Automatic HTTPS/SSL
- ✅ Global CDN (fast worldwide)
- ✅ Auto-deploys when you push to GitHub

---

## Making Updates

Whenever you want to change the site:

1. Edit `index.html` in VS Code
2. Open Terminal in VS Code and run:
   ```bash
   git add .
   git commit -m "Description of what you changed"
   git push
   ```
3. Netlify auto-detects the push and redeploys in ~15 seconds

---

## Next Steps After Launch

### Add Google AdSense
1. Sign up at https://adsense.google.com
2. Add the AdSense script tag to `<head>` in your HTML
3. Replace the ad placeholder `<div class="ad-space">` with the AdSense ad unit code
4. Wait for approval (can take 1–14 days; site needs some traffic first)

### Add Google Analytics
1. Go to https://analytics.google.com → Create property
2. Add the GA4 tracking script to `<head>`
3. Track visitors, most popular features, traffic sources

### Drive Traffic
- Post to **r/gamecollecting**, **r/customcovers**, **r/retrogaming**, **r/Steelbooks**
- Create a YouTube tutorial: "How to Make Custom Game Covers"
- Write a blog post targeting "printable PS2 covers" / "custom Switch case art"
- Submit to ProductHunt and web tool directories

### SEO Optimization
- Register with **Google Search Console** (https://search.google.com/search-console)
- Submit your sitemap (for a single page, just submit the URL)
- The structured data (JSON-LD) in the HTML will help Google understand your tool
