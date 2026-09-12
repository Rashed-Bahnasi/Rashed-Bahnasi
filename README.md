# Rashed Albahnasi

**Backend Developer — Laravel / SaaS Platforms**
Riyadh, Saudi Arabia

I build multi-tenant SaaS platforms in Laravel and take them all the way to production: architecture, REST APIs, payments and billing, deployment, and delivery to paying clients. Most of what I build is sold or runs commercially, so the code stays private — this page is what it does and how it's built.

---

## Live in production

| Product | What it is | Status |
|---|---|---|
| **[ManGym](https://managyms.com)** | Multi-tenant gym management SaaS — subscriptions, wallets, branch billing, coach revenue reporting | Live with a paying client running 2 branches and 1,000+ members |
| **Multi-Theme E-Commerce Platform** | Productized Arabic (RTL) store platform — Laravel 12 API, React storefront, optional Flutter app | Sold to clients as a ready store, delivered in 3 days |
| **BlueTouch** | On-demand multi-vendor laundry platform — order workflows, wallet, real-time messaging | Sold to a client, 2026 |
| **Wathiqati** | AI guide for recovering lost official documents, auto-generates application letters | Featured AI Showcase project, Kanz AI Training Hackathon 2026 |

---

## What I actually work on

**Multi-tenancy** — serving separate tenants and their branches from one codebase and database layer, with the isolation and billing boundaries that go with it.

**Payments** — Tap, Moyasar and Stripe behind one integration layer, with webhook verification so order settlement survives retries, duplicates and out-of-order callbacks.

**Subscription & wallet billing** — recurring renewals, per-branch billing, wallet recharge, PDF invoicing.

**API design for mobile** — REST APIs consumed by Flutter and React clients, with OTP-based passwordless auth and rate-limited endpoints.

**Schema design** — the e-commerce platform runs on a 46-table relational schema covering catalogue, orders, payments, wallets and content.

---

## Selected engineering work

### Cutting first-load JavaScript by 20% on a multi-theme storefront

The platform ships three storefront themes, but every visitor was downloading all three. The themes were statically imported at the top of the entry file, so they all landed in the main bundle regardless of which one was active. Worse, the Google Fonts link was injected by JavaScript *after* an API call returned the active theme — so font loading waited on the entire JS bundle to download and execute before it could even start.

Three changes:

1. **Dynamic `import()` per theme** — each theme became its own chunk, so the browser fetches exactly one.
2. **Server-side theme resolution** — the server already knows the active theme (`Setting::site_theme`). It now injects it into the initial HTML instead of making the client ask for it, removing a round-trip from the critical path entirely.
3. **Fonts in the document head** — the Google Fonts link renders server-side with `preconnect`, so fonts download in parallel with JavaScript rather than after it.

**Result:** main bundle down from 566KB to 453KB, plus a single ~35KB theme chunk instead of three. Live on three sites.

The part I care about most is #2 — the client was asking the server for something the server already knew. That's a round-trip that never needed to exist.

---

## Stack

**Backend** Laravel (incl. 12) · PHP · REST APIs · Laravel Backpack
**Data** MySQL · MongoDB · relational schema design · query optimization
**Payments** Tap · Moyasar · Stripe
**Clients** React · Flutter
**AI** Google Gemini API · OpenAI GPT-4 · n8n
**Testing & delivery** PHPUnit · Git · production deployment and maintenance

---

## A note on the private repositories

Nearly everything above is client work or a commercial product I sell, so the repositories aren't public — opening them would mean publishing other people's systems and giving away products that are still being sold. The live links are the demo; happy to walk through architecture, schema decisions or specific trade-offs in a conversation.

---

## Contact

📧 info@rashed-bahnasi.com · 🌐 [rashed-bahnasi.com](https://rashed-bahnasi.com)

Currently open to backend engineering roles in Riyadh.
