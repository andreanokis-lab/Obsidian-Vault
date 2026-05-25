---
status: in-progress
type: flow-spec
figma_node: "796:926"
figma_file: yhxCSzJrafZbqXGZOCBCKE
---

# Salary Request Flow

Three-screen flow that lets a driver submit a salary-related request (Advance / Reimbursement / Loan) and see its status. Built in the new **Salary Requests** section on Page 5, sitting below [[Orders List]] and [[Order Files]].

**Figma section:** https://www.figma.com/design/yhxCSzJrafZbqXGZOCBCKE/HaulEx-Driver-App?node-id=796-926

## Why this flow

Drivers are paid out on a delay (weekly / monthly settlements). When fuel goes onto a personal card, when a hotel needs to be booked mid-route, or when there's a personal cash crunch, the driver needs a fast in-app way to ask for an advance, claim a reimbursement, or request a loan against future earnings. Today this is presumably done over chat or by calling dispatch — moving it into the app makes it auditable, lets the back office prioritize, and reduces ad-hoc dispatcher overhead.

This is positioned as a **key user-driver flow**: high-frequency for some drivers, high-stakes when it matters, and the kind of feature that earns trust.

## Screens

| # | Screen | Node | Source |
|---|---|---|---|
| 1 | Salary Requests list | `798:20481` | Cloned from `1:40484` Request List (Done) |
| 2 | New Salary Request form (half sheet) | `804:20481` | Cloned from `379:25717` Create Request |
| 3 | Request Submitted confirmation | `807:20481` | Cloned from `1:40509` Request Placeholder (Done) + custom CTA |

All three screens are 393×852 iPhone frames; the section is 1355×924 (3 screens × 393 + 4 gaps × 44 + 44 inner padding) at page coordinates `(-119, 751)`.

### Screen 1 — Salary Requests list (`798:20481`)

- Nav bar: back chevron + title **"Salary Requests"**
- Segment Control: **All** / Pending / Approved / Declined
- 6 request cards (DS `Card` instances) with:
  - **Title** (was Full Name): request type — Salary Advance / Reimbursement / Loan
  - **Status badge**: Approved (blue), Pending (yellow), Declined (gray)
  - **Amount** (was truck info) on Approved/Loan rows
  - **Submitted date** (was trip number) on Approved/Loan rows
  - **Reason chip** (was Day Off/Trip): Advance / Fuel / Tolls / Loan
  - **Need by** range (single date)
- FAB (`+`) bottom right → opens Screen 2

Card variants vary — Pending/Declined rows render in a more minimal form (no amount or submitted line) because of how the underlying DS Card variant slots are wired. Acceptable for v1; can be reconciled when we fork a dedicated `Card · Role=Salary Request` variant.

### Screen 2 — New Salary Request (`804:20481`)

iOS Half Sheet over the dimmed Salary Requests list. Layout:

| Field | Value | Notes |
|---|---|---|
| Sheet title | **Request Salary** | with `Close` (left) / `Submit` (right) |
| Type | `Salary Advance ▼` | DS Select; options would be Salary Advance · Reimbursement · Loan · Other |
| Amount | `$2,500.00` | Currency input — formatting handled client-side |
| Need by | `Date needed → May 28, 2026` | Single date picker |
| Reason | `Why do you need this advance?` | DS Text Area, ~5 rows |

One small visual artifact: an empty container row sits below the date picker (residue from the cloned Departure row). Acceptable for v1; collapse with `visible = false` on the row in next polish pass.

### Screen 3 — Request Submitted (`807:20481`)

- Status bar + back chevron only (no nav title)
- Centered success block:
  - Icon (calendar — should be a checkmark; see follow-ups)
  - **Request Submitted** (28pt Semibold, white)
  - **$2,500.00** (22pt Semibold)
  - **Salary Advance** (15pt Regular, tertiary text)
  - Helper: *"We'll review your request within 24 hours and notify you here."*
- Bottom CTA (custom auto-layout, not yet a DS Button instance):
  - Primary: yellow rounded **Done** button (361×56, radius 999)
  - Secondary: blue text link **View request**

## Key user-driver intent

This flow optimizes for the driver who:
- Doesn't want to call dispatch for money
- Wants a same-day confirmation, even if pending review
- Submits irregularly (once a week or less) — speed > power-user shortcuts

Design choices that follow:
- **Half-sheet over full screen** for the form — keeps the list visible, reinforces "this is a quick task," easy to dismiss.
- **Pre-selected Type = Salary Advance** — covers the highest-frequency case.
- **Single Need-by date**, not a range — reduces decision overhead.
- **No mandatory file attachment** — drivers may not have receipts in hand for advances; reimbursements can attach via the FAB on the detail page (future).
- **24-hour SLA copy** — sets expectation. Replace with real SLA when we have one.

## Token & system compliance

| Element | Token |
|---|---|
| List spacing | Inherited from cloned `Request List` — `Space/L` row gap |
| Card rows | DS `Card` component (variant context preserved) |
| Sheet | iOS Half Sheet pattern — see [[Sheet Pattern]] |
| Form fields (Select, Input, Date, Text Area) | DS instances — semantic colors only |
| Status badges | DS Badge component, Role variants (success/warning/error) |
| Success screen Done button | **Manually built**, NOT a DS Button instance — hardcoded radius 999 + HaulEx yellow `{1.0, 0.85, 0.18}` |

## Font workaround

Same as every other Driver App screen built on this host: `SF Pro Text Regular` not installed → cloned each reference screen, walked text nodes, `setRangeFontName` to `SF Pro Regular`, then reparented. Totals: 40 (list) + 56 (form) + ~25 (success) text nodes rewritten.

## Follow-ups

- **Done button** on Screen 3 is hand-built, not a DS Button instance. Swap to `Button / Primary / L` instance once we resolve the SF Pro Text font situation (it'd fail font-load right now).
- **Calendar icon → checkmark** on Screen 3. The icon swap requires the `Icons/checkmark-circle-fill` (or similar) component key — search [[Component Status]] for confirmation, then swap the instance via `swapComponent`.
- **Empty row residue** below the date picker on Screen 2 — set `visible = false` on the Departure row container.
- **Card variant for Salary Requests** — current rows reuse the time-off request `Card` variant, so some rows lose info inappropriately. File a DS task: new `Card · Role=Salary` variant with slots for `Amount`, `Submitted`, `Reason chip`, `Need by`.
- **States not yet designed**: empty state (no requests), error states (submission failed, network), edit-pending (Driver wants to update a Pending request), detail view (tap a card → see breakdown), notification (`Approved`/`Declined` push).
- **Backend / data contract**: needs a server-side definition — types, statuses, decision turnaround, payout method. Loop in a PM before any handoff.
- **Permissions**: not every driver should see every type — Loan likely requires tenure. Conditional Type options driven by driver profile.
- **Tie-in to [[Orders List]]**: when reimbursing a specific order, the form should optionally accept an Order # link.

Back to [[Driver App]] · [[Design System]] · [[Sheet Pattern]] · [[Form Pattern]].
