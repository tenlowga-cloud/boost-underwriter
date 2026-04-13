# The Boost Underwriter — Vercel Deployment Guide

## What's in this folder

```
boost-underwriter/
├── index.html        ← The full tool (frontend)
├── api/
│   └── analyze.js    ← The proxy that keeps your API key secret
├── vercel.json       ← Routing config for Vercel
└── README.md         ← This file
```

---

## Step 1 — Create a free Vercel account

Go to https://vercel.com and sign up with GitHub, Google, or email.
(Free tier is all you need — no credit card required for hosting)

---

## Step 2 — Deploy the project

### Option A — Drag and Drop (easiest, no GitHub needed)

1. Go to https://vercel.com/new
2. Scroll down and click **"Browse"** under "Or deploy from your computer"
3. Drag the entire `boost-underwriter` FOLDER onto the upload area
4. Click **Deploy**
5. Wait ~60 seconds — Vercel will give you a live URL like:
   `https://boost-underwriter-abc123.vercel.app`

### Option B — Via GitHub (recommended for future updates)

1. Create a free GitHub account at https://github.com
2. Create a new repository called `boost-underwriter`
3. Upload all files in this folder to that repo
4. Go to https://vercel.com/new
5. Click **"Import Git Repository"** and select your repo
6. Click **Deploy**

---

## Step 3 — Add your Anthropic API key (CRITICAL)

This is what makes the tool work. The key is stored securely on Vercel's servers
and never exposed to the public.

1. Go to your Vercel dashboard: https://vercel.com/dashboard
2. Click on your `boost-underwriter` project
3. Click **Settings** (top menu)
4. Click **Environment Variables** (left sidebar)
5. Click **Add New**
6. Fill in:
   - **Name:** `ANTHROPIC_API_KEY`
   - **Value:** your key (starts with `sk-ant-...`)
   - **Environments:** check Production, Preview, and Development
7. Click **Save**
8. Go back to **Deployments** and click **Redeploy** on your latest deployment
   (the env variable won't take effect until you redeploy)

### Getting your Anthropic API key:
- Go to https://console.anthropic.com
- Sign up or log in
- Click **API Keys** in the left menu
- Click **Create Key**
- Copy the key immediately (you can only see it once)

---

## Step 4 — Use your tool

Your tool is now live at your Vercel URL.

To use a custom domain (e.g. `underwriter.yoursite.com`):
1. In your Vercel project → Settings → Domains
2. Add your domain and follow the DNS instructions

---

## Costs

| Service | Cost |
|---------|------|
| Vercel hosting | Free |
| Anthropic API | ~$0.02–0.05 per analysis |

You only pay Anthropic for actual usage. 100 case analyses ≈ $2–5.

---

## Updating the tool in the future

If you used Option A (drag and drop):
- Go to your Vercel project → Deployments → click the three dots → **Redeploy**
- Or drag a new version of the folder to create a new deployment

If you used Option B (GitHub):
- Push updated files to your GitHub repo
- Vercel automatically redeploys within ~60 seconds

---

## Security notes

- Your `ANTHROPIC_API_KEY` is stored as a server-side environment variable
- It is NEVER sent to the browser or visible in page source
- All API calls go: Browser → Your Vercel server → Anthropic
- The tool has no database and stores no client data
- Each analysis is stateless — nothing is logged or saved server-side
