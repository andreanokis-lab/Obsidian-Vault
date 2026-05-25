---
status: in-progress
type: flow-spec
figma_node: "817:1465"
figma_file: yhxCSzJrafZbqXGZOCBCKE
---

# Breakdown Alert Flow

Three-screen high-urgency flow that lets a driver alert dispatcher about a problem on the road — mechanical breakdown, accident, flat, fuel, cargo, anything that stops the truck. Built in the new **Breakdown Alerts** section on Page 5, below the Salary Request flow.

**Figma section:** https://www.figma.com/design/yhxCSzJrafZbqXGZOCBCKE/HaulEx-Driver-App?node-id=817-1465

## Why this is a key-user-driver flow

When a truck stops moving, the carrier loses money every minute. Dispatcher needs to know **fast**, with **enough detail** to roll a truck / call a mechanic / route a fuel delivery. Today this likely happens on the phone, blocking dispatcher capacity and producing no audit trail. Putting it in the app:

- Captures location automatically (GPS).
- Triages by severity so dispatch can prioritize.
- Logs timestamps for insurance, payroll-detention, and incident review.
- Frees dispatch from being a switchboard during a multi-truck event.

This flow has **higher urgency** than any other driver flow we've built. Design choices reflect that:
- Picker is one-tap-per-card (no "next" step).
- Severity defaults to *Urgent*, not the lowest tier — drivers tend to under-classify under stress, dispatcher prefers to triage down rather than miss escalations.
- Location is auto-populated, not asked.
- Description placeholder uses sensory prompts ("see, hear, smell") to scaffold the panicked driver.
- Primary actions are **red** throughout — visually distinct from normal yellow brand CTAs, signaling "this is the emergency path."

## Screens

| # | Screen | Node | Source |
|---|---|---|---|
| 1 | Report a Problem (issue type picker) | `818:1465` | Cloned from [[Salary Request Flow]] list (`798:20481`) + simplification |
| 2 | Report Details (half sheet) | `821:1584` | Cloned from [[Salary Request Flow]] form (`804:20481`) + relabel |
| 3 | Alert Sent (confirmation + status timeline) | `823:1776` | Cloned from [[Salary Request Flow]] success (`807:20481`) + recolor + custom timeline |

All three are 393×852 iPhone frames. Section is 1355×924 at `(-2407, 1708)`.

### Screen 1 — Report a Problem (`818:1465`)

- Nav: back chevron + "Report a Problem"
- Segment Control: **hidden** (no filtering — picker is one-shot)
- 6 large issue-type cards (DS `Card` instances, status badges hidden):

| Card | Subtitle | Chip |
|---|---|---|
| Mechanical Breakdown | Engine, transmission, electrical | Critical |
| Accident or Collision | Vehicle hit, scraped, or rolled | Critical |
| Flat Tire | Blowout, slow leak, sidewall | Tire |
| Out of Fuel | Need fuel delivery on route | Fuel |
| Cargo Issue | Strap loose, vehicle shifted | Cargo |
| Other | Anything else dispatcher should know | Other |

- FAB: **hidden** (no "add" — pick triggers next screen)

### Screen 2 — Report Details (`821:1584`)

Half sheet over the picker; user has tapped Mechanical Breakdown.

| Field | Value | Notes |
|---|---|---|
| Sheet title | **Report Details** | with `Close` / **Send Alert** (right action) |
| Issue Type | `Mechanical Breakdown ▼` | Pre-selected from tapped card; user can still change |
| Severity | `Urgent — need help now` | Defaults to Urgent. Options: Critical / Urgent / Standard |
| Location | `I-80 W · MP 142, Reno NV` + blue `Auto` chip | Auto-populated from GPS — driver shouldn't have to type while stressed |
| What's happening? | `Describe the issue — what you see, hear, smell. Photos help.` | Sensory-prompt placeholder; Text Area |

Same ghost-row residue as the salary form (cleared Departure container). To fix in polish pass: `visible = false` on the row container, not just clearing text.

