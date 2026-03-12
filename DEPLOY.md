# Deploy Memorix to GitHub Pages with GoDaddy Domain

## Step 1: Create GitHub Repository & Push Code

1. **Create a new repository** on GitHub:
   - Go to [github.com/new](https://github.com/new)
   - Name it `memorix.in` (or any name like `memorix-website`)
   - Set visibility to **Public**
   - Do NOT initialize with README (you already have files)
   - Click **Create repository**

2. **Push your code** from terminal:

```bash
cd /Users/tarunsaxena/Desktop/memorix.in

# Initialize git (if not already)
git init

# Add all files
git add .
git commit -m "Initial commit: Memorix one-pager"

# Add your GitHub repo as remote (replace YOUR_USERNAME with your GitHub username)
git remote add origin https://github.com/YOUR_USERNAME/memorix.in.git

# Push to GitHub
git branch -M main
git push -u origin main
```

## Step 2: Enable GitHub Pages

1. Go to your repo on GitHub → **Settings** → **Pages**
2. Under **Source**, select **Deploy from a branch**
3. Under **Branch**, select `main` and `/ (root)` folder
4. Click **Save**
5. Your site will be live at `https://YOUR_USERNAME.github.io/memorix.in/` (or your repo name)

## Step 3: Add Custom Domain in GitHub

1. In **Settings** → **Pages**, find **Custom domain**
2. Enter: `memorix.in`
3. Click **Save**
4. Wait for DNS check (may show "DNS check is still in progress" until GoDaddy is configured)

## Step 4: Configure GoDaddy DNS

1. Log in to [GoDaddy](https://www.godaddy.com) → **My Products** → **DNS** for memorix.in

2. **Remove conflicting records** (if any):
   - Delete any existing A records for `@` (root)
   - Delete any CNAME for `www` if it conflicts

3. **Add these records**:

| Type | Name | Value | TTL |
|------|------|-------|-----|
| A | @ | 185.199.108.153 | 600 |
| A | @ | 185.199.109.153 | 600 |
| A | @ | 185.199.110.153 | 600 |
| A | @ | 185.199.111.153 | 600 |
| CNAME | www | YOUR_USERNAME.github.io | 600 |

> Replace `YOUR_USERNAME` with your actual GitHub username (e.g., `tarunsaxena`).

4. **Save** and wait 5–60 minutes for DNS propagation.

## Step 5: Enforce HTTPS (Optional)

Once DNS is working:
1. Go back to **Settings** → **Pages**
2. Check **Enforce HTTPS**
3. Your site will be available at `https://memorix.in`

---

## Quick Reference: GoDaddy DNS Setup

- **A records** (4 total for `@`): Point root domain to GitHub Pages
- **CNAME** (for `www`): Points www.memorix.in to your GitHub Pages site

## Troubleshooting

- **DNS not resolving?** Propagation can take up to 48 hours (usually 15–60 mins)
- **Certificate error?** Wait for GitHub to provision SSL after DNS propagates
- **www not working?** Ensure CNAME `www` → `YOUR_USERNAME.github.io` (no `https://`)
