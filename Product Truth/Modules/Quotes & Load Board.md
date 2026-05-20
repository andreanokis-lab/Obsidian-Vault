---
tags: [module, quotes, loadboard, product-truth]
module: quotes
audiences: [sales, dispatcher, customer]
generated: 2026-05-20
---

# Quotes & Load Board

Quote authoring and the dispatcher's "available work" queue. **Same Angular module renders both** under `/quotes` and `/loadboard`.

## Screens designers must support
### Quote
- **Quote builder** — customer picker, vehicles (add multiple), stops (pickup/delivery, autocomplete via Google), service options, pricing breakdown, terms picker (`PAYMENT_TERMS`).
- **Quote preview / send** — customer-facing PDF/email.
- **Public quote widget** (embeddable on partner sites) — fed by `PluginQuoteRoute`.
- **Customer checkout flow** — quote → pay deposit → become Order. Lives at `Routes/Public/CheckoutRoute.js`.
- **Plugin quote (carrier-facing)** — for partners requesting capacity.

### Load Board (`/loadboard`)
- **Tabs by `DISPATCH_LOADBOARD_STATUS`**: `AVAILABLE TO BOOK` · `NOT ACCEPTED` · `DISPATCHED` · `PICKED-UP` · `DELIVERED` · `CANCELLED` · `ACCOUNTING` · `CLAIMS`.
- **Sub-filters** by `DISPATCH_LOADBOARD_DELIVERED_STATUS`, `DISPATCH_LOADBOARD_ORDER_STATUS`, `DISPATCH_LOADBOARD_ACCOUNTING_STATUS`, `DISPATCH_LOADBOARD_CLAIMS_STATUS`, `FOLLOW_UP_LOADBOARD_ORDER_STATUS` (F0–F4).
- **Row** = an order; columns commonly: #, route, vehicle count, customer, carrier/driver, pickup window, delivery window, price, last action, age.
- **Bulk select** — assign to trip, message, broadcast to Central Dispatch.

## Fields
- **Pricing breakdown** — uses `PricingPolicy` rules; show line items (base, surcharges, discounts).
- **Date precision** — `ORDER_DATE_VALS`: `Estimated` / `Exactly` / `No Earlier` / `No Later`. Designs must let the user pick this per stop.
- **Vehicle types** — `VEHICLE_TYPE` (12 types).
- **Stop location types** — `LOCATION_TYPES` (POV/TERMINAL/BUSINESS/WAREHOUSE/AUCTION/DEALER/RAILYARD).
- **Auction subtype** — `AUCTION_TYPES` when location = AUCTION.

## Permissions
- Internal quote: `LEADS`, `LEADS_ADVANCED`.
- Load board: `DISPATCH`, `DISPATCH_ADVANCED`.

## Gotchas
- **Central Dispatch sync.** Orders from CD are tagged — show provenance.
- **Plugin / embeddable** quote widget — designs must be self-contained (no app chrome).
- **Auction pickup quirks** — extra fields for auction lot #, gate fees (`GATE_FEE` in constants).
- **Date precision matters** — `Exactly` vs `Estimated` affects driver scheduling.

## Audit checks
- [ ] Load board has all 8 status tabs
- [ ] Sub-filter chips include all dropdown options (with `ALL`)
- [ ] Quote builder includes `ORDER_DATE_VALS` picker on each stop
- [ ] Pricing breakdown shows policy line items
- [ ] Payment terms picker covers all `PAYMENT_TERMS`
- [ ] Auction location enables auction-specific fields
- [ ] Public widget design has no app chrome
- [ ] Follow-up F0–F4 chips on load board rows
