---
tags: [module, tracking, gps, map, product-truth]
module: tracking-gps
audiences: [dispatcher, claims, customer]
generated: 2026-05-20
---

# Tracking & GPS

Live driver location + route on a Google Map.

## Where it lives
`/tracking` (Angular `TrackingModule`).

## Screens designers must support
- **Live map** — Google Maps base; truck pins from `LastGpsModel`; trip polylines from `TripPolylineModel`; route history from `RouteModel`.
- **Filters / legend** — driver, trip, vehicle status, last-seen freshness, online/offline.
- **Truck card / popover** — driver name, current trip, last ping age, speed, next stop ETA (Distance Matrix).
- **Side panel** — list of active trips with mini status, click to focus on map.
- **Geofence event surface** — entered yard / left yard / arrived at stop.
- **Customer-facing tracking** — narrowed map for one order, no other trucks; pull link uses tokenized URL.

## Fields
- **Position** (lat/lng) · **Speed** · **Heading** · **Timestamp** · **Battery / signal** (if reported) · **Trip ref** · **Vehicle status**.
- **Pin colors** — map to `DISPATCH_VEHICLE_STATUS` (e.g. `ON_THE_WAY` = solid, `AT_THE_YARD_*` = ringed).

## Realtime
- Socket.IO server (`server-socket.js`) broadcasts position updates.
- Stale threshold = pin goes ghost after N minutes (design states).
- Reconnect / refresh affordance for client.

## Permissions
`DISPATCH`, `DISPATCH_ADVANCED`. Customers see only their own order's pull link (`Routes/Public/`).

## Gotchas
- **Distance Matrix quota.** Don't request ETAs on every render — design batched / on-click.
- **Polyline stale.** A trip's polyline is cached; reorder of stops requires recompute affordance.
- **Privacy.** When showing customer-facing tracking, no other drivers / trips must leak.
- **Performance.** 50+ trucks on screen — clustering required.

## Audit checks
- [ ] Pin color scheme matches `DISPATCH_VEHICLE_STATUS`
- [ ] Stale / offline state designed (>N min no ping)
- [ ] Cluster behavior defined for many trucks
- [ ] Truck popover shows trip + driver + last-seen + ETA
- [ ] Side panel cross-links to Trip detail
- [ ] Customer-facing variant strips multi-driver context
- [ ] Reorder-stops triggers polyline recompute prompt
