# EventFlow — Multi-tenant Event Booking MVP Concept

A self-contained static web prototype designed to demonstrate Phase 1 feasibility discussions for an agency-managed multi-tenant event booking platform. **Not production software.**

## Run locally
Open `index.html` in a modern browser. No npm or build step required.

## Deploy on Vercel
1. Upload the contents of this folder to the **root** of a GitHub repository.
2. At https://vercel.com/new import the repository.
3. Choose **Framework Preset: Other** (or no framework), **Root Directory: `./`**, **Build Command: blank/override off**, **Output Directory: blank** (root).
4. Deploy. The homepage is `index.html`.

## Demonstration flows
- **Tenant switching:** Choose NOVA, ATLAS, or BLOOM from the brand selector. Each brand shows separate example events and filters its client-facing activity.
- **Booking:** Discover → Event details → quantity & code → Reserve tickets (5-minute browser-only hold) → Checkout → Confirm booking → My bookings.
- **Promotions:** `EARLY10` gives 10% off. `GROUP15` gives 15% off for 4+ tickets. Calculated locally, with no server enforcement.
- **Agency dashboard:** Switch brands to see demo event inventory, confirmed bookings, booking value, and planned workflows.
- **Assistant:** Open the floating assistant. Rules respond to events, prices, promos, booking changes, or escalation questions. It is not an LLM and cannot perform real actions.
- **Architecture view:** Agency dashboard → View technical plan.

## Current limitations — do not represent as complete
- All data lives in the browser's localStorage. There is no backend, authentication, tenant isolation, or user permission model. Tenant switching is a *visual demonstration only*.
- Inventory holds, quotas, and booking counts apply only to this single browser. **No concurrency protection or overbooking guarantee.** Holds are five-minute local timers and are not durable.
- Checkout creates a demo record only. **No real payment, PCI/payment integration, refund or reconciliation.** Do not enter payment-card details.
- Promo codes are demo rules without a secure promotion engine or per-user eligibility enforcement.
- The chat assistant is local rule-based text, not OpenAI, WhatsApp, telephony, or integrated AI.
- No real CRM/POS, email/SMS, message queue, backup, CI/CD, or monitoring.
- Synthetic brands/events, using placeholder dates and capacity. No client PRS or business data was supplied.

## Proposed production architecture for paid discovery
React + TypeScript customer storefront/admin; NestJS/TypeScript service API; PostgreSQL tenant-scoped tables and database transactions for inventory/holds; Redis for optional caching and queue support, with expiration enforcement backed by the database; background workers; idempotent payment webhooks and reconciliation; integration adapters; LLM assistant with read-only retrieval / explicitly permissioned tool calls, hard validation by authoritative booking & promotions services; audit logs, RBAC, monitoring, backups, automated tests, CI/CD.

## Recommended discovery deliverables
1. Reviewed PRS, user journeys, prioritized MVP backlog, exclusions and acceptance criteria.
2. Architecture, data flows, tenant access controls and integration diagrams.
3. Booking/payment/hold expiry/communication workflows with retries, failure handling, human handoff and reconciliation.
4. Provider/API feasibility matrix, AI safe-action boundaries, WhatsApp/voice requirements and costs.
5. Phase estimates, staffing assumptions, operational costs, risks, decisions and go/no-go gates.

## Owner
Prototype generated for proposal demonstration. Fully editable static HTML/CSS/JavaScript.
