# Rudra Capital — Deployment & Email Setup Guide

---

## PART 1 — Set Up EmailJS (5 minutes)

### Step 1 · Create a free account
Go to → https://www.emailjs.com/  
Sign up with **rudracapital.in@gmail.com**

### Step 2 · Add your Email Service
1. Dashboard → **Email Services** → **Add New Service**
2. Choose **Gmail**
3. Click **Connect Account** and sign in with rudracapital.in@gmail.com
4. Click **Create Service**
5. Copy the **Service ID** (looks like `service_xxxxxxx`)

### Step 3 · Create an Email Template
1. Dashboard → **Email Templates** → **Create New Template**
2. Use this template content:

**Subject:**
```
New Enquiry from {{from_name}} — {{subject}}
```

**Body:**
```
You have received a new enquiry from the Rudra Capital website.

Name:    {{from_name}}
Phone:   {{phone}}
Email:   {{from_email}}
Topic:   {{subject}}

Message:
{{message}}

---
Reply directly to this email to respond to the client.
```

3. Set **Reply To** field to: `{{reply_to}}`
4. Set **To Email** to: `rudracapital.in@gmail.com`
5. Click **Save** and copy the **Template ID** (looks like `template_xxxxxxx`)

### Step 4 · Get your Public Key
1. Dashboard → **Account** → **API Keys**
2. Copy your **Public Key**

### Step 5 · Update index.html
Open `index.html` and find these 3 lines near the top (inside the `<head>`):

```js
const EMAILJS_PUBLIC_KEY  = "YOUR_PUBLIC_KEY";
const EMAILJS_SERVICE_ID  = "YOUR_SERVICE_ID";
const EMAILJS_TEMPLATE_ID = "YOUR_TEMPLATE_ID";
```

Replace the placeholder values with your actual keys.

---

## PART 2 — Deploy to Vercel (5 minutes)

### Option A · Drag & Drop (easiest — no account needed temporarily)

1. Go to → https://vercel.com/new
2. Sign up / log in with GitHub or Google
3. Click **"Deploy without a Git repository"** or use **Vercel CLI** (see Option B)

### Option B · Vercel CLI (recommended for future updates)

#### Install CLI
```bash
npm install -g vercel
```

#### Deploy
```bash
cd /path/to/rudra-capital
vercel
```

Follow the prompts:
- Set up and deploy? → **Y**
- Which scope? → your account
- Link to existing project? → **N**
- Project name? → `rudra-capital`
- Directory? → `.` (current folder)

After ~30 seconds you get a live URL like:  
`https://rudra-capital.vercel.app`

#### Deploy updates in future
```bash
vercel --prod
```

### Option C · GitHub + Vercel (best for ongoing edits)

1. Create a GitHub repo and push the `rudra-capital` folder
2. Go to https://vercel.com → **New Project** → Import from GitHub
3. Select the repo → click **Deploy**
4. Every future `git push` auto-deploys ✓

---

## PART 3 · Custom Domain (optional)

1. In Vercel dashboard → your project → **Settings → Domains**
2. Add `rudracapital.in` (or whatever domain you own)
3. Update your domain registrar's DNS with the values Vercel shows

---

## Files in this folder

| File | Purpose |
|------|---------|
| `index.html` | The complete website with EmailJS integrated |
| `vercel.json` | Vercel routing config |
| `SETUP_GUIDE.md` | This guide |

---

## EmailJS Free Tier
- **200 emails/month** — more than enough for a financial advisory site
- Upgrade to Personal plan ($9/mo) for 1,000/month if needed
