# PortfolioStore 99 — SEO & AI Search Discovery Guide

This document defines the metadata architecture, search engine optimization (SEO) standards, structured data schemas, and AI search engine discovery recommendations for **PortfolioStore 99** ([portfoliostore99.in](https://www.portfoliostore99.in)) and its promotional landing page.

---

## 1. Grounded Expectations & Principles

To maintain technical integrity:
- **No Ranking Guarantees:** Search engine ranking algorithms (Google, Bing) and Large Language Model retrieval systems (Google AI Overviews, Perplexity, ChatGPT Search, Gemini) are dynamic and non-deterministic. We do **not** claim or promise guaranteed #1 rankings or forced citations in AI answer engines.
- **Focus on Fundamentals:** Maximum search visibility and AI answer citation are achieved through clean semantic HTML, rapid page speed, clear content hierarchy, accurate structured data, and authentic product value.

---

## 2. Core Metadata Architecture

Every public page in the PortfolioStore 99 ecosystem must implement consistent, descriptive metadata:

### Recommended HTML Meta Tags
```html
<!-- Primary Meta Tags -->
<title>PortfolioStore 99 — Ready-Made Developer Portfolio Templates from ₹99</title>
<meta name="title" content="PortfolioStore 99 — Ready-Made Developer Portfolio Templates from ₹99" />
<meta name="description" content="Stop paying monthly website builder subscriptions. Preview real deployed developer portfolio templates with Three.js, Spline 3D, and Next.js. Own 100% of the source code starting at ₹99 flat." />
<meta name="keywords" content="developer portfolio templates, next.js portfolio, three.js portfolio template, react developer portfolio, affordable portfolio templates, portfolio source code, web developer portfolio" />
<link rel="canonical" href="https://www.portfoliostore99.in" />

<!-- Open Graph / Facebook -->
<meta property="og:type" content="website" />
<meta property="og:url" content="https://www.portfoliostore99.in" />
<meta property="og:title" content="PortfolioStore 99 — Ready-Made Developer Portfolio Templates from ₹99" />
<meta property="og:description" content="Preview real deployed developer portfolio templates with Three.js, Spline 3D, and Next.js. Own your source code starting at ₹99 flat." />
<meta property="og:image" content="https://www.portfoliostore99.in/portfoliostore99.png" />

<!-- Twitter / X -->
<meta property="twitter:card" content="summary_large_image" />
<meta property="twitter:url" content="https://www.portfoliostore99.in" />
<meta property="twitter:title" content="PortfolioStore 99 — Ready-Made Developer Portfolio Templates from ₹99" />
<meta property="twitter:description" content="Preview real deployed developer portfolio templates with Three.js, Spline 3D, and Next.js. Own your source code starting at ₹99 flat." />
<meta property="twitter:image" content="https://www.portfoliostore99.in/portfoliostore99.png" />
```

---

## 3. Schema.org Structured Data (JSON-LD)

Implementing structured data enables search engines to display rich snippets (pricing, availability, breadcrumbs) in search results.

### Storefront Organization Schema
```json
{
  "@context": "https://schema.org",
  "@type": "OnlineStore",
  "name": "PortfolioStore 99",
  "url": "https://www.portfoliostore99.in",
  "logo": "https://www.portfoliostore99.in/portfoliostore99.png",
  "description": "Digital storefront providing production-ready, unbundled developer portfolio website templates.",
  "priceRange": "₹99 - ₹399",
  "paymentAccepted": "UPI, Credit Card, Debit Card, Netbanking",
  "currenciesAccepted": "INR, USD"
}
```

### Product Schema (Example for Template: Star)
```json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "Star Developer Portfolio Template",
  "image": "https://www.portfoliostore99.in/templates/store-star-preview.png",
  "description": "Flagship developer portfolio with Spline 3D scenes, AI chatbot, and interactive blog.",
  "brand": {
    "@type": "Brand",
    "name": "PortfolioStore 99"
  },
  "offers": {
    "@type": "Offer",
    "url": "https://www.portfoliostore99.in/templates/store-star",
    "priceCurrency": "INR",
    "price": "199",
    "priceValidUntil": "2027-12-31",
    "availability": "https://schema.org/InStock",
    "itemCondition": "https://schema.org/NewCondition"
  }
}
```

---

## 4. Robots & Indexing Governance

Search engine crawlers and AI search bots must be directed appropriately to maximize discoverability while protecting private transaction pages:

### Recommended `robots.txt` Directives
```txt
User-agent: *
Allow: /
Allow: /templates/
Allow: /privacy-policy
Allow: /terms
Allow: /refund-policy

# Strict Disallow: Prevent indexing of private checkout and order confirmation tokens
Disallow: /checkout/
Disallow: /thank-you
Disallow: /api/

Sitemap: https://www.portfoliostore99.in/sitemap.xml
```

---

## 5. AI Search Engine & LLM Crawler Optimization

Modern developers increasingly discover software tools and templates through AI answer engines (ChatGPT Search, Perplexity AI, Google AI Overviews, Claude, Gemini).

To ensure AI models accurately index and reference PortfolioStore 99:

1. **High Text-to-Code Ratio:** Ensure key product descriptions, pricing figures, tech stacks, and licensing terms are present in clean, server-rendered HTML text rather than embedded solely in images or client-only canvases.
2. **Clear Question-Answer Formats:** The FAQ section should use direct semantic heading tags (`<h3>`) paired with concise answers (`<p>`) matching common user search queries (e.g., *"How much do PortfolioStore 99 templates cost?"*, *"Do I own the code?"*).
3. **Transparent Fact Presentation:** LLM summarizers favor unambiguous numerical data (e.g., *"11 templates across 3 pricing tiers: ₹99, ₹199, ₹399 flat"*).
4. **Accessible Image Descriptions:** Every template screenshot must provide rich descriptive `alt` text (e.g., `alt="Preview of Star template featuring 3D Spline interactive hero, terminal splash screen, and dark theme"`).
