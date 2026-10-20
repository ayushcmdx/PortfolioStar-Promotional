# PortfolioStore 99 — Customer Journey & Order Lifecycle

This document defines the complete end-to-end user experience, checkout workflow, cryptographic payment verification, and digital fulfillment process for **PortfolioStore 99** ([portfoliostore99.in](https://www.portfoliostore99.in)).

---

## 1. Journey Architecture Diagram

```
┌─────────────────────────────────┐
│     Discovery & Promotion       │  Visitor arrives via Promotional Page,
│  (portfoliostore99.in / Promo)  │  GitHub showcase, or organic search.
└────────────────┬────────────────┘
                 │
                 ▼
┌─────────────────────────────────┐
│       Interactive Preview       │  Visitor tests full live deployment on
│  (https://store-*.vercel.app)   │  Vercel (animations, themes, mobile).
└────────────────┬────────────────┘
                 │
                 ▼
┌─────────────────────────────────┐
│      Product Selection          │  Clicks "Buy Template" or navigates to
│ (portfoliostore99.in/templates) │  official storefront detail page.
└────────────────┬────────────────┘
                 │
                 ▼
┌─────────────────────────────────┐
│       Standard Checkout         │  Enters Name and Email on
│ (/checkout/[slug])              │  https://www.portfoliostore99.in/checkout/[slug]
└────────────────┬────────────────┘
                 │
                 ▼
┌─────────────────────────────────┐
│   Razorpay Payment Gateway      │  UPI QR / Google Pay / PhonePe /
│   (Secure Native Modal)         │  Cards / Netbanking / Wallets.
└────────────────┬────────────────┘
                 │
                 ▼
┌─────────────────────────────────┐
│ Cryptographic Verification      │  Server verifies Razorpay signature via
│ (/api/razorpay/verify-payment)  │  HMAC SHA256 & records order in Neon DB.
└────────────────┬────────────────┘
                 │
                 ▼
┌─────────────────────────────────┐
│ Instant Digital Fulfillment     │  1. Customer gets instant Google Drive link
│ (/thank-you?order_id=...)       │     on the Thank-You confirmation screen.
│ & Automated Email Delivery      │  2. Automated receipt sent via Resend.
└─────────────────────────────────┘
```

---

## 2. Step-by-Step Experience Breakdown

### Phase 1: Discovery & Evaluation
1. **First Touchpoint:** The visitor lands on the promotional landing page or the main storefront homepage (`https://www.portfoliostore99.in`).
2. **Catalog Browsing:** The visitor filters templates by pricing tier:
   - **Newbie (₹99):** Clean, fast single-page starter portfolios.
   - **General (₹199):** Interactive 3D Spline, Three.js room, or editorial codex themes.
   - **Premium (₹399):** Next.js 15, macOS desktop, cyber CRT terminal, and 3D island universes.
3. **Live Deployed Preview:**
   - Crucially, the customer does not rely on static mockups.
   - Every product card features a direct **"Live Preview"** button that opens a production deployment on Vercel (e.g., `https://store-star.vercel.app`, `https://store-desktop.vercel.app`, `https://store-3dhome.vercel.app`).
   - The customer interacts with 3D scenes, toggles dark/light themes, tests sound effects, and checks mobile responsiveness on their own device.

---

### Phase 2: Checkout & Purchase
1. **Selecting the Template:** On the product detail page (`/templates/[slug]`), the customer reviews included deliverables, supported tech stacks, and licensing terms, then clicks **"Buy Template — ₹XXX"**.
2. **Checkout Page (`/checkout/[slug]`):**
   - The customer enters two required contact fields:
     - **Full Name**
     - **Email Address** (where order confirmation and backup access links are sent)
   - Order summary is clearly displayed with exact INR pricing (e.g., ₹99, ₹199, or ₹399 flat).
   - Zero hidden processing charges, upsells, or recurring fees.
3. **Initiating Payment:**
   - The frontend calls the backend API: `POST /api/razorpay/create-order`.
   - The server validates the product slug, generates an official Razorpay order with the verified catalog price, and returns the `order_id`.
   - The official Razorpay checkout modal opens securely over the page.

---

### Phase 3: Payment Processing & Security
1. **Supported Payment Options (India & Domestic):**
   - **UPI:** Instant scan-and-pay QR code, Google Pay, PhonePe, Paytm, CRED.
   - **Cards:** Visa, MasterCard, RuPay, Maestro credit and debit cards.
   - **Netbanking:** All major Indian banks.
   - **Wallets:** Paytm, Mobikwik, etc.
2. **Zero Credential Storage:** PortfolioStore 99 never touches, processes, or stores payment credentials, card numbers, or UPI PINs. All financial transactions are handled end-to-end by Razorpay under industry-standard PCI-DSS compliance.

---

### Phase 4: Server-Side Cryptographic Verification
Once the customer authorizes payment in Razorpay:
1. Razorpay returns three security parameters to the client:
   - `razorpay_order_id`
   - `razorpay_payment_id`
   - `razorpay_signature`
2. The frontend submits these credentials to `POST /api/razorpay/verify-payment`.
3. The server validates the cryptographic authenticity using HMAC SHA256:
   $$\text{generated\_signature} = \text{HMAC-SHA256}(\text{order\_id} + "|" + \text{payment\_id}, \text{RAZORPAY\_KEY\_SECRET})$$
4. If the signatures match exactly:
   - The order is marked as `PAID`.
   - The order record is persisted in **Neon Serverless PostgreSQL** (`orders` table).
   - The matching secure Google Drive download URL is retrieved from the verified registry (`lib/drive.js`).
   - An automated transactional email is dispatched via **Resend** with the order receipt and download link.

---

### Phase 5: Instant Fulfillment & Post-Purchase Access
1. **Confirmation Screen (`/thank-you?order_id=...`):**
   - The user is immediately redirected to a clear order confirmation page.
   - An **"Access Your Files (Google Drive)"** button is rendered prominently.
   - The customer can immediately download the complete source code `.zip` archive containing all React/Next.js files, assets, models, and configuration.
2. **Email Receipt (Resend):**
   - A backup email is delivered to the customer's inbox containing:
     - Order ID and transaction timestamp.
     - Purchased template name and tier.
     - Persistent Google Drive access link for future re-downloads.
     - Setup and hosting instructions for Vercel/Netlify.
3. **Customer Support Availability:**
   - If the customer needs assistance extracting files, updating their resume data, or linking custom domains on Vercel, direct support is available via:
     - **WhatsApp:** `@ayushcmd` (`https://wa.me/917587246554`)
     - **Email:** `portfoliostore99@gmail.com`

---

## 3. Strict Architecture Boundary

The promotional landing page is a **presentation layer only**. It must link to the existing storefront for all purchase workflows:

- **Do NOT** duplicate or rebuild Razorpay endpoints in the promotional project.
- **Do NOT** connect directly to the Neon production database from external sites.
- **Do NOT** attempt to fulfill orders or handle payments independently.
- **Always route** the customer to `https://www.portfoliostore99.in/checkout/[slug]` for transactions.
