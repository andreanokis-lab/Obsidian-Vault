---
tags: [module, mobile, driver, ios, product-truth]
module: mobile-api
audiences: [driver]
generated: 2026-05-20
figma:
  uikit: 3qOFF7kHsaZPfdftDb1CVz
  driver-app: yhxCSzJrafZbqXGZOCBCKE
---

# Driver Mobile (iOS)

The native iOS app drivers use in the field. Calls `Routes/Mobile/` exclusively. **Separate codebase** — design lives in `Driver App/` folder of this vault and the two Figma files above.

## Backend surface (what the app can do)
- `Routes/Mobile/Order/PaymentRoute.js` — collect payment at delivery (cash/card/MO).
- `Routes/Mobile/Adjustment/AdjustmentRoute.js` — request order adjustments.
- `Routes/Mobile/NotificationPush/NotificationPushRoute.js` — push registration.
- `Routes/Mobile/DeviceToken/DeviceTokenRoute.js` — device token lifecycle.
- Plus mobile-flagged endpoints across `Routes/Order/`, `Routes/Gps/`, `Routes/Expense/`, `Routes/ScheduleRequests/`.

Auth: same bearer token as web, role = `DRIVER`. Mobile-only middleware checks `frommobile` header.

## Screens designers must support (Driver App)
Per native navigation (no URL routes):

| Screen | Purpose | Key statuses / fields |
|---|---|---|
| **Onboarding / Login** | OAuth/bearer auth | — |
| **Trips list** | Assigned trips | `TRIP_STATUS` + `DRIVER_RESPONSE` |
| **Trip detail** | Order list in sequence, polyline preview | `TRIP_STATUS`, deposits, route name (A/B/SINGLE) |
| **Order detail** | Vehicles, stops, contacts | `DISPATCH_ORDER_STATUS` |
| **Pre-pickup inspection (BOL)** | Photos (4-side + damage), condition notes, signature | Per vehicle → `DISPATCH_VEHICLE_STATUS.ON_THE_WAY` |
| **At-pickup** | Confirm vehicle loaded | — |
| **Delivery / POD** | Photos, signature, payment collection | → `DELIVERED` |
| **Payment collection** | `PAYMENT_OPTIONS_CASH` (Bill/MO/Check/Cash) + card | `PAYMENT_STATUS` |
| **Expense entry** | Category + amount + receipt photo | `EXPENSE_CATEGORY` (with caps) |
| **Schedule / Day-off request** | Request via `ScheduleRequests` | `SCHEDULE_STATUS` |
| **Settlement** | View own payout history | `DRIVER_PAYMENT_STATUS` |
| **Notifications inbox** | In-app + push | — |
| **Chat** | Thread with dispatcher | Socket.IO |
| **Profile / Device** | Truck/trailer assignment | `DEVICE_TYPES.IOS` |
| **Adjustment request** | Ask dispatch for fee/route change | — |

## Statuses driver sees
- **Booking** (driver-facing flow): `BOOKING_STATUS` 1–12.
- **Trip**: `TRIP_STATUS`.
- **Vehicle**: `DISPATCH_VEHICLE_STATUS` (drives the inspection screen logic).
- **Payment**: `PAYMENT_STATUS`, `DRIVER_PAYMENT_STATUS`.
- **Schedule**: `SCHEDULE_STATUS`.

## Gotchas
- **iPhone-first per project CLAUDE.md.** Design for iOS HIG ([[../../hig_guidelines]]).
- **HaulEx UIKit** (`3qOFF7kHsaZPfdftDb1CVz`) is the component library — Light + Dark mode for colors, iOS-only typography.
- **Offline tolerance** — drivers lose signal. Inspection photos must queue + retry; expense entry must persist locally.
- **GPS background** — the app pings GPS on a cadence; show clear permission/battery affordances.
- **Push payload variants** — assignment, reassign, cancel, chat, schedule decision. Each needs an inbox card design.
- **Signature capture** — both BOL and POD need finger-drawn signatures stored as `FILE_TYPES.SIGNATURE`.
- **Driver types** — `DRIVER_TYPES.INHOUSE` vs `FREELANCER` may see slightly different settlement/expense UI.

## Permissions
Driver role only. No staff routes available. Cannot see other drivers' trips.

## Audit checks
- [ ] Bottom tab IA reflects the screen list above
- [ ] Inspection screen handles 4-side + damage photo set per vehicle
- [ ] Signature capture present on BOL **and** POD
- [ ] Payment collection covers `PAYMENT_OPTIONS_CASH` + card
- [ ] Expense entry shows category caps in helper text
- [ ] Offline queue indicator for photos/expenses
- [ ] Push notification inbox card design covers each trigger
- [ ] Settlement view shows `DRIVER_PAYMENT_STATUS` and method
- [ ] Day-off request flow exists and matches `SCHEDULE_STATUS` transitions
- [ ] HIG compliance ([[../../hig_guidelines]]): touch targets, dynamic type, safe areas

Source: `_vector-db/modules/mobile-api.md`, project CLAUDE.md.
