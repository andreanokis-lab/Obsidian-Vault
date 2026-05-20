---
tags: [reference, vocabulary, enums, status]
type: reference
source: D:/Backend/config/constants.js
generated: 2026-05-20
---

# Status Vocabulary

The exact string enums used by the API and UI. **If your design shows a status badge, filter chip, dropdown option, or empty-state label, it must come from this list** (or be a clearly proposed addition).

Conventions to apply in design:
- Storage on backend is **UPPER_SNAKE_CASE** or short codes. Display label is usually Title Case (engineers handle the transform — but copy must match the intent).
- Many filter dropdowns start with an `'ALL'` option (`'' → ALL`). Always include this in list views.
- Numeric statuses (e.g. `TRIP_STATUS`, `BOOKING_STATUS`) are stored as integers — designers should ignore the number, design around the name.

## Order — `DISPATCH_ORDER_STATUS`
The lifecycle of an Order shown across CRM, Load Board, Trip view, and Driver app.
`NEW` · `ON_HOLD` · `CONFIRMED` · `ON_THE_WAY` · `ONGOING` · `DELIVERED` · `CLAIMS_PENDING` · `COMPLETED` · `CANCELLED`

## Vehicle (per line item) — `DISPATCH_VEHICLE_STATUS`
A single vehicle on an order may diverge from the order status (e.g. multi-vehicle order where one vehicle is delivered, one in transit).
`DRAFT` · `NEW` · `PROSPECTING` · `CONFIRMED` · `LOCAL_HAULER_PICKUP` · `AT_THE_YARD_PICKUP` · `ON_THE_WAY` · `ONGOING` · `AT_THE_YARD_DROPOFF` · `LOCAL_HAULER_DROPOFF` · `DELIVERED` · `INVOICED` · `CLAIMS_PENDING` · `COMPLETED` · `CANCELLED`

## Trip — `TRIP_STATUS` (numeric)
`CREATED (0)` · `PENDING (1)` · `ONGOING (2)` · `ON_THE_WAY (3)` · `CONFIRMED (4)` · `COMPLETED (5)` · `EXPIRED (6)` · `REJECTED (7)` · `CANCELLED (8)` · `CANCELLED_BY_DRIVER (9)` · `CANCELLED_BY_ADMIN (10)` · `REQUESTED (11)`

## Booking — `BOOKING_STATUS` (numeric, driver-facing)
`PENDING (1)` · `CONFIRMED (2)` · `ON_THE_WAY (3)` · `PICKED (4)` · `ONGOING (5)` · `DELIVERED (6)` · `COMPLETED (7)` · `EXPIRED (8)` · `REJECTED (9)` · `CANCELLED (10)` · `CANCELLED_BY_DRIVER (11)` · `CANCELLED_BY_ADMIN (12)`

## Load Board filters
- `DISPATCH_LOADBOARD_STATUS` — top-level tabs: `AVAILABLE TO BOOK` · `NOT ACCEPTED` · `DISPATCHED` · `PICKED-UP` · `DELIVERED` · `CANCELLED` · `ACCOUNTING` · `CLAIMS`
- `DISPATCH_LOADBOARD_DELIVERED_STATUS`: `ALL` · `NOT-CLOSED` · `CLOSED` · `NOT-CONFIRMED` · `CONFIRMED`
- `DISPATCH_LOADBOARD_ORDER_STATUS`: `ALL` · `NOT-CONFIRMED` · `CONFIRMED`
- `DISPATCH_LOADBOARD_ACCOUNTING_STATUS`: `READY` · `BILLED` · `PAID`
- `DISPATCH_LOADBOARD_CLAIMS_STATUS`: `OPEN` · `ACTIVE` · `CLOSED`
- `DISPATCH_LOADBOARD_CLAIMS_STAGE`: `New` · `Cold` · `Warm` · `Hot`
- `FOLLOW_UP_LOADBOARD_ORDER_STATUS`: `ALL` · `F0` · `F1` · `F2` · `F3` · `More (F4)`

## Lead / CRM funnel
- `DISPATCH_LEAD_STATUS`: `ALL` · `NEW` · `ON-HOLD` · `ORDER` · `PICKED-UP` · `DELIVERED` · `CANCELLED`
- `DISPATCH_LEAD_STAGE`: `New` · `Hot` · `Warm` · `Cold`
- `ACCOUNT_CONTACT_STATUSES`: `LEAD` · `PROSPECT` · `DNC` · `ACTIVE`
- `ACCOUNT_CONTACT_SUBSTATUSES`: `DO NOT USE` · `SUSPENDED` · `RESTRICTED`
- `CUSTOMER_PRIVILEGE_TYPES`: `VIP` · `VVIP` · `NORMAL`

