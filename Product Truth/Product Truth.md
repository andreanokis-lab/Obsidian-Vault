---
tags: [hub, product-truth, haulex]
type: hub
generated: 2026-05-20
source: D:/Info-storage/HaulEx-Vault/HaulEx/_vector-db
---

# HaulEx — Product Truth (Designer Source of Truth)

This is the **designer-facing mirror** of the HaulEx codebase. It tells you what the product actually does today — surfaces, screens, entities, fields, statuses, permissions — so you can audit Figma work against shipping reality.

> Code knowledge base lives at `D:/Info-storage/HaulEx-Vault/HaulEx/_vector-db/` (frontend `D:/CRM_V2`, backend `D:/Backend`). This vault distils it to what a designer needs.

## Start here
1. [[Product Overview]] — what HaulEx is, in one page
2. [[Personas & Surfaces]] — who uses what (CRM web, Driver iOS, Admin, Customer/Public, Carrier)
3. [[Information Architecture]] — every top-level route, what lives inside
4. [[Status Vocabulary]] — the enums that become badges, filters, empty states
5. [[Entities]] — the nouns your UI must represent (Order, Trip, Account…)
6. [[Workflows]] — quote → order → trip → POD → invoice → settlement → claim

## Modules (designer view)
Each note answers: **What screens? What fields? What states? What actions? What permissions? What gotchas?**

Priority (built first):
- [[Modules/Orders & Dispatch]]
- [[Modules/Trips]]
- [[Modules/CRM & Accounts]]
- [[Modules/Quotes & Load Board]]
- [[Modules/Driver Mobile (iOS)]]
- [[Modules/Tracking & GPS]]
- [[Modules/Expense, Settlements & Invoice]]
- [[Modules/Claims]]

Remaining (stubbed):
- [[Modules/Tasks]] · [[Modules/Calendar & Schedule]] · [[Modules/Chat & Realtime]] · [[Modules/Notifications & Push]] · [[Modules/Carriers & Sub-haulers]] · [[Modules/Drivers & Candidates]] · [[Modules/Shop & Maintenance]] · [[Modules/Workflow Automation]] · [[Modules/Feedback]] · [[Modules/Reports & Dashboards]] · [[Modules/Admin & Permissions]] · [[Modules/Auth & Users]] · [[Modules/Public & Landing]] · [[Modules/Integrations]]

## Auditing your designs
- [[_audit/Audit Checklist Template]] — copy this when reviewing a Figma screen against the code truth.
- [[_audit/How to use this vault]] — workflow for design review.

## Relation to other parts of this vault
- **Design System/** — tokens, components, primitives (HaulEx UIKit Figma `3qOFF7kHsaZPfdftDb1CVz`).
- **Driver App/** — screen specs and flows for the iOS Driver App (Figma `yhxCSzJrafZbqXGZOCBCKE`).
- **Product Truth/** (this folder) — what shipping code does. Use it as the **reality check** when designing.

## Provenance
Every claim here is sourced from `_vector-db/`. When uncertain, grep `D:/Backend` or `D:/CRM_V2` directly — the code is authoritative.
