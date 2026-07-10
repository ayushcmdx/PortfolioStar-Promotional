# 01 — Project Structure & Frontend Architecture

> **Free Edition** · Part 1 of 7

---

## Directory Tree (Top Level)

```
portfolio-architecture/
├── app/                    ← Next.js App Router root
│   ├── layout.tsx          ← Root layout: fonts, providers, shell
│   ├── page.tsx             ← Homepage (largest page file)
│   ├── globals.css
│   ├── about/ skills/ projects/ credentials/ gallery/ spectrum/ kiro/
│   └── api/                ← kiro, lounge/*, gallery/*, analytics, track, visitors, spectrum
├── components/              ← 16 shared UI components
├── lib/                     ← constants.ts, types.ts, utils.ts
├── public/                  ← previews/, certs/
└── config files             ← next.config.js, tailwind.config.ts, tsconfig.json
```

The largest files by size are `VisitorLounge.tsx` (~71 KB, the entire chat system), `app/page.tsx` (~44 KB, the homepage), and `Footer.tsx` (~21 KB). This tells you where the complexity concentrates.

---

## Component Categories

| Category | Examples | Behaviour |
|---|---|---|
| **Shell** | `ThemeProvider`, `LenisProvider`, `Navbar`, `Footer` | Mount once in layout, persist across navigation |
| **Page** | `app/*/page.tsx` | Server Components by default, one per route |
| **Feature** | `VisitorLounge`, `Globe3D`, `FluidRippleBg` | Self-contained, stateful client systems |
| **Presentational** | `ProjectCard`, `CredentialCard`, `LiquidButton` | Stateless, driven entirely by props |

---

## The `lib/` Layer

- **`constants.ts`** — single source of truth for content: `PROJECTS`, `CREDENTIALS`, `TECH_STACK` arrays, plus social links. No component hardcodes content strings.
- **`types.ts`** — shared interfaces (e.g. `Project`) used by both constants and components.
- **`utils.ts`** — a single `cn()` helper for merging Tailwind classes.

All imports use the `@/` path alias instead of relative paths.

---

## App Router — Server vs Client

Every file in `app/` is a **React Server Component** by default. Client Components opt in with `'use client'` at the top — used wherever hooks, event listeners, canvas, or browser APIs are needed.

- All `app/*/page.tsx` files → Server Components
- Interactive `components/*.tsx` (chat, canvas FX) → Client Components

This means initial HTML is fully server-rendered and SEO-friendly; interactive features hydrate afterward.

---

## Root Layout Shell

```
RootLayout (Server)
└── ThemeProvider (dark/light context)
    ├── SolarSystemBgClient (always-on bg)
    ├── GlassCursor
    └── LenisProvider (smooth scroll)
        ├── Navbar
        ├── PageTransition → {children}
        └── Footer
```

Navbar, Footer, and the background effects persist across client-side navigation — they never remount.

---

## Theming

Handled via `next-themes`. The design is **dark-first**: default theme is hardcoded to `dark` with `enableSystem={false}`, deliberately ignoring OS preference. Color tokens live as CSS custom properties in `globals.css`:

```css
--background: #0a0a0a
--foreground: #ffffff
--accent: #00d9ff   /* the signature cyan */
--muted: #1a1a1a
--border: rgba(255,255,255,0.08)
```

---

## Motion & Scroll (Summary)

- **Page transitions** — Framer Motion `AnimatePresence`, ~0.3s fade + slight slide, kept subtle.
- **Smooth scroll** — Lenis with a lerp factor of `0.08` replaces native scroll for a fluid feel.
- **Scroll-triggered reveals** — `useInView` fires section animations at 20% visibility.
- **Stagger children** — grids (projects, skills) cascade in with `staggerChildren`.

> 🔒 **Pro edition adds:** full Navbar internals (scroll-aware blur, mobile menu logic), the homepage's full section-by-section breakdown, splash screen implementation, and the complete global CSS reference.

---

*Prev: [00 — Index & Overview](./00-index-and-overview.md) · Next: [02 — Visual FX Engine →](./02-visual-fx-engine.md)*
