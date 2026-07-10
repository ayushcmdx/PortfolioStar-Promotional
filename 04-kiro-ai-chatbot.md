# 04 — KIRO AI Chatbot

> **Free Edition** · Part 4 of 7

---

## What KIRO Is

KIRO lives at `/kiro` and is powered by Groq's LLaMA 3.3 70B via a Next.js Edge Function. It's programmed with a detailed system prompt that makes it an authoritative spokesperson for the portfolio owner — answering questions about background, projects, skills, and availability. Giving it a distinct name (rather than "Chat") makes it feel like an intentional feature rather than a bolted-on LLM widget.

---

## Architecture (Summary)

```
Browser → POST /api/kiro { messages }
        → Edge Function prepends system prompt
        → POST to Groq (llama-3.3-70b-versatile)
        → { content } → rendered in the UI
```

**Why Edge runtime?** No Redis or Node built-ins are needed, so Edge gives faster cold starts and lower latency by running closer to the user.

**Why Groq over OpenAI?** Groq's custom hardware delivers roughly 500–800 tokens/sec on LLaMA 3.3 70B vs. ~50–80 tokens/sec on comparable OpenAI models — meaningfully snappier first-token latency for a chat UX, on a generous free tier.

---

## System Prompt Structure

The prompt is a structured document with named sections (Personal, Education, Personality & Interests, Career Goals, Projects, Tech Stack, Social Handles, and Response Rules). The Response Rules section is what makes KIRO consistently handle recurring recruiter-style questions well — e.g. giving a warm 3–4 sentence summary for "tell me about them," staying specific rather than vague on project questions, and directing genuinely unknown questions to email instead of fabricating answers.

> 🔒 **Pro edition adds:** the complete system prompt template, all section content and formatting rules, and guidance for tuning KIRO's tone/length per section.

---

## Conversation Management

The client keeps the full message history in React state and sends it in full with every request — the model has no server-side memory, so context is reconstructed each call. For a typical 5–15 turn portfolio conversation this is well within LLaMA 3.3's context window and doesn't need trimming.

---

## Chat UI (Summary)

- **Suggestion chips** — 5 preset questions on load, removing first-touch friction
- **Lightweight markdown parsing** — bold/code/bullets rendered without a full markdown library
- **Pulsing-dot loading state** — a CSS animation, not a per-frame React update
- **Auto-scroll** — scrolls to the latest message on update
- **Reset** — clears local state only, no API call

---

## Error Handling (Shapes)

```ts
{ error: 'API key not configured' }        // 500
{ error: data.error?.message }              // forwarded status
{ content: "KIRO's response text" }         // 200
```

The client shows a friendly fallback message rather than a raw error string.

---

## Token Economics

Roughly 300–400 prompt tokens + 100–200 completion tokens per exchange. Groq's free tier (14,400 requests/day on LLaMA 3.3 70B) comfortably covers normal portfolio traffic.

> 🔒 **Pro edition adds:** the full route handler source, the complete `MessageText` markdown parser, and a step-by-step guide to personalising the system prompt.

---

*Prev: [03 — Visitor Lounge & Real-Time](./03-visitor-lounge-realtime.md) · Next: [05 — API & Data Layer →](./05-api-and-data-layer.md)*
