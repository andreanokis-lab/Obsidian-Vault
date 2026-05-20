---
tags: [entities, data-model, product-truth]
type: reference
source: D:/Backend/Models/
generated: 2026-05-20
---

# Entities

The nouns your UI must represent. Field lists are designer-relevant — full schema is in `D:/Backend/Models/...`.

> **Soft delete:** virtually every model uses the `mongoose-delete` plugin. The UI **never** shows a hard "Delete forever" path — only "Archive / Restore". When designing list views, assume a `deleted: false` filter is always applied.
> **Numeric IDs:** the public-facing order number, invoice number, etc. come from `Services/CounterService` — **not** from Mongo `_id`. Show the public number, never the Mongo id.

## Order (`dispatchOrders` collection)
The central business object. Represents a customer's request to move N vehicles between N stops.

Designer-relevant fields:
- **Public number** (sequential, from CounterService) — primary identifier shown everywhere.
- **Status** — `DISPATCH_ORDER_STATUS`.
- **Stage / tags** — `ORDER_TAGS` (`BILLED`, `PAID`, `ISSUES`, `INVOICED`).
- **Notify rules** — who gets emailed/texted on transitions.
- **Accounting** (embedded) — invoice/payable ref with `status` (`ORDER_ACCOUNT_STATUS`), `dueDate`, `paidAt`, paperwork completion, amount, document number.
- **Creator** — staff member who opened the order.
- **History** — full audit log (event, action, who, when). The order detail UI should expose this.
- **Trip ref** — links to a Trip when dispatched.

Children:
- **OrderVehicle** — per-vehicle line items (year/make/model/VIN, condition, weight, `VEHICLE_TYPE`, `DISPATCH_VEHICLE_STATUS`, inspection photos for BOL/POD).
- **OrderStop** — pickup/delivery stops (address, contact, `LOCATION_TYPES`, `ORDER_DATE_VALS` window precision, sequence).
- **OrderAccount** — order-level financial records (`INVOICE` / `BILL` / `PAYMENT` / `REFUND_RECEIPT`).

## Trip (`TripModel`)
A group of Orders assigned to one driver. Has its own lifecycle.

Designer-relevant fields:
- **Status** — `TRIP_STATUS` (numeric, but display the name).
- **Driver / dispatcher refs.**
- **Ownership** — `TRIP_OWNERSHIP_TYPE` (`Diesel Auto Express` (inhouse) vs `Sub Hauler`).
- **Route name** — `TRIP_ROUTE_NAME` (`A` / `B` / `SINGLE`) — single-truck route split.
- **Driver response** — `DRIVER_RESPONSE` (PENDING/ACCEPTED/REJECTED).
- **Driver payment status** — `DRIVER_PAYMENT_STATUS`.

Children:
- **TripPolyline** — cached Google Directions polyline (the line on the map).
- **TripDeposit** — advances paid against the trip.

## Account (CRM master record)
Any external party — customer, lead, broker, carrier, vendor — typed by `AccountType`.

Designer-relevant fields:
- **Type** — `CUSTOMER_TYPES` (`INDIVIDUAL`, `DEALER`, `BUSINESS`, `BROKER`, `CUSTOMER`, `SALVAGE DEALER`).
- **Status / sub-status** — `ACCOUNT_CONTACT_STATUSES` × `ACCOUNT_CONTACT_SUBSTATUSES`.
- **Stage** — `DISPATCH_LEAD_STAGE` (`New` / `Hot` / `Warm` / `Cold`).
- **Privilege** — `CUSTOMER_PRIVILEGE_TYPES` (`VIP`, `VVIP`, `NORMAL`) — badge in lists.
- **Payout history** — list of payouts with windows.
- **History audit log.**

Linked:
- **AccountContact** (people at the account, typed `ACCOUNT_CONTACT_INDIVIDUAL_TYPES` or `ACCOUNT_CONTACT_COMPANY_TYPES`).
- **AccountConnection** (relationships between accounts).
- **AccountCharts**, **AccountStatus**, **AccountStatusStage**, **AccountType**.

