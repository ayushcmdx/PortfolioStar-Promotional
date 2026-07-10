# 03 — Visitor Lounge & Real-Time System

> **Free Edition** · Part 3 of 7

---

## What It Is

An always-on **multi-user chat room** embedded in the portfolio. Visitors pick a character name (Marvel/DC/Anime pool) and avatar colour, then chat live with everyone else connected. At ~71 KB, `VisitorLounge.tsx` is the largest file in the codebase — it holds the entire client-side chat system in one component.

---

## Why Server-Sent Events, Not WebSockets

| | SSE | WebSockets |
|---|---|---|
| Vercel support | Native, Node.js runtime | Needs an adapter or paid service |
| Cost | Free | Usually requires Pusher/Ably |
| Direction | Server → Client | Bidirectional |
| Reconnect | Automatic (browser built-in) | Manual |

Since clients only need to send via HTTP POST and receive via a persistent stream, SSE gives nearly all of the real-time UX at zero cost.

---

## Data Flow (Concept)

```
SEND:    Client → POST /api/lounge/send → Redis RPUSH → 200 OK
RECEIVE: Client ← EventSource /api/lounge/stream
             ← server polls Redis every 1.5s
             ← diffs state, sends an SSE event only if changed
```

The stream is a **full-state-replace** model — each update sends the complete current state (messages, presence, typing, poll) rather than a delta. Simpler to reason about, at the cost of slightly larger payloads.

---

## User Identity

No accounts. On first open, a random character name and colour are chosen client-side and stored in `localStorage`, persisting until manually changed. Country flags are resolved server-side from IP headers and attached to each message.

---

## Feature Inventory

**Messaging** — text up to 280 chars, reply threading, timestamp hover, copy-to-clipboard, admin pin.

**Reactions** — 5 emoji options, toggle-able, inline counts.

**Polls** — admin-created, up to 4 options with expiry, one vote per user, live percentages via SSE.

**Presence** — live user count, typing indicators (4s TTL heartbeat).

**File Attachments** — up to 500 KB, images/PDF/text/code, stored as base64 inside the Redis message.

**GIF Search** — Tenor integration via a server-side proxy route.

**Admin Tools** — message deletion and pin/unpin, gated behind an admin key header.

**Sound** — a toggleable notification tone generated with the Web Audio API (no audio file needed).

---

## Message Shape (Simplified)

```ts
type LoungeMessage = {
  id: string
  user: string
  text: string
  ts: number
  country?: string
  reactions?: Record<string, string[]>
  replyTo?: { id: string; user: string; text: string }
  file?: { name: string; type: string; size: number; data: string }
}
```

> 🔒 **Pro edition adds:** the full Redis key schema for the lounge, the exact SSE handler implementation, the client-side connection-management code, and the complete admin auth flow.

---

*Prev: [02 — Visual FX Engine](./02-visual-fx-engine.md) · Next: [04 — KIRO AI Chatbot →](./04-kiro-ai-chatbot.md)*