## Customer / contact types
- `CUSTOMER_TYPES`: `INDIVIDUAL` · `DEALER` · `BUSINESS` · `BROKER` · `CUSTOMER` · `SALVAGE DEALER`
- `ACCOUNT_CONTACT_INDIVIDUAL_TYPES`: `BROKER` · `DRIVER` · `DISPATCH` · `EVERYTHING` · `CUSTOMER` · `ACCOUNTING` · `CLAIMS` · `MECHANIC` · `POV`
- `ACCOUNT_CONTACT_COMPANY_TYPES` (full list): `POV`, `AUCTION`, `COMPANY`, `OEM`, `CARRIER`, `CAR-PULLER`, `BROKER`, `RENTAL`, `DEALER`, `SALVAGE`, `IMPORT/EXPORT`, `GOV. MILITARY`, `CORP BROKER`, `AUTO SHOP`, `TRUCK SHOP`, `TOWING`, `PORT`, `RAIL YARD`, `POTENTIAL DRIVER`, `SPECIAL MOVE`, `CONSULTANT`, `RELO AGENT`, `INSURANCE`, `STOP`, `VENDOR`, `ADVERTISERS`

## Order tags / call outcomes
- `ORDER_TAGS`: `BILLED` · `PAID` · `ISSUES` · `INVOICED`
- `ORDER_CALL_OUTCOME_TAGS`: `Future Shipment` · `Will Call Back` · `Could Not Reach` · `Hired Other` · `Bad Phone` · `Shopping Around` · `Quote` · `Left Message` · `No Longer Shipping` · `Duplicate` · `Unsubscribed`

## Invoicing & payments
- `ORDER_ACCOUNT_TYPE`: `Invoice` · `Bill` · `Payment` · `Refund`
- `ORDER_ACCOUNT_STATUS`: `DRAFT` · `CREATED` · `PAID` · `SENT` · `PROCESSED` · `PARTIAL PAID` · `PENDING` · `UNPAID`
- `PAYMENT_STATUS`: `WAITING` · `COMPLETED` · `DECLINED` · `HOLD` · `REFUND`
- `DRIVER_PAYMENT_STATUS`: `WAITING` · `DECIDED` · `PAID` · `DECLINED` · `HOLD`
- `PAYMENT_OPTIONS`: `COP` · `COD` · `BILL` · `MO (Money Order)` · `ONLINE`
- `PAYMENT_OPTIONS_CASH`: `BILL` · `MO` · `CHECK` · `CASH`
- `PAYMENT_OPTION` (broker side): `UPFRONT` · `INBOUND` · `BROKERAGE` · `OTHER`
- `PAYMENT_TERMS`: `ACH` · `Bank Deposit` · `CashApp` · `CKOD` · `COD` · `COP` · `Due on receipt` · `Comcheck` · `Credit Card` · `2/5/7/10/15/20/30/45/60 days` · `Other` · `USHIP` · `QuickPay` · `Zelle`
- `PAYMENT_METHODS`: `Zelle` · `CashApp` · `ACH Transfer` · `Mailed Check` · `E-Check` · `Venmo`
- `PAYMENT_FEE_VALS`: `Fee 1.5% / 2% / 2.5% / 3% / 5%`

## Claims
- `CLAIM_STATUS`: `NEW` · `ACTIVE` · `PENDING` · `CLOSED`
- `CLAIM_SUB_STATUS`: `IN REVIEW` · `ACCEPTED` · `DENIED`
- `CLAIM_STAGES`: `NEW` · `COLD` · `WARM` · `HOT`
- `CLAIM_PAYMENT_METHODS`: `Transport deduction` · `Insurance Pay` · `Check sent out` · `CashApp` · `ACH` · `PayPal`
- `CLAIM_SOURCES` (top): `Bond Claim`, `Vehicle Damage`, `Late Delivery`, `Non Payment`, `Communication`, `Negative Reviews`, `Rental Reimburse`, `Property Damage`, `Parking`, `Accident`, `Breakdowns`, `Weather`, `Bounced Check`, `Car Driven`, `Late Pickup`, `Dispatch Error`, `Driver Error`, `Partial Payment`, `Fake Claim`, `Truck Damage`, `Lost Keys`, `Lost Title`, `Lawsuit`, `Windshield Damage`, `Insurance Reported`, `Late Night Drop`, `Dead Battery`, `Rock Chips`, `Gas Cap`, `DOT / Ticket`, `Driver Claim`, `Tree Scratches`, `Interior`, `Shipping Discount`, `Other`

