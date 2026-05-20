---
tags: [module, crm, accounts, leads, product-truth]
module: crm-accounts
audiences: [sales, admin]
generated: 2026-05-20
---

# CRM & Accounts

The lead-to-customer funnel. Accounts are any external party: customer, lead, broker, carrier, vendor.

## Where it lives
`/crm` (Angular `CRMModule`).

## Screens designers must support
- **Account list** — filterable by type/status/stage; bulk actions; saved views.
- **Account detail** — header (name, type, status, stage, VIP/VVIP badge), tabs: Overview / Contacts / Connections / Orders / Quotes / Notes / Files / History / Integrations.
- **Account create / edit** — type-driven form (Individual vs Company vs Broker fields differ).
- **Contact panel** — list of `AccountContact`s with typed roles.
- **Connection diagram** — visual of related accounts (broker → customer, parent → child).
- **Pipeline board** — leads grouped by `DISPATCH_LEAD_STAGE` (Kanban).
- **Charts dashboard** — `AccountCharts` pre-aggregated data.
- **Call outcome logging** — pick from `ORDER_CALL_OUTCOME_TAGS`.

## Fields
- **Type** (`CUSTOMER_TYPES`) · **Status** (`ACCOUNT_CONTACT_STATUSES`) · **Sub-status** (`ACCOUNT_CONTACT_SUBSTATUSES` — DNC/Suspended/Restricted) · **Stage** (`DISPATCH_LEAD_STAGE`) · **Privilege** (`CUSTOMER_PRIVILEGE_TYPES`) · **Owner** · **Source** (`LEAD_SOURCE`) · **Created** · **Last activity**.

## Contact typing
- `ACCOUNT_CONTACT_INDIVIDUAL_TYPES` — for people: BROKER, DRIVER, DISPATCH, EVERYTHING, CUSTOMER, ACCOUNTING, CLAIMS, MECHANIC, POV.
- `ACCOUNT_CONTACT_COMPANY_TYPES` — 26 company types from `AUTO SHOP` to `AUCTION`; design as searchable picker, not a flat dropdown.

## Permissions
- `LEADS` / `LEADS_ADVANCED`. DNC/Suspended/Restricted must be enforced in UI (no quote creation).

## Workflows
1. **Lead capture** — public quote widget creates Account (type LEAD).
2. **Ad attribution** — `TrackAdsModel` records UTM/click ID; show source on detail.
3. **Promote lead** — Lead → Prospect → Active via status change + stage.
4. **Quote / Order** — see [[Quotes & Load Board]] and [[Orders & Dispatch]].
5. **Connections** — broker accounts route orders to customer accounts.

## Gotchas
- **Multi-role accounts.** Same Account can be customer **and** broker **and** carrier. Don't gate UI by single type.
- **DNC enforcement.** `ACCOUNT_CONTACT_SUBSTATUSES.DO NOT USE` must visibly block "New Quote" / "Email" actions.
- **VIP/VVIP badges** affect dispatcher prioritization — surface in lists, not just detail.
- **Soft delete** — archive/restore only.

## Audit checks
- [ ] Account type selector covers all 6 types
- [ ] Status × Sub-status × Stage shown distinctly (3 axes, not 1)
- [ ] VIP/VVIP badge on list rows
- [ ] DNC blocks "New Quote" / "Email" affordances
- [ ] Contact panel allows typing per `INDIVIDUAL_TYPES`/`COMPANY_TYPES`
- [ ] Connections visualized
- [ ] Source / UTM exposed
