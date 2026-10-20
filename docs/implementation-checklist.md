# PortfolioStore 99 — Implementation Checklist

This checklist defines the technical verification steps, design audit criteria, and deployment milestones for the future implementation of the **PortfolioStore 99 Promotional Landing Page**.

> **Current Project Status:**  
> **Phase 1: Architecture & Specification — COMPLETED**  
> **Phase 2: Promotional Website Implementation — NOT STARTED (Pending Separate Authorization)**

---

## 1. Business & Catalog Verification Checklist

- [x] Verify production website URL: `https://www.portfoliostore99.in`.
- [x] Verify private store repository: `https://github.com/ayushcmdx/PortfolioStore`.
- [x] Verify promotional documentation repository: `https://github.com/ayushcmdx/PortfolioStar-Promotional`.
- [x] Verify full 11-template catalog in `data/templates.js`.
- [x] Verify pricing tiers:
  - [x] Newbie Tier: ₹99 flat (`store-outlet`)
  - [x] General Tier: ₹199 flat (`store-star`, `store-houseblue`, `store-parchment`)
  - [x] Premium Tier: ₹399 flat (`store-desktop`, `store-neon`, `store-hazebloom`, `store-cyanlight`, `store-artcraft`, `store-typo`, `store-3dhome`)
- [x] Verify all 11 live Vercel preview deployment URLs.
- [x] Verify official policy routes (`/privacy-policy`, `/terms`, `/refund-policy`).
- [x] Verify support email (`portfoliostore99@gmail.com`) and WhatsApp (`+91 7587246554`).

---

## 2. Brand & Visual Design Audit Checklist

- [ ] Primary brand orange `#FE5116` applied consistently to action buttons, active badges, and pricing highlights.
- [ ] Black (`#000000` / `#0D0D11`) and White (`#FFFFFF`) establish sharp, readable contrast.
- [ ] Official `PS` logo container rendered faithfully without distorting proportions or adding artificial neon glows.
- [ ] Heading typography implemented with Plus Jakarta Sans (`--font-heading`).
- [ ] Body copy implemented with IBM Plex Sans / Inter (`--font-body`).
- [ ] Technical tags and pricing pills implemented with IBM Plex Mono (`--font-mono`).
- [ ] Restrained visual design: no emoji clutter, no tacky gradients, clean hairline borders (`border-[var(--border-theme)]`).

---

## 3. Page Structure & Component Implementation Checklist

- [ ] **Sticky Header:** Logo, links to `#catalog`, `#why-us`, `#how-it-works`, `#faq`, and a prominent `Visit Storefront ↗` CTA pill.
- [ ] **Hero Section:** Core value headline, concise description, primary CTA `Browse All 11 Templates`, secondary CTA `See How It Works`.
- [ ] **Hero Visual Mockup:** High-impact showcase of 3 flagship templates (Star, Typo, 3d-Home).
- [ ] **Technical Trust Bar:** Unbundled code, free Vercel hosting, Google Drive delivery, Razorpay security.
- [ ] **Filterable Catalog Showcase:**
  - [ ] Tab filters for All (11), Newbie (₹99), General (₹199), and Premium (₹399).
  - [ ] 11 product cards with screenshots, tech stacks, descriptions, and INR prices.
  - [ ] Every card features a `Live Demo ↗` button opening the real Vercel preview.
  - [ ] Every card features a `Get Template` button routing to `https://www.portfoliostore99.in/templates/[slug]`.
- [ ] **Why PortfolioStore 99:** 6-card bento grid detailing true code ownership, zero monthly fees, live demos, and human support.
- [ ] **Direct Comparison Matrix:** Side-by-side table comparing PortfolioStore 99 with Framer/Squarespace and free GitHub themes.
- [ ] **How It Works (4 Steps):** Visual flow covering Explore &rarr; Instant Checkout &rarr; Download &rarr; Deploy in Minutes.
- [ ] **Target Audience:** Personas for CS students, junior engineers, frontend devs, freelancers, and career switchers.
- [ ] **FAQ Accordion:** 10 verified Q&As covering file deliverables, zero subscriptions, payment methods, replacement policy, and support.
- [ ] **Final CTA Banner:** High-contrast conversion block routing visitors to `https://www.portfoliostore99.in`.
- [ ] **Global Footer:** Official brand mark, tier links, verified policy links, WhatsApp/email support, and copyright statement.

---

## 4. Responsive & Accessibility Audit Checklist

- [ ] Mobile Layout (<640px): Single-column cards, touch-friendly tap targets (&ge;48px), responsive drawer/header.
- [ ] Tablet Layout (640px – 1024px): 2-column grid, responsive tables, fluid font scaling.
- [ ] Desktop Layout (&ge;1024px): 3-column catalog grid, full comparison matrix.
- [ ] WCAG 2.1 AA Color Contrast: Minimum 4.5:1 for body text, 3:1 for large display titles.
- [ ] Keyboard Accessibility: Visible focus rings on all buttons, tabs, and interactive links.
- [ ] Image Optimization: Modern WebP formats with explicit dimensions and descriptive `alt` tags.
- [ ] Motion Accessibility: Respects `prefers-reduced-motion: reduce`.

---

## 5. SEO & Structured Data Checklist

- [ ] Title tag: `PortfolioStore 99 — Ready-Made Developer Portfolio Templates from ₹99`.
- [ ] Meta description under 160 characters describing unbundled code and zero recurring fees.
- [ ] Canonical URL pointing to `https://www.portfoliostore99.in`.
- [ ] Open Graph (`og:*`) and Twitter Card (`twitter:*`) tags configured with `portfoliostore99.png`.
- [ ] Schema.org JSON-LD structured data for `OnlineStore` and individual `Product` templates.
- [ ] Semantic HTML tags used throughout (`<header>`, `<main>`, `<section>`, `<nav>`, `<footer>`).

---

## 6. Architecture & Security Boundary Checklist

- [ ] Confirm the promotional page is **strictly presentational**.
- [ ] Confirm no Razorpay API routes or checkout handlers are duplicated in the promotional site.
- [ ] Confirm no direct database connections to Neon PostgreSQL exist in the promotional site.
- [ ] Confirm no Google Drive download URLs or transactional email triggers are exposed in client-side code.
- [ ] Confirm all purchase buttons redirect users to `https://www.portfoliostore99.in/checkout/[slug]`.
- [ ] Confirm zero private API keys, secrets, or customer records are present in the repository.
