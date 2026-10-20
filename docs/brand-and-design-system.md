# PortfolioStore 99 — Brand & Design System

This document outlines the visual identity, color tokens, typography scales, logo rules, and UI component standards for **PortfolioStore 99** ([portfoliostore99.in](https://www.portfoliostore99.in)).

All promotional pages, marketing assets, and related documentation must strictly adhere to these design conventions.

---

## 1. Brand Palette & Color Tokens

The visual identity is anchored on strong contrast between deep black, crisp white surfaces, and an intense digital orange accent (`#FE5116`).

```
┌─────────────────┐   ┌─────────────────┐   ┌─────────────────┐
│                 │   │                 │   │                 │
│  BRAND ORANGE   │   │   DEEP BLACK    │   │   PURE WHITE    │
│    #FE5116      │   │    #000000      │   │    #FFFFFF      │
│                 │   │                 │   │                 │
└─────────────────┘   └─────────────────┘   └─────────────────┘
```

### Core Palette Values

| Token Name | Hex Code | Primary Usage |
|---|---|---|
| **Brand Orange (Primary Accent)** | `#FE5116` | Primary action buttons, active badges, pricing emphasis, selection highlights, key brand accents. |
| **Brand Orange Glow / Tint** | `rgba(254, 81, 22, 0.15)` | Subtle backdrop highlights, active badge backgrounds, ring focus outlines. |
| **Pure Black** | `#000000` | Deepest contrast background, high-contrast dark mode foundation, primary wordmark text. |
| **Surface Dark (Card Base)** | `#0D0D11` | Background for dark cards, bento grid panels, navigation pill container. |
| **Elevated Dark** | `#14141A` | Hover states for dark cards, interactive buttons, modal headers. |
| **Border Dark** | `#22222B` | Hairline card borders, divider lines, grid lines in dark mode. |
| **Pure White** | `#FFFFFF` | Light mode surface base, primary high-contrast text in dark mode. |
| **Surface Light** | `#F8F9FA` | Light mode card backgrounds, secondary containers. |
| **Border Light** | `#E5E7EB` | Hairline card borders and divider lines in light mode. |
| **Text Primary (Dark / Light)** | `#FFFFFF` / `#111827` | Primary headings, body copy, pricing numbers. |
| **Text Secondary** | `#9CA3AF` / `#4B5563` | Subtitles, feature lists, metadata labels, descriptions. |
| **Text Muted** | `#6B7280` / `#9CA3AF` | Footnotes, copyright text, technical specifications. |

---

## 2. Logo & Brand Mark

### Official Brand Mark
The official logo of PortfolioStore 99 consists of a solid, rounded black square containing the vibrant orange brand initials **`PS`**, paired with the clean typographic wordmark **`PortfolioStore 99`**.

```
┌───────────┐
│  ┌─────┐  │
│  │ PS  │  │   PortfolioStore 99
│  └─────┘  │
└───────────┘
```

- **Reference Assets:**
  - Vector SVG logo: `public/portfoliostore-logo.svg`
  - High-resolution master icon: `public/portfoliostore99.png` (256x256)
  - Browser favicon: `public/portfoliostore99.ico` and `public/favicon.ico`
  - Apple touch icon: `public/apple-touch-icon.png` (180x180)

### Logo Usage Guidelines
- **Faithful Representation:** Preserve the exact proportions of the `PS` initials and the rounded container.
- **No Artificial Effects:** Do **NOT** add drop shadows, outer neon glows, plastic bevels, 3D extrusions, or multi-color rainbow gradients to the logo.
- **Clear Space:** Maintain generous whitespace around the logo to preserve legibility at both 16px favicon scale and 48px hero scale.
- **Contrast:** The logo container must always contrast sharply with the background (black container on light surfaces, or dark container with fine hairline border on dark surfaces).

---

## 3. Typography System

The typography reflects a modern engineering and digital product aesthetic: clean, highly readable, and technically precise.

### Font Families

1. **Heading & Display:** `Plus Jakarta Sans`
   - **Weights:** 500 (Medium), 600 (SemiBold), 700 (Bold), 800 (ExtraBold)
   - **Variable:** `--font-heading`
   - **Usage:** Hero headlines, section titles, template names, pricing numbers.
   - **Characteristics:** Tight tracking (`tracking-tight`), crisp geometric letterforms, modern digital feel.

2. **Body Copy:** `IBM Plex Sans` (or `Inter`)
   - **Weights:** 400 (Regular), 500 (Medium), 600 (SemiBold)
   - **Variable:** `--font-body`
   - **Usage:** Paragraphs, feature explanations, policy documentation, FAQ answers.
   - **Characteristics:** High x-height, open apertures, fatigue-free reading at 14px–16px.

3. **Technical & Metadata:** `IBM Plex Mono`
   - **Weights:** 400 (Regular), 500 (Medium)
   - **Variable:** `--font-mono`
   - **Usage:** Price badges, slug tags, technology stack lists, file counts, license codes.
   - **Characteristics:** Distinct monospaced glyphs that signal raw code, terminal capability, and developer authenticity.

---

## 4. UI Component & Interaction Standards

### A. Buttons & Interactive Controls
- **Primary CTA Button:**
  - Background: Brand Orange (`#FE5116`)
  - Text: White (`#FFFFFF`), font weight 600
  - Border radius: Full pill (`rounded-full`) or clean rounded rectangle (`rounded-xl`)
  - Hover state: Brightness increase (`hover:brightness-110`), subtle scale (`hover:scale-[1.02]`)
  - Transition: `transition-all duration-150 ease-out`
  - Focus Ring: `focus-visible:ring-2 focus-visible:ring-[#FE5116] focus-visible:ring-offset-2`
- **Secondary CTA Button:**
  - Background: Neutral transparent with hairline border (`border border-[#22222B] bg-[#14141A]/50`)
  - Text: High-contrast primary text (`text-white` or `text-gray-900`)
  - Hover state: Background lightens (`hover:bg-[#1E1E26]`), border sharpens
- **Live Preview Button:**
  - Clear icon indicator (external arrow `↗` or eye icon)
  - Opens live deployment in a new browser tab (`target="_blank" rel="noopener noreferrer"`)

### B. Product Cards & Bento Panels
- **Structure:**
  - Hairline border (`1px solid var(--border-theme)`)
  - Subtle corner radius (`rounded-2xl` / 16px)
  - Card background: `#0D0D11` (dark) or `#FFFFFF` (light)
  - Content padding: 20px–24px
- **Preview Image Container:**
  - Fixed aspect ratio (16:9 or 16:10)
  - Overflow hidden with smooth zoom on hover (`group-hover:scale-105 transition-transform duration-300`)
  - Live preview button floating over image or anchored cleanly in the card footer.
- **Badge Elements:**
  - Monospaced, uppercase micro-labels (`text-[11px] font-mono tracking-wider`)
  - Example: `NEWBIE · ₹99`, `GENERAL · ₹199`, `PREMIUM · ₹399`

### C. Visual Decoration Restraint
- **Forbidden:**
  - Excessive emoji decoration (no paragraphs filled with rocket ships, fire, or sparkles).
  - Heavy rainbow gradients or uncontrolled drop shadows.
  - Distracting auto-playing sound effects on the promotional landing page.
- **Encouraged:**
  - Subtle SVG grid backdrops with low opacity (`opacity-[0.03]`).
  - Fine technical separator rules.
  - Interactive tab switchers with smooth spring animations.
  - Clean monospaced badges and data tables.