## Roles & access
- `USER_ROLES`: `SUPER_ADMIN` · `ADMIN` · `CUSTOMER` · `DRIVER`
- `ADMIN_ACCESS_LEVEL`: `SUPER_ADMIN` · `SALES_ADMIN` · `FINANCE_ADMIN` · `DISPATCHER_ADMIN`
- `ADMIN_PRIVILEDGES` (sic): `ALL`, `LEADS`, `LEADS_ADVANCED`, `DISPATCH`, `DISPATCH_ADVANCED`, `ACCOUNTING_ALL`, `ACCOUNTING_PAYMENTS`, `ACCOUNTING_INVOICES`, `ACCOUNTING_CLAIMS`, `DASHBOARD_DISPATCHER`, `DASHBOARD_GENERIC`
- `DRIVER_TYPES`: `INHOUSE` · `LOCAL` · `FREELANCER` · `LONGHAULER` · `TOWINGDRIVER`
- `HAULER_TYPES`: `LONGHAULER` · `LOCALHAULER` · `ALL`
- `OWNER_TYPE` / `YARD_OWNER_TYPE`: `INHOUSE` · `OUTSOURCED`
- `TRIP_OWNERSHIP_TYPE`: `Diesel Auto Express` (inhouse) · `Sub Hauler`
- `DISPATCH_PLAN_TYPES`: `NORMAL` · `PRIME` · `ENTERPRISE` · `CUSTOM`

## Driver / scheduling
- `SCHEDULE_STATUS`: `ALL` · `PENDING` · `APPROVED` · `DECLINED`
- `SCHEDULE_TYPES`: `ALL` · `DAY OFF` · `TRIP`
- `DRIVER_RESPONSE`: `PENDING (0)` · `ACCEPTED (1)` · `REJECTED (2)`
- `TRIP_ROUTE_NAME`: `A` · `B` · `SINGLE`

## Vehicles
- `VEHICLE_TYPE`: `SEDAN` · `JEEP` · `HATCHBACK` · `SUV` · `MINIVAN` · `PICKUP` · `SPRINTER` · `MOTORCYCLE` · `CLASSIC` · `CONVERTIBLE` · `EXOTIC` · `LUXURY`
- `LOCATION_TYPES` (stop type): `POV` · `TERMINAL` · `BUSINESS` · `WAREHOUSE` · `AUCTION` · `DEALER` · `RAILYARD`
- `AUCTION_TYPES`: `COPART` · `IAAI` · `MANHEIM` · `MYCENTRALAUCTION` · `ADESA` · `BRASHERS`
- `ORDER_DATE_VALS` (pickup/delivery window precision): `Estimated` · `Exactly` · `No Earlier` · `No Later`

## Recruiter
- `JOB_POSITIONS`: `LOCAL` · `LONGHAUL` · `BOTH`
- Candidate `CONTACT_STAGES`: `New` · `Active` · `Awaiting` · `Review` · `Hired` · `Rejected`

## Driver expenses (mobile)
- `EXPENSE_CATEGORY` (with caps): `Fuel ($200 max)` · `Small Tools & Equipment ($50 max)` · `Scales ($15 max)` · `Tolls` · `Towing / Yard` · `Truck Repairs` · `Travel` · `Storage` · `Hotels (within reasonable amounts)` · `Taxi / Uber ($70 max)` · `Parking ($200 max/month)` · `Gate Fees ($60 max)` · `Truck Wash ($200 max)` · `DOT Inspections` · `Shop (Employee Only)` · `Office (Employee Only)`

## Shop service categories
`Air / ABS / Breaks` · `Engine` · `Hydraulics` · `Lights / Electrical` · `Maintenance` · `PM Services` · `Tires` · `Transmission` · `Suspension`

## Feedback
`FEEDBACK_STATUSES`: `SENT` · `OPENED` · `REVIEWED`

## Files
`FILE_TYPES`: `LOGO` · `DOCUMENT` · `DELIVERY_RECEIPT` · `SIGNATURE` · `OTHERS`

## Devices / phones
- `DEVICE_TYPES`: `IOS` · `ANDROID` · `WEB`
- `PHONE_TYPES`: `Office` · `Direct` · `Work` · `Home` · `Mobile` · `Fax` · `Main`

## Customer portal status
`ALL` · `QUOTES` · `ORDERS` · `PICKED-UP` · `DELIVERED` · `CANCELLED`

---

**Use this note when designing:**
- Status badges, chips, segmented controls
- Filter dropdowns and list view tabs
- Empty-state copy ("No orders in `CONFIRMED`")
- Form selects (vehicle type, payment terms, claim source, expense category)
- Role-based visibility logic

**If you propose a new status or label, add it here with a note explaining the gap so engineering can wire it in.**

See also: [[Entities]] · [[Workflows]] · [[Modules/Orders & Dispatch]] · [[Modules/Claims]]
