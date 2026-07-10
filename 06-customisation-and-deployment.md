# 06 — Customisation & Deployment

> **Free Edition** · Part 6 of 7 (final)

---

## Where to Edit Your Content

Personalisation is intentionally centralised. Start here, in this order:

1. **`lib/constants.ts`** — the one file for all editable content: `PROJECTS`, `CREDENTIALS`, `TECH_STACK`, and `SOCIAL_LINKS`. Add/remove array entries to change what's displayed; layouts adapt automatically.
2. **`app/api/kiro/route.ts`** — the AI system prompt. Every `[bracketed placeholder]` needs your real Personal / Education / Career / Projects / Tech Stack / Social Handles info.
3. **`app/kiro/page.tsx`** — the `SUGGESTIONS` array of preset chat questions.
4. **`app/layout.tsx`** — page `metadata` (title, description) and your GA4 measurement ID if using analytics.
5. **`app/page.tsx`** / **`app/about/page.tsx`** — hero heading, bio paragraphs, and stats.

---

## Visual Identity

The signature cyan accent is a single CSS variable in `app/globals.css`:

```css
:root {
  --accent: #00d9ff;  /* change to your brand colour */
}
```

This one value flows through buttons, hover states, the globe wireframe, and the cursor ring. Project screenshots go in `/public/previews/`, certificate images in `/public/certs/`, and the 24 tech-globe icons are configured as a `techLabels` array in `components/Globe3D.tsx`.

---

## Environment Variables

```bash
UPSTASH_REDIS_REST_URL=https://your-db.upstash.io
UPSTASH_REDIS_REST_TOKEN=your-token-here
GROQ_API_KEY=gsk_...
LOUNGE_ADMIN_KEY=any-long-random-string
```

VAPID keys are optional and only needed for browser push notifications.

> 🔒 **Pro edition adds:** the full field-by-field reference for every `PROJECTS`/`CREDENTIALS` entry, the complete system-prompt template with every section filled in as an example, and a pre-publish checklist.

---

## Deployment — Vercel (Recommended)

Vercel is built by the Next.js team and natively supports everything this project needs: App Router, Edge + Node route handlers, SSE on Node functions, and zero-config CI/CD from GitHub. **Cost: ₹0/month** on the Hobby tier for personal traffic.

### Quick Steps

1. **Upstash** — create a free Redis database (region `ap-south-1` for India), copy the REST URL and token from the REST API tab.
2. **Groq** — create a free account at console.groq.com, generate an API key (`gsk_...`).
3. **Vercel** — push to GitHub, import the repo at vercel.com, add the four required env vars under Environment Variables, click Deploy.
4. **Custom domain (optional)** — add it under Settings → Domains; Vercel auto-provisions SSL.

Every subsequent push to `main` triggers an automatic redeploy.

---

## A Note on the SSE Stream and the Hobby Tier

Vercel's Hobby tier caps Node.js function duration at 10 seconds. The Lounge's SSE stream will therefore reconnect roughly every 10 seconds — the browser's `EventSource` handles this automatically, and the only visible effect is a brief typing-indicator reset. This is fine for a portfolio. Upgrading to Vercel Pro (30s functions) removes the reconnect cadence if you want a fully production-grade chat experience.

---

## Post-Deployment Checklist

- [ ] Homepage loads, canvas effects (Galaxy BG, Solar System) initialise
- [ ] `/kiro` responds to a test message
- [ ] Visitor Lounge opens, message history loads, sending works
- [ ] `/gallery` — likes increment
- [ ] `/spectrum` — analytics counters visible
- [ ] Contact form sends (if Resend configured)
- [ ] Custom domain resolves over HTTPS

---

## Scaling Beyond Free Tier

If traffic grows: Upstash moves to pay-as-you-go with no code changes, Vercel Pro adds longer function durations, and Groq credits are inexpensive per token if the free 14,400 requests/day is ever exceeded. None of these require architectural changes — just plan upgrades.

> 🔒 **Pro edition adds:** the complete environment variable reference table, Web Push VAPID setup walkthrough, Google Analytics wiring, and the full Vercel function-limits reference.

---

*Prev: [05 — API & Data Layer](./05-api-and-data-layer.md)*

---

> **End of Free Edition.**
> 7 files covering overview, structure, visual FX, real-time system, AI chatbot, API/data layer, and customisation/deployment — at summary depth.
> The **Pro edition** (10 files) adds full implementation detail: exact math, complete route contracts, full Redis command sequences, the entire AI system prompt template, and a step-by-step personalisation checklist.
