---
tags: [workflows, state-machines, product-truth]
type: reference
generated: 2026-05-20
---

# Workflows

The cross-module flows that define the product. Use these to verify your screens stitch together correctly.

## 1. Lead → Quote → Order
1. Sales captures lead → `Account` created with `ACCOUNT_CONTACT_STATUSES.LEAD`, stage `DISPATCH_LEAD_STAGE.New`.
2. Call outcomes logged via `ORDER_CALL_OUTCOME_TAGS`.
3. Quote sent → `DISPATCH_LEAD_STATUS` advances (`NEW → ON-HOLD → ORDER`).
4. Quote accepted → **Order created** via `OrderRoute.create`, `CounterService` issues public order #, invoice draft generated, Socket.IO broadcast to all open CRM tabs.
5. `Account` stage often moves `New → Hot → Warm` as engagement progresses.

**Designer surfaces involved:** CRM list, Account detail, Quote builder, Quote accept flow (customer web), Order detail (post-creation).

## 2. Order → Trip → Driver Assignment
1. Order sits with status `NEW` on the **Load Board** (`DISPATCH_LOADBOARD_STATUS.AVAILABLE TO BOOK`).
2. Dispatcher creates a **Trip** (`TRIP_STATUS.CREATED`) and adds orders.
3. Dispatcher assigns a driver — `TRIP_STATUS.REQUESTED`, `DRIVER_RESPONSE.PENDING`.
4. **Push** sent to driver (FCM/APN) via `NotificationPush`.
5. Driver opens iOS app → accepts (`DRIVER_RESPONSE.ACCEPTED`, `TRIP_STATUS.PENDING → ONGOING`) or rejects (`TRIP_STATUS.REJECTED` → back to Load Board).
6. Order status flips `NEW → CONFIRMED → ON_THE_WAY`.

**Designer surfaces involved:** Load Board, Trip builder modal, Driver iOS trip list, push notification card, Calendar.

## 3. In-transit (GPS + Realtime)
1. Driver iOS app pings GPS → `GpsModel` (history) + `LastGpsModel` (latest).
2. Socket.IO broadcasts position to subscribed dispatcher views.
3. `Tracking` map shows truck position + `TripPolyline` route.
4. ETA computed via Google Distance Matrix.
5. Per-vehicle: `DISPATCH_VEHICLE_STATUS` may diverge (`AT_THE_YARD_PICKUP` → `ON_THE_WAY` → `AT_THE_YARD_DROPOFF`).

**Designer surfaces involved:** Tracking map, Trip detail (CRM), Trip detail (Driver), Order detail.

## 4. Pickup / Delivery (Inspection)
1. Driver arrives at pickup → opens **OrderVehicleInspaction** form.
2. Captures: photos (sides, damage), condition notes, customer signature (BOL).
3. Status → `DISPATCH_VEHICLE_STATUS.ON_THE_WAY`, `DISPATCH_ORDER_STATUS.ON_THE_WAY`.
4. At delivery → POD photos + signature.
5. Vehicle status → `DELIVERED`. When all vehicles delivered → Order `DELIVERED`.
6. `BOOKING_STATUS` (driver-facing): `CONFIRMED → ON_THE_WAY → PICKED → ONGOING → DELIVERED → COMPLETED`.

**Designer surfaces involved:** Driver iOS — inspection screen, photo capture, signature capture, vehicle list, delivery confirmation.

## 5. Delivered → Invoiced → Paid
1. `OrderAccount` invoice exists with `ORDER_ACCOUNT_STATUS.DRAFT` or `CREATED`.
2. Finance reviews → `SENT` (emailed via SendGrid).
3. Customer pays via Stripe / Authorize.Net / Bill / COD/COP/Money Order.
4. `PAYMENT_STATUS.WAITING → COMPLETED`.
5. `ORDER_ACCOUNT_STATUS` → `PROCESSED` / `PAID` (or `PARTIAL PAID`).
6. Order tag `INVOICED` then `PAID` (`ORDER_TAGS`).
7. QuickBooks sync via Intuit webhooks.

**Designer surfaces involved:** Invoice list, Invoice detail, Payment modal, Customer-facing pay link (public), Receipt email.

## 6. Settlement (driver payout)
1. Period closes → `DispatcherSettlement` computed for each driver/dispatcher across their delivered trips.
2. Adjustments applied (deductions, claims, expenses).
3. `DRIVER_PAYMENT_STATUS.WAITING → DECIDED → PAID` (or `HOLD` / `DECLINED`).
4. Payment sent via selected method (`PAYMENT_METHODS`: Zelle, CashApp, ACH, Mailed Check, etc.).
5. Driver sees own settlement in iOS app.

**Designer surfaces involved:** Settlements list, Settlement detail (CRM), Settlement view (Driver iOS).

## 7. Claim (when something goes wrong)
1. Triggered manually (any role) or auto on `CLAIMS_PENDING` order status.
2. `Claim` created with `CLAIM_STATUS.NEW`, `CLAIM_STAGES.NEW`.
3. Source picked from `CLAIM_SOURCES` (long list).
4. Stage progresses `NEW → COLD → WARM → HOT` as severity/urgency increases.
5. Sub-status `IN REVIEW → ACCEPTED / DENIED`.
6. Payment via `CLAIM_PAYMENT_METHODS` (often `Transport deduction` = deduct from driver settlement).
7. Closes → `CLAIM_STATUS.CLOSED`.

**Designer surfaces involved:** Claim list (filters by `DISPATCH_LOADBOARD_CLAIMS_STATUS`), Claim detail, Claim payment modal, Driver-facing notification of deduction.

## 8. Expense (driver-side)
1. Driver submits expense from iOS — category from `EXPENSE_CATEGORY` (with caps).
2. Photos of receipts attached.
3. Finance reviews in `/expense`.
4. Approved expenses roll into settlement.

## 9. Notifications & Push
- Triggers: status transitions on Order/Trip/Vehicle/Claim, new chat message, schedule changes.
- Channels: in-app `Notification` list, push (FCM/APN), email (SendGrid), SMS (Twilio).
- `Notify` rules embedded on each Order control who is contacted at each event.

## 10. Multi-tab session
- Same staff member may have 2+ CRM tabs open with `userIndex` 0, 1, …
- `X-Tab-Id` header on every request.
- Socket.IO room per user — events fan out to all their tabs.
- Optimistic UI must reconcile when a sibling tab makes a change.

---

**Use these when designing:**
- Verify your screen represents the **correct state(s)** in the flow above.
- Verify the **next-action affordance** matches what the state allows.
- Verify **who triggered the transition** is shown (history).
- Verify **side-effects are visible** — e.g. when a driver accepts a trip in iOS, the dispatcher's Load Board updates within seconds.
