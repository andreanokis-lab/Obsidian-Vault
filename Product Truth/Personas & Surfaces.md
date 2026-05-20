---
tags: [personas, surfaces, product-truth]
type: reference
generated: 2026-05-20
---

# Personas & Surfaces

Who uses what, derived from `USER_ROLES`, `ADMIN_ACCESS_LEVEL`, `ADMIN_PRIVILEDGES`, route folders, and feature modules.

## Roles (`USER_ROLES`)
`SUPER_ADMIN` · `ADMIN` · `CUSTOMER` · `DRIVER`

## Admin access levels (`ADMIN_ACCESS_LEVEL`)
`SUPER_ADMIN` · `SALES_ADMIN` · `FINANCE_ADMIN` · `DISPATCHER_ADMIN`

## Admin privileges (granular toggles, `ADMIN_PRIVILEDGES`)
`ALL`, `LEADS`, `LEADS_ADVANCED`, `DISPATCH`, `DISPATCH_ADVANCED`, `ACCOUNTING_ALL`, `ACCOUNTING_PAYMENTS`, `ACCOUNTING_INVOICES`, `ACCOUNTING_CLAIMS`, `DASHBOARD_DISPATCHER`, `DASHBOARD_GENERIC`.

> Frontend uses `UrlPermissionsGuard` on every authenticated route — features can be hidden per privilege. Designs of nav/sidebar must show **conditional** items, not assume all are visible.

## Personas (composite)

### Sales / Lead Specialist
- Lives in **CRM** (`/crm`) and **Quotes** (`/quotes`).
- Works the funnel: `LEAD → PROSPECT → ACTIVE` (`ACCOUNT_CONTACT_STATUSES`) and `New → Hot → Warm → Cold` (`DISPATCH_LEAD_STAGE`).
- Privileges: `LEADS`, `LEADS_ADVANCED`.
- Pain points (informed by `ORDER_CALL_OUTCOME_TAGS`): triage, callbacks, dedupes.

### Dispatcher
- Lives in **Load Board** (`/loadboard`), **Trips** (`/trips`), **Tracking** (`/tracking`), **Calendar** (`/calendar`).
- Assigns Orders to Drivers via Trips. Watches live GPS.
- Privileges: `DISPATCH`, `DISPATCH_ADVANCED`, `DASHBOARD_DISPATCHER`.
- Core verbs: assign, reassign, hold, cancel, broadcast to load board.

### Finance / Accounting
- Lives in **Invoice** (`/invoice`), **Settlements** (`/settlements`), **Expense** (`/expense`), **Reports** (`/reports`).
- Statuses they care about: `ORDER_ACCOUNT_STATUS`, `PAYMENT_STATUS`, `DRIVER_PAYMENT_STATUS`, `DISPATCH_LOADBOARD_ACCOUNTING_STATUS`.
- Privileges: `ACCOUNTING_ALL`, `ACCOUNTING_PAYMENTS`, `ACCOUNTING_INVOICES`.

### Claims Specialist
- Lives in **Claims** (`/claims`).
- Statuses: `CLAIM_STATUS`, `CLAIM_SUB_STATUS`, `CLAIM_STAGES`. Sources: `CLAIM_SOURCES`.
- Privileges: `ACCOUNTING_CLAIMS`.

### Recruiter
- Lives in **Recruiter** (`/recruiter`).
- Pipeline: `New → Active → Awaiting → Review → Hired / Rejected`.

### Shop Manager / Mechanic
- Lives in **Shop** (`/shop`) — maintenance orders for the in-house fleet.
- Service categories: `SERVICE_TYPES` (engine, transmission, etc.).

### Admin / Super-Admin
- Lives in **Admin** (`/admin`), **Settings** (`/settings`).
- Manages permissions, roles, users, equipment.

### Driver (iOS only)
- Mobile app exclusively. Calls `Routes/Mobile/`.
- Sees: assigned trips, vehicle inspection forms, expense entry, push notifications.
- Statuses driven by `BOOKING_STATUS`, `DRIVER_RESPONSE`, `DRIVER_PAYMENT_STATUS`.

### Customer
- Public/customer web — gets quote, accepts order, tracks, pays.
- Sees a narrowed status surface: `CUSTOMER_PORTAL_STATUS` (`QUOTES`, `ORDERS`, `PICKED-UP`, `DELIVERED`, `CANCELLED`).

### Carrier / Sub-hauler
- Separate auth (`Routes/Carrier/`). Receives orders assigned by HaulEx.
- Sees order assignment + status updates only.

## Surface × Persona matrix

| Area | Sales | Dispatcher | Finance | Claims | Driver | Customer | Carrier | Admin |
|---|---|---|---|---|---|---|---|---|
| CRM | ✅ | view | view | view | — | — | — | ✅ |
| Quotes | ✅ | view | — | — | — | request | — | ✅ |
| Load Board | — | ✅ | view | view | — | — | — | ✅ |
| Trips | view | ✅ | view | — | mobile | — | view | ✅ |
| Tracking | — | ✅ | — | view | mobile push | own order | — | ✅ |
| Calendar | — | ✅ | — | — | own | — | — | ✅ |
| Tasks | ✅ | ✅ | ✅ | ✅ | — | — | — | ✅ |
| Claims | view | view | ✅ | ✅ | — | — | — | ✅ |
| Invoice | — | view | ✅ | view | — | view | — | ✅ |
| Settlements | — | view | ✅ | — | view (own) | — | view (own) | ✅ |
| Expense | — | — | view | — | ✅ entry | — | — | ✅ |
| Reports | — | view | ✅ | view | — | — | — | ✅ |
| Feedback | — | — | — | view | — | submit | — | ✅ |
| Schedule | — | ✅ | — | — | request day-off | — | — | ✅ |
| Shop | — | view | — | — | view own | — | — | ✅ |
| Workflow | — | — | — | — | — | — | — | ✅ |
| Recruiter | — | — | — | — | apply | — | — | ✅ |
| Admin | — | — | — | — | — | — | — | ✅ |

See [[Information Architecture]] for the underlying route map.
