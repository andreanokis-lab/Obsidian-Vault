---
tags: [module, orders, dispatch, product-truth]
module: orders-dispatch
audiences: [admin, sales, dispatcher, finance, claims]
generated: 2026-05-20
---

# Orders & Dispatch

The biggest surface in the product. The Order is the central business object.

## Where this lives in the UI
- **CRM** (`/crm`) — order detail accessed via account.
- **Trips** (`/trips`) — order shown as a card on the trip board.
- **Load Board** (`/loadboard`) — dispatcher's queue of orders by status.
- **Invoice** (`/invoice`) — orders viewed by their `OrderAccount` records.
- **Modals everywhere** (`src/app/modals/`) — order edit dialogs are summoned cross-module.

## Screens designers must support
- **Order detail** — header (public #, status, stage, tags), tabs for Vehicles / Stops / Accounting / History / Notes / Files.
- **Order create / edit modal** — multi-step: customer → vehicles → stops → accounting → notify rules.
- **Order list rows** — public #, status badge, stage chip, customer, route summary, $ amount, owner, age.
- **History / audit log** — chronological list of `eventType + action + creator + timestamp`.
- **Notify rules editor** — recipients + channels (email/SMS) per transition.
- **Vehicle inspection viewer** — BOL/POD photo grid + signature.

## Fields (designer-relevant)
See [[../Entities]] for full list. Header row must include:
`# Number · Status · Stage · Customer · Route (origin → destination) · Vehicle count · Total $ · Owner · Age`

## Statuses you must design for
- Order: `NEW`, `ON_HOLD`, `CONFIRMED`, `ON_THE_WAY`, `ONGOING`, `DELIVERED`, `CLAIMS_PENDING`, `COMPLETED`, `CANCELLED` ([[../Status Vocabulary]]).
- Per-vehicle: the 15-state `DISPATCH_VEHICLE_STATUS` may diverge from order status — design a per-vehicle status pill.
- Tags overlay status: `BILLED`, `PAID`, `ISSUES`, `INVOICED`.

## Actions per state (next-action affordance)
| State | Primary action | Secondary |
|---|---|---|
| `NEW` | Assign to Trip | Edit / Cancel / Hold |
| `ON_HOLD` | Resume | Cancel |
| `CONFIRMED` | (driver-driven) | Reassign / Cancel |
| `ON_THE_WAY` / `ONGOING` | Track | Message driver |
| `DELIVERED` | Send invoice | Open claim |
| `CLAIMS_PENDING` | Open claim | — |
| `COMPLETED` | Archive | — |
| `CANCELLED` | Restore | Archive |

## Permissions
- Visible to: `LEADS`, `LEADS_ADVANCED`, `DISPATCH`, `DISPATCH_ADVANCED`, `ACCOUNTING_*`.
- Edit gated by `DISPATCH_ADVANCED` for status overrides; `ACCOUNTING_*` for accounting block.

## Gotchas
- **Public # ≠ Mongo _id.** Show the CounterService number.
- **Soft delete.** "Delete" is "Archive" — always restorable.
- **Multi-tab realtime.** Order can mutate while user is editing — design conflict/refresh affordance.
- **Notify embedded.** Per-order notify rules override account defaults.
- **Central Dispatch integration.** Some orders mirror to/from the 3rd-party load board (`OrderCentralRoute.js`) — surface the linkage on the order.

## Audit when reviewing your design
Use [[../_audit/Audit Checklist Template]] with these extra checks:
- [ ] Status badge covers all 9 states (color + label)
- [ ] Per-vehicle status differs from order status case
- [ ] Tags (`BILLED`/`PAID`/`ISSUES`/`INVOICED`) shown as overlays, not as the primary status
- [ ] History panel is reachable on every order detail
- [ ] Permissions: dispatcher-only actions hidden from sales role mockup
- [ ] Central Dispatch source/sync indicator if applicable

Source: `_vector-db/modules/orders-dispatch.md`, `_vector-db/embeddings/be-model-order.md`.
