# PortfolioStore 99 — Promotional Landing Page Specification

## 1. Document Overview

This document specifies the complete architectural, visual, content, and functional requirements for a dedicated promotional landing page for **PortfolioStore 99** ([portfoliostore99.in](https://www.portfoliostore99.in)).

The purpose of this specification is to provide a developer, designer, or autonomous coding agent with a complete blueprint to build the promotional page without needing to re-engineer the business model or guess at design decisions.

> **Status:** Specification Complete — Implementation Pending Approval.  
> **Target Storefront:** `https://www.portfoliostore99.in`  
> **Brand Accent:** `#FE5116`  
> **Catalog Size:** 11 Verified Templates (₹99 – ₹399)

---

## 2. Page Objectives & Key Metrics

1. **Immediate Value Communication:** Within 5 seconds, communicate that PortfolioStore 99 offers **production-ready portfolio website templates and complete source code** starting at ₹99 flat with zero recurring subscriptions.
2. **Interactive Proof:** Enable visitors to launch live interactive deployments of templates on Vercel directly from the page.
3. **High-Conversion Routing:** Guide qualified visitors seamlessly to the primary storefront (`https://www.portfoliostore99.in`) and dedicated checkout pages (`/checkout/[slug]`).
4. **Trust Building:** Emphasize domestic payment ease (UPI QR, cards, netbanking via Razorpay), instant Google Drive file delivery, and the fair 7-day one-time replacement policy.

---

## 3. Section-by-Section Wireframe & Specification

```
┌─────────────────────────────────────────────────────────────┐
│ 1. Header / Navigation (Sticky Bar)                         │
├─────────────────────────────────────────────────────────────┤
│ 2. Hero Section (Headline, Value Hook, Dual CTAs, Mockups)  │
├─────────────────────────────────────────────────────────────┤
│ 3. Social Proof & Architecture Badges (Vercel, React, Drive)│
├─────────────────────────────────────────────────────────────┤
│ 4. Verified Catalog Showcase (11 Filterable Template Cards) │
├─────────────────────────────────────────────────────────────┤
│ 5. Value Proposition: "Why PortfolioStore 99?"              │
├─────────────────────────────────────────────────────────────┤
│ 6. Comparison Table (PortfolioStore 99 vs. Monthly Builders)│
├─────────────────────────────────────────────────────────────┤
│ 7. How It Works (4-Step Purchase & Deployment Journey)      │
├─────────────────────────────────────────────────────────────┤
│ 8. Target Audience & Personas                               │
├─────────────────────────────────────────────────────────────┤
│ 9. Frequently Asked Questions (Accordion)                   │
├─────────────────────────────────────────────────────────────┤
│ 10. Final Call-to-Action Banner                             │
├─────────────────────────────────────────────────────────────┤
│ 11. Footer (Official Links, Verified Policies, Support)     │
└─────────────────────────────────────────────────────────────┘
```

---

### Section 1: Sticky Navigation Bar
- **Purpose:** Provide instant brand recognition, effortless section navigation, and a prominent persistent CTA to browse the live store.
- **Components:**
  - **Brand Logo:** `PS` icon (black rounded container with orange initials) + `PortfolioStore 99` wordmark, linking to `https://www.portfoliostore99.in`.
  - **Nav Links:**
    - `Catalog` &rarr; jumps to Section 4 (`#catalog`)
    - `Why PS99` &rarr; jumps to Section 5 (`#why-us`)
    - `How It Works` &rarr; jumps to Section 7 (`#how-it-works`)
    - `FAQ` &rarr; jumps to Section 9 (`#faq`)
  - **Right CTA Button:**
    - Text: `Visit Storefront ↗`
    - Style: Pill button (`rounded-full`), Brand Orange (`#FE5116`), white text, bold font.
    - Action: Opens `https://www.portfoliostore99.in` in a new tab.
- **Responsive Behavior:**
  - On mobile (<768px): Collapse links into a clean slide-over drawer or minimalistic header with Logo + `Visit Store` pill.

---

### Section 2: Hero Section
- **Purpose:** Capture attention, articulate the core value proposition, and provide visual evidence of template quality immediately.
- **Copywriting Direction:**
  - **Badge / Micro-label:** `VERIFIED NEXT.JS & THREE.JS TEMPLATES · FLAT ₹99 – ₹399`
  - **Headline:**
    > **Own Your Portfolio Code.**  
    > **Stop Paying Monthly Builder Subscriptions.**
  - **Subheadline:**
    > Production-ready, unbundled developer portfolio templates with real interactive 3D scenes, terminal emulators, and dynamic themes. Pay once starting at ₹99 flat, own 100% of the source code, and host for free on Vercel forever.
  - **Primary CTA:**
    - Text: `Browse All 11 Templates`
    - Action: Smooth scroll to `#catalog` or link to `https://www.portfoliostore99.in/#catalog`.
  - **Secondary CTA:**
    - Text: `See How It Works`
    - Action: Smooth scroll to `#how-it-works`.
- **Hero Visual Showcase:**
  - A responsive 3-card isometric floating carousel or bento preview highlighting three contrasting template styles:
    1. **Star** (Spline 3D Flagship & AI Chatbot)
    2. **Typo** (Orbiting tech stack rings & GSAP target crosshair)
    3. **3d-Home** (3D isometric island universe & Three.js robot companion)
  - Each card displays real screenshot thumbnails, a monospaced price badge, and an interactive "Live Demo" button.

---

### Section 3: Technical Trust Bar
- **Purpose:** Reassure developers about the technical legitimacy and freedom of the platform.
- **Content:**
  - `✓ 100% Unbundled Source Code (React 19, Next.js 15, Vite, Three.js)`
  - `✓ Free Forever Hosting on Vercel / Netlify / GitHub Pages`
  - `✓ Instant Automated Google Drive File Delivery`
  - `✓ Secured by Razorpay Standard Checkout (UPI QR, Cards, Netbanking)`

---

### Section 4: Verified Product Catalog Showcase
- **Purpose:** Present all 11 real portfolio templates with transparent pricing, verified preview URLs, and direct storefront links.
- **Interactive Controls:**
  - Category filter tabs:
    - **All Templates (11)**
    - **Newbie Tier (₹99)** — Starter single-page portfolios.
    - **General Tier (₹199)** — Spline 3D, Three.js rooms, editorial parchment themes.
    - **Premium Tier (₹399)** — macOS desktop, cyber CRT terminal, WebGL shaders, 3D island universes.
- **Card Layout & Components (For each of the 11 products):**
  - High-resolution preview image with subtle hover zoom.
  - Category badge + INR price callout:
    - `Outlet`: ₹99 flat
    - `Star`: ₹199 flat
    - `HouseBlue`: ₹199 flat
    - `Parchment`: ₹199 flat
    - `Desktop`: ₹399 flat
    - `Neon`: ₹399 flat
    - `Hazebloom`: ₹399 flat
    - `CyanLight`: ₹399 flat
    - `ArtCraft`: ₹399 flat
    - `Typo`: ₹399 flat
    - `3d-Home`: ₹399 flat
  - Product name and 1-line punchy description.
  - Monospaced technology stack pill badges (e.g., `Three.js`, `GSAP`, `Next.js 15`, `Tailwind v4`).
  - Dual action buttons:
    - `Live Demo ↗` &rarr; Opens the dedicated Vercel deployment (e.g., `https://store-star.vercel.app`).
    - `Get Template` &rarr; Links directly to `https://www.portfoliostore99.in/templates/[slug]`.

---

### Section 5: Why PortfolioStore 99? (Core Value Propositions)
- **Grid Layout (3x2 Bento Layout):**
  1. **True Code Ownership:** You receive the raw, unminified source code. No proprietary lock-in, no closed platforms.
  2. **Zero Recurring Fees:** Pay once. Never pay ₹2,000/month just to keep your custom domain connected to a builder.
  3. **Live Deployed Previews:** What you see is exactly what you get. Every template runs live on Vercel before you spend a single rupee.
  4. **Diverse Visual Aesthetics:** From retro CRT scanlines and vintage book codices to interactive 3D islands and macOS desktops.
  5. **Instant Delivery:** Download links are delivered immediately on your confirmation screen and emailed via Google Drive.
  6. **Human Developer Support:** Direct setup guidance via WhatsApp (`@ayushcmd`) if you ever get stuck running or deploying your template.

---

### Section 6: Direct Comparison Table
- **Purpose:** Dramatically illustrate the financial and technical contrast between PortfolioStore 99 and traditional website builders.

| Feature / Capability | PortfolioStore 99 | Proprietary Builders (Framer / Squarespace) | Generic Free GitHub Themes |
|---|---|---|---|
| **Pricing Model** | **₹99 – ₹399 One-Time Flat** | ₹1,200 – ₹3,500+ / Month Recurring | Free (Often unmaintained) |
| **Code Ownership** | **100% Unbundled Source Code** | Locked in proprietary platform | Varies (often fragmented) |
| **Hosting Cost** | **Free (Vercel / Netlify / GitHub)** | Must pay builder monthly fee | Free |
| **Interactive 3D / WebGL** | **Included (Three.js, Spline, Shaders)** | Extra plugins / heavy workarounds | Rarely present or broken |
| **Live Deployed Demos** | **100% Verified Vercel Demos** | Preview limited to designer canvas | Frequently broken links |
| **Setup Support** | **Direct WhatsApp & Email Support** | Ticket queue or forum | None |

---

### Section 7: How It Works (4 Simple Steps)
1. **Explore & Preview:** Browse the catalog and click **Live Demo** to test real 3D physics, theme toggles, and mobile layouts on Vercel.
2. **Instant Checkout:** Click **Buy Template**, enter your name and email, and complete payment securely via Razorpay (UPI QR, Google Pay, Cards, Netbanking).
3. **Download Codebase:** Immediately receive your secure Google Drive download link on screen and via automated email receipt.
4. **Deploy in Minutes:** Unzip the folder, add your personal bio and project links, and run `vercel` or link to GitHub for instant free hosting.

---

### Section 8: Target Audience & Use Cases
- **Students & Graduates:** Stand out in placement drives with a portfolio that looks like it took 3 months to build.
- **Frontend & Full-Stack Developers:** Upgrade from a basic resume to an interactive developer playground without burning your weekends.
- **Freelancers & Consultants:** Impress clients with high-end digital rooms, bento layouts, and case study presentations.
- **Career Switchers:** Establish technical credibility immediately with modern UI engineering standards.

---

### Section 9: Frequently Asked Questions (FAQ)

1. **What exactly is PortfolioStore 99?**  
   PortfolioStore 99 is a digital storefront offering ready-made, production-tested personal portfolio website templates. We provide complete unbundled source code for a one-time flat fee starting at ₹99.

2. **What files and assets do I receive after purchase?**  
   You receive a complete `.zip` archive containing the production frontend source code (React, Next.js, or Vite), styling configurations, component libraries, 3D asset models, icons, and a step-by-step setup and hosting guide.

3. **Can I preview the templates before buying?**  
   Yes! Every single template in our store has a live, working Vercel deployment link. You can interact with the animations, test dark/light mode toggles, and verify mobile responsiveness on your own device before purchasing.

4. **Are there any monthly subscription fees?**  
   None. All purchases are 100% one-time flat payments. Once you download the code, you own it permanently and can host it for free on Vercel, Netlify, or GitHub Pages.

5. **How does payment work?**  
   Payments are securely processed through Razorpay Standard Checkout. We accept all major Indian payment methods including UPI (Google Pay, PhonePe, Paytm, CRED), Debit/Credit Cards, and Netbanking.

6. **How is the source code delivered?**  
   Fulfillment is automated. Once payment succeeds, you are immediately redirected to an Order Confirmation page with a direct Google Drive download button. An email receipt containing the persistent download link is also sent to your inbox.

7. **Do I need advanced coding skills to customize a template?**  
   No. If you know basic HTML/JavaScript or React, you can customize your name, bio, social links, and project cards in under 15 minutes by editing a single configuration file.

8. **Can I use the template for my commercial personal brand or client projects?**  
   Yes. Each purchase grants a perpetual, single-user license to customize and deploy the website for your own personal brand or for a client project. Reselling or redistributing the raw template code is prohibited.

9. **What is your refund policy?**  
   Because our products are delivered digitally as full source code archives, we do not offer refunds after delivery. However, we offer a fair **one-time replacement option** within 7 days: you can swap your template for any other template in our catalog by paying 50% of the new template's listed price. Furthermore, if any deliverable is corrupted or defective, we replace or fix it free of charge.

10. **What if I get stuck during setup?**  
    We provide direct developer support! You can message us directly on WhatsApp at `@ayushcmd` (`+91 7587246554`) or email `portfoliostore99@gmail.com`.

---

### Section 10: Final Call to Action
- **Visual Design:** High-contrast dark container with subtle orange border accent and background mesh.
- **Headline:** `Ready to Own Your Developer Portfolio?`
- **Subline:** `Join hundreds of developers who stopped paying monthly builder subscriptions. Pick your template and launch today.`
- **Primary Action Button:** `Browse Templates on PortfolioStore 99 ↗` (Links to `https://www.portfoliostore99.in`).

---

### Section 11: Global Footer
- **Branding:** PortfolioStore 99 logo + wordmark.
- **Catalog Links:** Newbie Tier (₹99), General Tier (₹199), Premium Tier (₹399).
- **Verified Policy Links:**
  - Privacy Policy: `https://www.portfoliostore99.in/privacy-policy`
  - Terms of Service: `https://www.portfoliostore99.in/terms`
  - Refund Policy: `https://www.portfoliostore99.in/refund-policy`
- **Verified Contact & Support:**
  - Email: `portfoliostore99@gmail.com`
  - WhatsApp: `https://wa.me/917587246554` (`@ayushcmd`)
- **Copyright & Transparency Statement:**  
  `© 2026 PortfolioStore 99. All rights reserved. Zero builder lock-in · Unbundled source code.`

---

## 4. Technical & Responsive Requirements

### A. Responsive Breakpoints
- **Mobile (<640px):** Single-column catalog grid, stacked buttons, drawer navigation, touch-friendly tap targets (&ge;48px).
- **Tablet (640px – 1024px):** Two-column catalog grid, compact comparison table, balanced typography.
- **Desktop (&ge;1024px):** Three-column catalog grid, full horizontal comparison matrix, persistent sticky navigation bar.

### B. Accessibility & Performance Benchmarks
- **Color Contrast:** All text must maintain a minimum WCAG 2.1 AA contrast ratio (4.5:1 for body copy, 3:1 for large display titles).
- **Keyboard Navigation:** Every button, tab, and link must display an unmistakable focus ring (`focus-visible:ring-2 focus-visible:ring-[#FE5116]`).
- **Image Optimization:** All template preview images must be served in WebP or modern formats with explicit `width`, `height`, and descriptive `alt` text.
- **Motion Accessibility:** Respect user preferences via `prefers-reduced-motion: reduce` by disabling non-essential floating transforms and transition scale animations.
