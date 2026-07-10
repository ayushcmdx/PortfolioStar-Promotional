# 05 — API Routes & Data Layer

> **Free Edition** · Part 5 of 7

---

## API Design Philosophy

Every endpoint is a **Next.js Route Handler** (`app/api/*/route.ts`) — no Express server, no separate API process. Routes group into four domains: Lounge (8 routes), Gallery (4), Analytics & Tracking (4), and AI (1).

---

## Route Summary

| Route | Runtime | Auth | Purpose |
|---|---|---|---|
| `GET /api/lounge/stream` | Node.js | None | SSE stream — polls Redis every 1.5s, emits diffs |
| `POST /api/lounge/send` | Node.js | None (rate-limited) | Appends a message, sanitises, trims history to 50 |
| `POST /api/lounge/react` | Node.js | None | Toggles an emoji reaction |
| `POST /api/lounge/typing` | Node.js | None | Sets a 4s-TTL typing indicator |
| `POST /api/lounge/poll` | Node.js | Admin (create/delete) | Poll create/vote/delete |
| `DELETE /api/lounge/delete` | Node.js | Admin key | Removes a message |
| `GET /api/lounge/gif-search` | Node.js | None | Proxies Tenor GIF search |
| `GET /api/kiro` *(actually POST)* | Edge | None | AI chatbot completion |
| `GET /api/gallery` | Node.js | None | Static image manifest |
| `POST /api/gallery/like` | Node.js | None | Increments an image's like count |
| `GET /api/gallery/likes` | Node.js | None | Returns all like counts |
| `POST /api/gallery/visitors` | Node.js | None | Gallery-specific visit counter |
| `POST /api/track` | Node.js | None | Increments country/OS counters |
| `GET /api/spectrum` | Node.js | None | Full analytics read for the dashboard |
| `GET/POST /api/visitors` | Node.js | None | Global visitor counter |
| `GET /api/analytics` | Node.js | None | GA-format analytics data |

**Runtime rule of thumb:** Edge is used only for `/api/kiro` (no Node APIs needed, latency-sensitive). Everything touching Redis or streaming runs on Node.js, since the SSE stream needs Node's streaming capabilities and persistent-connection state.

**Response shapes are consistent throughout:** success → 200 with a JSON payload; client error → 400; auth failure → 403; server error → 500.

---

## Why Redis, Why Upstash

There's no traditional database — everything dynamic lives in **Upstash Redis**, a serverless Redis with an HTTP REST API. This fits three constraints: a free tier generous enough for portfolio traffic (10,000 commands/day, 256 MB), HTTP compatibility with Vercel's stateless functions (no persistent TCP connection needed), and a natural fit between Redis's native structures (lists, hashes, TTL strings) and the app's actual access patterns.

---

## Key Schema (Summary)

| Domain | Key Pattern | Type | Notes |
|---|---|---|---|
| Lounge | `portfolio:lounge:history` | List | Capped at 50 via `LTRIM` |
| Lounge | `portfolio:lounge:presence:<id>` | String, TTL 45s | Auto-expires on disconnect |
| Lounge | `portfolio:lounge:typing:<id>` | String, TTL 4s | Auto-expires on inactivity |
| Lounge | `portfolio:lounge:reactions` | Hash | `messageId → reactions JSON` |
| Lounge | `portfolio:lounge:poll` / `:poll:votes` | String | Active poll + vote counts |
| Gallery | `portfolio:gallery:likes` | Hash | `imageId → count` |
| Gallery | `portfolio:gallery:visitors` | String | Integer counter |
| Analytics | `portfolio:analytics:countries` / `:os` | Hash | Field → visit count |
| Analytics | `portfolio:visitors` | String | Global counter |

**TTL-based presence** is the standout pattern: no cleanup job is needed anywhere. A user's presence or typing key simply expires if their heartbeat stops.

---

## Data Operation Types (Concept)

- **Lists** for chat history — `RPUSH` to append, `LTRIM` to cap size, `LRANGE` to read
- **Hashes** for counters — `HINCRBY` to increment, `HGETALL` to read everything in one round trip
- **TTL strings** for presence/typing — set-and-forget, self-cleaning
- **Atomic counters** — `INCR` for visitor counts, safe under concurrent serverless invocations

All Redis access goes through the official `@upstash/redis` client via `Redis.fromEnv()`, which works in both Node.js and Edge runtimes over HTTP.

---

## Concurrency Notes

Message sends aren't fully atomic as a three-step operation (read/append/trim), so a race under heavy simultaneous traffic could briefly exceed 50 stored messages — self-correcting on the next write, and invisible to users. Reaction toggling uses a read-modify-write pattern with the same tradeoff. Both are acceptable for a portfolio-scale chat feature.

---

## Free Tier Capacity

A portfolio with ~100 visitors/day and a handful of concurrent lounge users stays well under 5,000 of the 10,000 daily command budget.

> 🔒 **Pro edition adds:** full request/response body shapes for all 17 routes, the exact Redis command sequences per route, and a worked capacity-planning table by feature.

---

*Prev: [04 — KIRO AI Chatbot](./04-kiro-ai-chatbot.md) · Next: [06 — Customisation & Deployment →](./06-customisation-and-deployment.md)*
