# Form Pattern

How to compose [[Components/Input|Input]], [[Components/Text Area|Text Area]], [[Components/Checkbox|Checkbox]], [[Components/Toggle|Toggle]], and [[Components/Button|Button]] into data-entry screens. Used for log-in, profile edits, request submission, notes, settings, and any place the user provides structured data.

- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit)
- **Figma documentation:** Section `1774:9451` "Form Pattern — Documentation" on the `----- Patterns` page

---

## Anatomy

A form is a vertical stack of field rows + a submit affordance.

- **Header (optional)** — [[Section Header Pattern]] or [[Components/Action Section|Action Section]] for grouped contexts
- **Field rows** — one per input:
  - [[Components/Input|Input]] for single-line text, numbers, search
  - [[Components/Text Area|Text Area]] for multi-line text (notes, descriptions)
  - [[Components/Checkbox|Checkbox]] for multi-select choices (with `Show Text=true`)
  - [[Components/Toggle|Toggle]] for instant on/off settings (paired with a label outside the toggle)
  - [[Components/Select|Select]] + [[Components/Menu|Menu]] for picking from a known list
- **Helper line (optional)** — error / hint text under the field. Input / Text Area expose `Helper` + `Show Helper` properties for this
- **Submit affordance** — [[Components/Button|Button]] (`Size=L, Type=Primary, Role=Inverse`) anchored to the bottom of the screen or sheet

Field-level anatomy (label, container, placeholder, helper) lives inside each component note — this pattern only governs how the fields combine.

---

## Composition rules

| Rule | Value |
|---|---|
| Screen horizontal margin | `Space/L` (16pt) |
| Gap between fields | `Space/L` (16pt) |
| Gap between field groups / sections | `Space/2XL` (32pt) |
| Gap label → field (inside one component) | `Space/S` (8pt) — set by the component, don't override |
| Submit button bottom margin (above safe area) | `Space/L` (16pt) |
| Submit button width | Fill container (full width minus 2× `Space/L`) |
| Minimum interactive height | `Space/TapTarget` (44pt) — already enforced by atoms |
| Vertical scroll on keyboard | Required — focused field always visible above keyboard |

### Field-state choices per use case

| Situation | State variant to apply |
|---|---|
| Empty form field awaiting input | Input: `State=Default` |
| Field currently focused | Input: `State=Focused` (Border/Blue) |
| Field with a typed value | Input: `State=Filled` |
| Inline validation error | Input: `State=Negative` **and** populate `Helper` with the error message |
| Field temporarily unavailable | Input: `State=Disabled` (do not use for read-only display of saved values) |

### Required vs optional fields

- Mark required fields with an asterisk in the `Label` text — e.g., "Email *"
- Mark optional fields with "(optional)" in the `Label` — never leave it ambiguous

### Validation timing

- **Validate on submit** by default — don't flag errors as the user types
- **Validate on blur** for strict-format fields (phone, date, email)
- **Never clear a field** to show an error — show the error, keep the user's input

---

## Layout choices — sheet vs screen

| Form size | Container |
|---|---|
| 1–3 fields | Half sheet (medium detent) — see [[Sheet Pattern]] |
| 4+ fields, or context needs full focus | Full sheet or pushed screen with a Navigation Bar (organism, see [[Sheet Pattern]]) |
| Single-field edits | Action Sheet or inline edit on the existing row |

For pushed screens with a Navigation Bar, place `Cancel` on the leading edge and `Save` / `Done` on the trailing edge.

---

## Real Driver App screens using this pattern

Verified against the Driver App DS page on 2026-05-21. See [[_Pattern Evidence Map]] for the full list.

- **Log In (Done)** + **Log in via Phone Number (Done)** — Login section `1:29600`
- **Carrier Sign-up (Done)** — multi-field registration · Login section
- **Forgot Password Stage 1 / 2 / 3 (Done)** — multi-step recovery · Login section
- **Password (Done)** + **Not Match (Done)** — Change Pass section `667:31702` · shows `Negative` state in practice
- **Profile Settings (Done)** — Profile section `667:31697`
- **New Note (Done)** — Text Area form · Notes section `667:31700`
- **Driver Notes (Done)** — Text Area form · Driver Notes section `737:21942`
- **Add Truck Services (Done)** — multi-field form · Truck Service section `662:30875`
- **Receipts Add COP/COD (Done)** — amount + type form · Receipts section `662:30759`
- **Add Driver Notes (Done)** + **ETA (Done)** + **Customer Template (Done)** — Order Details section `667:31707`

---

## Do

- ✅ Use a vertical single-column layout — side-by-side fields only for very short, tightly related pairs (e.g., expiry month + year).
- ✅ Always show the `Label` on every field — no placeholder-only inputs.
- ✅ Pair `State=Negative` with a populated `Helper` line — error border alone fails accessibility.
- ✅ Make the Submit button full-width and anchor it to the bottom.
- ✅ Disable the Submit button until the minimum required fields are filled.
- ✅ Use sentence case in labels — matches iOS HIG conventions.

## Don't

- ❌ Don't rely on the placeholder for the field's meaning — placeholder disappears on typing.
- ❌ Don't place destructive actions (Delete, Clear) near the Submit button — separate them spatially.
- ❌ Don't use all-caps labels.
- ❌ Don't use `Input` `State=Disabled` for read-only display of saved values — use a [[Components/Content Row|Content Row]] or [[Components/Row Text|Row Text]] instead.
- ❌ Don't override the component-internal spacing (label → field gap, helper gap) — that's owned by the atom.

---

Back to [[Patterns]] · [[Design System]].
