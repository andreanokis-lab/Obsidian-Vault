---
status: in-progress
type: screen-spec
figma_file: pxgSYYHXZvoBzTek9xJVZM
---

# Customer Portal — Order Detail Page

The order/quote detail screen in the **Customer Portal / My Orders** web app (Figma file `pxgSYYHXZvoBzTek9xJVZM`). This is the page a customer lands on to track a single vehicle shipment. Distinct product from the [[Driver App/Driver App|Driver App]] — web, not iOS — but reuses the same HaulEx visual language.

**Figma:**
- Polished "elements" reference — [node 714-8301](https://www.figma.com/design/pxgSYYHXZvoBzTek9xJVZM/Customer-Portal---My-Orders?node-id=714-8301)
- Wireframe structure explorations — [node 724-8890](https://www.figma.com/design/pxgSYYHXZvoBzTek9xJVZM/Customer-Portal---My-Orders?node-id=724-8890)
- Wireframe selections (built by Claude) — Section **"Order Detail — Wireframe Selections"**, page *customer portal* (`725:10298`)

## Building blocks (consistent across all explorations)

- **Header:** HaulEx logo + company name, `Quote #10933` pill, account avatar.
- **Order progress** — horizontal 3-step stepper (Booked → Picked up → Delivered) + estimated delivery date.
- **Confirm-step flow** — a stepped action ("Step 1 of 3: Confirm pickup address") with Confirm / Cancel + page-dot indicator. Same mechanic reused for confirming vehicle details.
- **Order status feed / timeline** — vertical rail of timestamped events with a current-step checkmark node.
- **Vehicle details** — vehicle name + spec rows + **BOL set** chips (links to Bill of Lading).
- **Payment details** — line items + total + **Download** (→ Bill of Lading) + **Buy / Pay now** CTA.
- **Map** — live location (embedded or linked via "See map").
- **Contacts & info** — accordion rows (carrier, dispatch, order info, payment, insurance).
- **Order note** — editable note field.
- **Trip history** — collapsible route/sparkline history.

## Open questions (from wireframe annotations)

- Download must redirect to **"Bill of Lading"**.
- Can the customer **complete a purchase / payment** inside the portal? (Buy CTA placement assumes yes.)

## Wireframe directions explored

The original wireframes (724-8890) showed **2 directions × 2 states**:
- **Direction A — two-column dashboard:** horizontal stepper + cards (Order Progress, Trip History, Vehicle Details) on the left; one tall right panel (Payment + Map + Contacts) + Order Note. States: default and active (Step-1-of-3 confirm + Buy).
- **Direction B — timeline-led tracking:** narrow left column (Vehicle, Payment+Buy, Contacts) + a vertical Order Status timeline with an event feed and "See map". States: default and "Confirm Vehicle Details" alert.

Difference: A = information dashboard (horizontal stepper, embedded map); B = tracking feed (vertical timeline, map linked out).

## Selections delivered (hybrid, clean grey-block wireframes)

Per request — a **hybrid of both directions**, low-fidelity grey blocks. Two options:

| Option | Idea | Layout |
|---|---|---|
| **Option 1 — Timeline + detail panel** (`725:10299`) | Status feed is the hero (B) wrapped in A's chrome | Header + confirm banner + horizontal stepper on top; left = vertical **status event feed** + Vehicle + Trip history; right sidebar = Payment(+Pay now) + Map + Contacts accordion + Order note |
| **Option 2 — Map-forward + consolidated rail** (`725:10408`) | Map is the hero; status condensed | Same top chrome; left = large **Map** + Vehicle + Trip history; right = one panel stacking compact status mini-timeline + Payment(+Pay now) + Contacts; Order note below |

Both keep: horizontal top stepper + confirm-step banner (from A), and the vertical status timeline (from B). They differ in what leads the left column (event feed vs. map) and how the right rail is composed.

## Follow-ups

- Decide Option 1 vs 2 (or merge) before raising fidelity to real DS components.
- Resolve the two open questions above with product.
- Map BOL chips / Download to the actual Bill of Lading destination.

Back to [[Hub]].
