# Tit & Pecker — Landing page

Plain HTML/CSS landing page with branding, logo, and favicon. No build step.

## File structure

```
titandpecker-landing/
├── vercel.json          # proxies /drink-tracker to the existing app
└── public/
    ├── index.html
    ├── tp-logo.png
    ├── favicon.ico
    ├── favicon-16.png / 32.png / 48.png / 180.png / 512.png
    └── fonts/
        └── BigCaslon.ttf
```

## IMPORTANT — before deploying

In `vercel.json`, replace `YOUR-DRINK-TRACKER-PROJECT` with your actual
drink-tracker Vercel deployment URL (e.g. if your drink tracker is at
`drink-tracker-abc123.vercel.app`, use that hostname). Find this in your
Vercel dashboard under the drink-tracker project → Domains.

## Deploy

1. Push this folder to a new GitHub repo (e.g. `titandpecker-landing`).
2. In Vercel: Add New Project → import the repo.
3. Framework preset: **Other** (no build needed — set Output Directory to
   `public`, or just leave defaults since there's no build command).
4. Deploy.
5. In Vercel project settings → Domains, add `titandpecker.com` and
   `www.titandpecker.com`.
6. Vercel will show you DNS records to add at GoDaddy (see below).

## GoDaddy DNS setup

1. Log into GoDaddy → My Products → find `titandpecker.com` → DNS.
2. You'll currently have records forwarding to your drink-tracker Vercel
   project — remove/replace those.
3. Vercel will tell you exactly what to add when you attach the domain in
   step 5 above, typically:
   - An **A record** for the root domain (`@`) pointing to Vercel's IP
     (Vercel shows this exact value, e.g. `76.76.21.21`)
   - A **CNAME record** for `www` pointing to `cname.vercel-dns.com`
4. Remove any existing "forwarding" record GoDaddy set up — that's
   different from DNS records and will conflict.
5. Save changes. DNS propagation can take a few minutes up to a few
   hours.
6. Back in Vercel, the domain should show as "Valid" once DNS propagates.

## How /drink-tracker works

This project doesn't contain the drink tracker code — it's a separate,
independent Vercel deployment. The `rewrites` rule in `vercel.json`
transparently proxies any request to `titandpecker.com/drink-tracker`
through to that other deployment, so visitors never see the underlying
`.vercel.app` URL. Both projects stay independently deployable.