## Driver (within Account or separate)
Driver-specific:
- **DRIVER_TYPES** — `INHOUSE` / `LOCAL` / `FREELANCER` / `LONGHAULER` / `TOWINGDRIVER`.
- **HAULER_TYPES** — `LONGHAULER` / `LOCALHAULER` / `ALL`.
- Schedule, availability, day-off requests.

## Carrier / SubHauler
External carrier. Has its own auth (`Routes/Carrier/`). Receives assigned orders.

## Candidate (recruiter pipeline)
- **CONTACT_STAGES** — `New` → `Active` → `Awaiting` → `Review` → `Hired` / `Rejected`.
- **JOB_POSITIONS** — `LOCAL` / `LONGHAUL` / `BOTH`.

## Claim / ClaimVehicle
- **CLAIM_STATUS** — `NEW`, `ACTIVE`, `PENDING`, `CLOSED`.
- **CLAIM_SUB_STATUS** — `IN REVIEW`, `ACCEPTED`, `DENIED`.
- **CLAIM_STAGES** — `NEW`, `COLD`, `WARM`, `HOT`.
- **Source** — `CLAIM_SOURCES` (long list — see [[Status Vocabulary]]).
- **Payment method** — `CLAIM_PAYMENT_METHODS`.
- Linked: order, vehicles, contacts, payments.

## DispatcherSettlement
Driver/dispatcher payouts. Linked to orders for the period.

## Task / TaskBoard / TaskProject
Internal task tracker. Boards group projects, projects group tasks. Priority + assignee.

## Chat
- **ChatThread** — conversation between staff (or staff ↔ driver).
- **ChatMessages** — individual messages. Realtime via Socket.IO.

## Notifications / Push
- **Notification** — in-app notification record.
- **NotificationPush** — outbound push payload.
- **Device** + **DeviceToken** — registered devices (`DEVICE_TYPES`: IOS/ANDROID/WEB).

## GPS
- **GpsModel** — historical GPS pings.
- **LastGpsModel** — most recent position per driver/truck (used by map).
- **RouteModel** — historical route geometry.

## Expense / ChargeLog / PricingPolicy
- **Expense** — driver-submitted expense; `EXPENSE_CATEGORY` enum with caps.
- **ChargeLogs** — fee charges (CC processing, etc.).
- **PricingPolicy** — rules for quote pricing.

## Shop (maintenance)
Shop orders for the in-house fleet. Categorised by `SERVICE_TYPES`.

## Workflow*
Automation rules — triggers (`ORDER_CREATED`, `CHECKOUT_ORDER_CREATED`, etc.), conditions, actions, delays.

## FillerRequest, FollowUp, Feedback, ScheduleRequests, Expiration
Smaller domain models — see module notes.

## Admin
- **Permission**, **PermissionRole**, **AdminUser**, **Equipment**.

---

## Relationship map (high level)

```
Account ──< AccountContact
  │
  ├──< Order ──< OrderVehicle ──< Claim
  │      │       └──< InspectionPhoto (BOL/POD)
  │      ├──< OrderStop
  │      ├──< OrderAccount (Invoice/Bill/Payment/Refund)
  │      └──< History
  │
  └──< Trip ──< Driver (Account subtype)
         ├──< TripPolyline
         ├──< TripDeposit
         └──< DispatcherSettlement
```

## What this means for design
- Every list view of Orders/Trips/Accounts/Claims must show the **public number** + **status** + **stage** + **owner** at minimum.
- Detail views must surface **history** (audit log is universal).
- "Delete" is **archive** — design the archive/restore affordances.
- The same Account can appear as customer **and** broker **and** carrier — designs must handle multi-role accounts.

See [[Status Vocabulary]] · [[Workflows]] · module notes.
