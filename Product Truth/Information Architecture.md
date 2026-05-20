---
tags: [ia, routes, navigation, product-truth]
type: reference
source: D:/CRM_V2/src/app/core/app-routing.module.ts
generated: 2026-05-20
---

# Information Architecture

The frontend uses **hash routing** with a `userIndex` prefix that supports multiple authenticated tabs in the same browser:

```
#/<userIndex>/<area>/...
```

All authenticated areas are guarded by `AuthGuard + CoreValsGuard + UrlPermissionsGuard` (CRM uses only the first two). That means **every nav item is permission-aware** — designs must depict the case where the user only sees a subset.

## Top-level areas (lazy-loaded NgRx feature modules)

| Route | Module | Purpose | Designer module note |
|---|---|---|---|
| `/login` | UsersModule | Auth flows | [[Modules/Auth & Users]] |
| `/crm` | CRMModule | Accounts, contacts, leads, charts, integrations | [[Modules/CRM & Accounts]] |
| `/quotes` | QuotesModule | Quote builder (customer & internal) | [[Modules/Quotes & Load Board]] |
| `/loadboard` | QuotesModule (same code) | Dispatcher's queue of orders | [[Modules/Quotes & Load Board]] |
| `/trips` | TripsModule | Trip board + dispatch | [[Modules/Trips]] |
| `/calendar` | CalendarModule | Schedule view | [[Modules/Calendar & Schedule]] |
| `/tracking` | TrackingModule | Live GPS / map | [[Modules/Tracking & GPS]] |
| `/tasks` | TasksModule | Task tracker (boards/projects) | [[Modules/Tasks]] |
| `/claims` | ClaimsModule | Damage claims | [[Modules/Claims]] |
| `/reports` | ReportsModule | Reports & dashboards | [[Modules/Reports & Dashboards]] |
| `/settlements` | SettlementsModule | Driver/dispatcher payouts | [[Modules/Expense, Settlements & Invoice]] |
| `/dashboards` | (Dashboards) | Charts surfaces | [[Modules/Reports & Dashboards]] |
| `/expense` | ExpenseModule | Driver/staff expenses | [[Modules/Expense, Settlements & Invoice]] |
| `/invoice` | InvoiceModule | Invoices over `OrderAccount` | [[Modules/Expense, Settlements & Invoice]] |
| `/feedbacks` | FeedbackModule | Customer feedback inbox | [[Modules/Feedback]] |
| `/schedule` | ScheduleModule | Driver availability, day-off requests | [[Modules/Calendar & Schedule]] |
| `/shop` | ShopModule | Maintenance shop | [[Modules/Shop & Maintenance]] |
| `/workflow` | WorkflowModule | Automation rules | [[Modules/Workflow Automation]] |
| `/recruiter` | RecruiterModule | Driver hiring pipeline | [[Modules/Drivers & Candidates]] |
| `/admin` | AdminModule | Permissions, roles, users, equipment | [[Modules/Admin & Permissions]] |
| `/settings` | SettingsModule | App + user settings | [[Modules/Admin & Permissions]] |
| `/profile` | ProfileModule | User profile | [[Modules/Auth & Users]] |

## Driver iOS app (separate surface)
Calls `Routes/Mobile/` only. Areas (not URL-based — native nav):
- Trips list (assigned to me)
- Trip detail → order list
- Order detail → vehicle inspection forms (pickup BOL, delivery POD)
- Photo/signature capture
- Push notification inbox
- Expense entry (`EXPENSE_CATEGORY`)
- Schedule / day-off requests
- Settlement view (own)
- Profile / device

See [[Modules/Driver Mobile (iOS)]].

## Public / customer web
- Quote request, checkout, payment, inspection viewer, candidate apply, feedback (`Routes/Public/`).

## Carrier portal
- Carrier login + carrier order list (`Routes/Carrier/`).

## Navigation patterns to honor in design
- **Multi-tab user index** — same browser may have 2+ open sessions. Top bar must indicate which user/tab.
- **Permission-aware nav** — items conditionally render. Design empty/restricted states.
- **`X-Tab-Id` header** — every request carries it; multi-tab race conditions are real. Optimistic UI must reconcile.
- **Hash routes** — deep links use `#/...`. Share-link UX must include the hash.
