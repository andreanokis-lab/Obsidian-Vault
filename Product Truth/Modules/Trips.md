---
tags: [module, trips, dispatch, product-truth]
module: trips
audiences: [dispatcher, driver]
generated: 2026-05-20
---

# Trips

A **Trip** groups multiple Orders for one driver/truck. The trips board is the **dispatcher's primary work surface**.

## Where it lives
- `/trips` — board view (Angular `TripsModule`, lazy-loaded).
- Driver iOS — own trips list + active trip detail.

## Screens designers must support
- **Trip board** — Kanban-like columns by `TRIP_STATUS`, or table view filtered by driver/date.
- **Trip builder modal** — drag & drop orders into a trip (uses SortableJS/Dragula in code); assign driver/truck/trailer; preview polyline.
- **Trip detail (CRM)** — header (#, status, driver, ownership), order list, map with polyline, deposits panel, history.
- **Trip detail (Driver iOS)** — list of stops in sequence, navigate-to-next-stop CTA, inspection entry per vehicle.
- **Driver assignment / response modal** — push sent, awaits `DRIVER_RESPONSE`.

## Fields
- **Trip #** (CounterService) · **Status** (`TRIP_STATUS`) · **Ownership** (`TRIP_OWNERSHIP_TYPE`) · **Route name** (`A`/`B`/`SINGLE`) · **Driver** · **Truck/Trailer** · **Order count** · **Total miles** · **Deposits** · **Driver response**.

## Statuses
Numeric — display the **name**: `CREATED`, `PENDING`, `ONGOING`, `ON_THE_WAY`, `CONFIRMED`, `COMPLETED`, `EXPIRED`, `REJECTED`, `CANCELLED`, `CANCELLED_BY_DRIVER`, `CANCELLED_BY_ADMIN`, `REQUESTED`.

Driver response (separate field): `PENDING (0)` · `ACCEPTED (1)` · `REJECTED (2)`.

## Actions per state
| State | Dispatcher CTA | Driver CTA (iOS) |
|---|---|---|
| `CREATED` | Add orders, assign | — |
| `REQUESTED` | Cancel request | Accept / Reject |
| `PENDING` (accepted) | Send to driver | Start trip |
| `ONGOING` / `ON_THE_WAY` | Track, message | Update status, inspect vehicle |
| `COMPLETED` | Close, settle | — |
| `EXPIRED` / `REJECTED` | Reassign | — |
| `CANCELLED_BY_*` | Reopen / archive | — |

## Permissions
`DISPATCH`, `DISPATCH_ADVANCED`. Drivers see only their own trips on iOS.

## Realtime
- Socket.IO broadcasts trip updates to dispatcher boards.
- Push (FCM/APN) to driver on assign / reassign / cancel.

## Gotchas
- **Trip route splitting** — `TRIP_ROUTE_NAME` (`A`/`B`/`SINGLE`) lets one truck handle two legs; designs must show both legs on the map distinctly.
- **Polyline cached** in `TripPolylineModel` — design the "recompute route" affordance.
- **Deposits** are advance payments against the trip — surface on the detail.
- **Sub-hauler trips** behave the same but assignment goes to a carrier account, not an in-house driver.

## Audit checks
- [ ] Status pill covers 12 states
- [ ] Driver response shown distinctly from trip status
- [ ] Trip detail shows polyline + stop sequence
- [ ] Deposits panel visible
- [ ] Sub-hauler vs inhouse visually distinguished
- [ ] Reassign / cancel paths designed
- [ ] Driver iOS trip card matches CRM info parity (no leaking dispatcher fields)
