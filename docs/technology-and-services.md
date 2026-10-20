# PortfolioStore 99 — Technology & Infrastructure Architecture

This document outlines the verified technology stack, third-party infrastructure services, and architectural boundaries governing **PortfolioStore 99** ([portfoliostore99.in](https://www.portfoliostore99.in)).

---

## 1. Production Architecture Overview

The PortfolioStore 99 storefront is engineered on a modern serverless architecture designed for high availability, zero-maintenance operational overhead, and rapid static page delivery:

```
┌─────────────────────────────────────────────────────────────┐
│                 Client Browser / Visitor                    │
└──────────────────────────────┬──────────────────────────────┘
                               │
                HTTPS Requests │ Next.js 14 App Router
                               ▼
┌─────────────────────────────────────────────────────────────┐
│                    Vercel Edge & Serverless                 │
│  - Static Page Pre-rendering (24 SSG Routes)                │
│  - Dynamic API Endpoints (/api/razorpay/*, /api/orders/*)   │
└───────────────┬─────────────────────────────┬───────────────┘
                │                             │
   Payment Flow │ Webhook / API               │ SQL Queries
                ▼                             ▼
┌──────────────────────────────┐ ┌────────────────────────────┐
│      Razorpay Gateway        │ │  Neon Serverless Postgres  │
│  - UPI QR, Cards, Netbanking │ │  - Orders Table            │
│  - HMAC-SHA256 Signatures    │ │  - Payment Status Logs     │
└───────────────┬──────────────┘ └────────────────────────────┘
                │
                │ Verified Payment Event
                ▼
┌─────────────────────────────────────────────────────────────┐
│               Automated Fulfillment Services                │
│  - Resend: Transactional Order Receipt Emails               │
│  - Google Drive: Persistent Digital Source Code Delivery    │
└─────────────────────────────────────────────────────────────┘
```

---

## 2. Verified Service Registry

| Service | Category | Technical Role in Storefront | Configuration Source |
|---|---|---|---|
| **Next.js 14 (App Router)** | Web Framework | Server-Side Rendering (SSR), Static Site Generation (SSG), and API route handlers. | `next.config.mjs`, `package.json` |
| **React 18** | UI Library | Component-driven UI rendering, state management, and theme transitions. | `package.json` |
| **Tailwind CSS** | Styling Engine | Utility-first CSS with custom CSS variables for light/dark theme persistence. | `tailwind.config.js`, `app/globals.css` |
| **Vercel** | Hosting & Edge CDN | Global edge deployment, automated CI/CD builds, and custom domain routing for `portfoliostore99.in`. | Vercel Project Settings |
| **Neon PostgreSQL** | Serverless Database | Persistent relational storage for order metadata, payment status, and customer email records. | `DATABASE_URL` |
| **Razorpay** | Payment Gateway | Merchant payment collection, Indian payment method processing (UPI, Cards, Netbanking), and webhook callbacks. | `RAZORPAY_KEY_ID`, `RAZORPAY_KEY_SECRET` |
| **Resend** | Transactional Email | Automated delivery of purchase confirmation receipts containing secure Google Drive download links. | `RESEND_API_KEY` |
| **Google Drive** | Digital Storage & CDN | Encrypted, reliable cloud storage hosting the official production source code `.zip` archives. | `lib/drive.js`, `DRIVE_URL_*` |
| **GitHub** | Source Control | Private production codebase repository (`https://github.com/ayushcmdx/PortfolioStore`). | Git Repository |

---

## 3. Strict Architectural Boundaries

The promotional landing page is a **presentation and marketing layer only**. It operates under strict architectural isolation from the transactional core of PortfolioStore 99:

### What the Promotional Page MUST Do:
- Display high-fidelity product cards, feature lists, pricing tables, and value propositions.
- Link out to live Vercel deployments (`https://store-*.vercel.app`) for interactive previews.
- Route purchase intent directly to the official storefront (`https://www.portfoliostore99.in/templates/[slug]` and `/checkout/[slug]`).
- Link to official policy documents (`/privacy-policy`, `/terms`, `/refund-policy`).

### What the Promotional Page MUST NOT Do:
- **Never** re-implement Razorpay checkout, payment modals, or order creation.
- **Never** connect directly to the Neon production database.
- **Never** attempt to handle webhooks or store customer payment records.
- **Never** store, manage, or expose Google Drive download URLs directly in client-side code.
- **Never** send transactional fulfillment emails.

All purchase transactions, receipt issuance, and digital fulfillment are strictly reserved for the authoritative production application at `https://www.portfoliostore99.in`.

---

## 4. Security & Credential Hygiene

In compliance with strict security protocols:
- **Zero Secrets in Documentation:** This repository and all promotional documentation must never contain real production credentials, database connection strings, API secrets, or private customer records.
- **Environment Variable Abstraction:** Only abstract variable names (e.g., `RAZORPAY_KEY_ID`, `DATABASE_URL`, `RESEND_API_KEY`) may be cited when describing system mechanics.
- **Customer Privacy Protection:** No real order IDs, customer names, or telephone numbers may be committed to documentation.