### Screen 3 — Alert Sent (`823:1776`)

- Status bar + back chevron only
- Centered header block:
  - Icon (currently calendar — should be a warning/alert glyph; see follow-ups)
  - **Alert Sent** (28pt Semibold, white)
  - **Mechanical Breakdown** (22pt Semibold)
  - **Urgent — sent 12:34 PM** (15pt Regular, tertiary)
  - Helper: *"Dispatcher has been notified. Help is on the way."*
- **Status Timeline** card (custom-built, dark surface, 16pt radius):

| Step | State | Time |
|---|---|---|
| Alert sent | done (green dot) | 12:34 PM |
| Dispatcher acknowledged | pending (gray dot) | — |
| Help dispatched | pending (gray dot) | — |
| Arrived on scene | pending (gray dot) | — |

- Bottom CTA stack:
  - Primary: red **Update Status** button (matches alert-red theme)
  - Secondary: blue link **Call dispatcher · (555) 421-9988** (tap-to-call)

## Token & system compliance

| Element | Status |
|---|---|
| Issue cards | DS `Card` instances with status badges hidden |
| Form fields (Select, Input, Date row, Text Area) | DS instances inherited from cloned salary form |
| Status timeline | **Custom built** with `figma.createAutoLayout` — not a DS component |
| Alert-red color | Hardcoded `{0.95, 0.27, 0.27}` — should be promoted to a `Color/Alert/Critical` semantic token |
| Update Status button | **Custom built**, not a DS Button instance (same constraint as [[Salary Request Flow]] success) |
| Dispatcher contact link | Custom text — should become a [[Content Row]] with leading phone icon |

## Font workaround

Same `SF Pro Text` → `SF Pro` rewrite as every other screen. Cloned bases already had the rewrite applied (from the Salary flow), so no additional font work was needed.

## Follow-ups

### High-priority polish

- **Icon swap on Screen 3** — calendar → `Icons/exclamationmark-triangle-fill` or `Icons/sos`. The icon's fill recolor didn't land (fill bindings on locked instance children).
- **Empty ghost row** on Screen 2 below location — collapse with `visible = false`.
- **Send Alert truncation** — sheet header right action ("Send Alert") is wider than the original "Submit" and clips. Either shorten ("Send") or widen the right slot.
- **Alert-red token** — formalize `Color/Alert/Critical` in [[Colors - Semantic]] and rebind hardcoded reds.

### Missing variants

- **Severity selector** — currently a Select. Should arguably be a 3-segment control with color-coded segments (red / orange / yellow).
- **Photo capture row** — the description prompts photos but there's no photo-attach affordance. Hook into [[Camera Capture Flow]].
- **Pre-flight quick-pick** — for true emergencies, "I'm OK" / "I'm hurt" toggle before going deeper. See *Safety Check-In* in [[Driver App]].
- **Status updates by dispatcher** — push notification + lock-screen update so driver sees progress without re-opening the app.
- **Cancel alert** — what if the driver fixed it themselves? Need a "Cancel / Resolved" path off Screen 3.
- **Multi-stop scenarios** — when the breakdown is at a Pickup location, link to the [[Orders List]] order so the customer can also be notified.

### Backend & ops

- **SLA copy** — "Help is on the way" is a promise. Confirm dispatcher SLA before shipping.
- **Severity → routing** — Critical should page on-call; Standard can queue. Spec needed from ops.
- **Location accuracy** — display nearest milepost AND lat/long (collapsed) so dispatcher can plug into Google Maps.
- **Offline behavior** — driver may have no signal at the breakdown site. Need queued-send with retry + offline confirmation copy ("Alert will send when you have signal").
- **Integration with [[Salary Request Flow]]** — if breakdown causes detention, the resulting reimbursement should pre-fill from the alert.

Back to [[Driver App]] · [[Design System]] · [[Sheet Pattern]] · [[Form Pattern]] · [[Salary Request Flow]].
