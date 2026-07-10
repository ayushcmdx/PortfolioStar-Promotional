# Portfolio Architecture Documentation — Free Edition

> A high-level technical overview of the Next.js 15 portfolio codebase. Covers system design, real-time architecture, AI integration, visual FX, data layer, and deployment — at a summary level.

**This is the Free Edition.** It explains *what* the system does and *how the pieces fit together*. It does not include internal implementation math, full API contracts, complete Redis command sequences, or the step-by-step personalisation walkthrough — those are in the **Pro edition**.

---

## Document Index (7 files)

| # | File | What It Covers |
|---|---|---|
| 00 | Index & Overview (this file) | Tech stack, architecture diagram, pages/routes at a glance |
| 01 | Project Structure & Frontend | Directory tree, component model, App Router basics, theming |
| 02 | Visual FX Engine | Galaxy background, 3D globe, glass cursor — concepts only |
| 03 | Visitor Lounge & Real-Time | SSE chat overview, feature list |
| 04 | KIRO AI Chatbot | Groq LLaMA integration, persona design |
| 05 | API & Data Layer | Route summary + Redis schema overview |
| 06 | Customisation & Deployment | Where to edit content, how to deploy to Vercel |

---

## What This Codebase Is

A **production-grade personal portfolio** built on Next.js 15, going beyond a static site with: a real-time multi-user chat room, an AI chatbot (Groq LLaMA 3.3), a photo gallery with live likes, and several canvas-based visual effects. Every dependency runs on a free tier — deployable at ₹0/month.

Three design goals drive the architecture:
1. **Visual richness** — Canvas 3D globe, galaxy particle field, glass cursor
2. **Real interactivity** — SSE live chat, presence, reactions, polls
3. **Minimal infrastructure** — Upstash Redis, Vercel Edge/Node, Groq free tier

---

## Tech Stack at a Glance

| Layer | Technology |
|---|---|
| Framework | Next.js 15 (App Router) |
| Language | TypeScript 5 |
| Styling | TailwindCSS 3 + CSS vars |
| Animation | Framer Motion 11 |
| Scroll | Lenis 1.3 |
| 3D / Canvas | Vanilla Canvas2D (no Three.js) |
| AI Chatbot | Groq API (LLaMA 3.3 70B) |
| Realtime | Upstash Redis + SSE |
| Email | Resend |
| Deployment | Vercel |

---

## System Map (Simplified)

```
Browser (Pages, Components, Canvas FX, Visitor Lounge)
        │  fetch / EventSource
        ▼
┌─────────────┬───────────────┬────────────────┐
│  /api/kiro  │ /api/lounge   │ /api/gallery,   │
│  (Edge)     │ (Node.js)     │ /api/track...   │
└──────┬──────┴───────┬───────┴────────┬────────┘
       ▼               ▼                ▼
   Groq API      Upstash Redis    Upstash Redis
  (LLaMA 3.3)     (chat data)     (gallery/analytics)
```

---

## Pages

| Route | Purpose |
|---|---|
| `/` | Hero, about, projects, skills, enquiry |
| `/about` | Extended bio & timeline |
| `/skills` | Interactive skills matrix |
| `/projects` | Full project grid |
| `/credentials` | Certificates & academic record |
| `/gallery` | Photo gallery with live likes |
| `/spectrum` | Visitor analytics dashboard |
| `/kiro` | AI chatbot |

---

## API Surface (Grouped)

```
/api/kiro            AI chatbot (Edge, Groq)
/api/lounge/*         8 routes — real-time chat system
/api/gallery/*         4 routes — photos + likes
/api/analytics, /api/track, /api/visitors, /api/spectrum
```

Full request/response contracts for every route are covered in **Doc 05** at a summary level, and in complete detail in Pro.

---

## Data Flow (One-Line Summaries)

- **Lounge chat:** Browser → POST `/api/lounge/send` → Redis → SSE stream broadcasts to clients
- **KIRO AI:** Browser → POST `/api/kiro` → Edge function → Groq API → response
- **Gallery likes:** POST `/api/gallery/like` → Redis hash increment
- **Analytics:** POST `/api/track` → Redis hash increment → read via `/api/spectrum`

---

## Required Environment Variables

| Variable | Required |
|---|---|
| `UPSTASH_REDIS_REST_URL` | ✅ |
| `UPSTASH_REDIS_REST_TOKEN` | ✅ |
| `GROQ_API_KEY` | ✅ |
| `LOUNGE_ADMIN_KEY` | ✅ |
| `NEXT_PUBLIC_VAPID_PUBLIC_KEY` / `VAPID_PRIVATE_KEY` | Optional |

---

## Key Design Decisions (Summary)

- **No database** — everything dynamic lives in Redis; its key-value/hash/list types map cleanly onto chat, likes, and analytics.
- **SSE over WebSockets** — native on Vercel Node runtime, free, no extra service needed.
- **Groq over OpenAI** — much faster inference on LLaMA 3.3 70B, snappier first-token latency.
- **Canvas2D over Three.js** — comparable visual quality for these effects, ~600KB lighter bundle.

> 🔒 **Pro edition adds:** the reasoning behind each tradeoff, alternative approaches considered, and migration notes if you outgrow the free-tier stack.

---

*Next: [01 — Project Structure & Frontend Architecture →](./01-project-structure-and-frontend.md)*
