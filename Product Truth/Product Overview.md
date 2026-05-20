---
tags: [overview, product-truth]
type: overview
generated: 2026-05-20
---

# Product Overview

**HaulEx is a logistics SaaS for vehicle hauling / auto transport.** It owns the entire pipeline: lead → quote → load board → trip dispatch → driver mobile workflow → POD/inspection → invoice → settlement → claim. Add-ons: shop/maintenance, driver recruiting, carrier/sub-hauler management, workflow automation, dashboards.

## Core idea (one paragraph)
A customer requests a vehicle move. Sales turns that lead into a **Quote**. Accepted quotes become **Orders** containing one or more **OrderVehicle** lines and **OrderStops** (pickup/delivery). Dispatchers group orders into **Trips** assigned to **Drivers** (in-house or sub-haulers). Drivers run the trip from the **iOS Driver App** — accepting the trip, inspecting vehicles at pickup, capturing POD/signatures at delivery. Live **GPS** + **Socket.IO** keep the CRM updated. Delivered orders flow into **Invoices**, **Settlements**, and (when something goes wrong) **Claims**.

## What "the app" actually is
Three distinct products that share the same backend:

| Surface | Tech | Audience | Primary use |
|---|---|---|---|
| **CRM Web** (`D:/CRM_V2`) | Angular 21, NgRx 20 | Office staff (admin, sales, dispatch, finance, claims) | All operational work |
| **Driver iOS App** (HaulEx UIKit Figma `3qOFF7kHsaZPfdftDb1CVz`, Driver App Figma `yhxCSzJrafZbqXGZOCBCKE`) | iOS, calls `Routes/Mobile/` | Drivers in the field | Run the trip, capture inspection/POD, log expenses |
| **Customer / Public Web** | Same Angular app + `Routes/Public/` | Customers, leads | Get a quote, track an order, pay an invoice |

Additional small surfaces:
- **Carrier portal** — sub-hauler auth + order assignment (`Routes/Carrier/`).
- **Admin** — login, permissions, roles, users, equipment (`Routes/Admin/`).

## Why this matters for design
Every screen you design lives on one of these surfaces and serves one persona, but **the data flows through all of them**. A status change on the Driver iOS app has to be reflected in the CRM Load Board within seconds (Socket.IO). Designs must respect this — see [[Workflows]] for the full state machines.

## Stack truth (for context only — designers don't ship code)
- Frontend: Angular 21, NgRx 20, hash routing (`#/<userIndex>/...`), Socket.IO client.
- Backend: Hapi.js 21 (Node), MongoDB (Mongoose, soft-delete plugin), Socket.IO server, Firebase Admin (FCM) + APN for push.
- Integrations affecting UI: Stripe, Authorize.Net, QuickBooks, SendGrid, Twilio, RingCentral, Dialpad, Google Maps / Distance Matrix, OneSignal, Central Dispatch (3rd-party load board), Anthropic Claude.

See [[Personas & Surfaces]] · [[Information Architecture]] · [[Entities]] · [[Status Vocabulary]] · [[Workflows]].
