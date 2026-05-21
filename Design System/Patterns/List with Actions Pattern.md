# List with Actions Pattern

How to compose [[Components/List|List]], [[Components/Row Text|Row Text]], [[Components/Trailing (Content Row)|Trailing (Content Row)]], and [[Components/Divider|Divider]] into scrollable lists where each row has tap targets or controls. Used for settings, notifications, trip stops, receipt rows, and any list where rows do more than display text.

For domain-specific rows (Receipts, Trackshop, Truck Service…) compose with [[Components/Content Row|Content Row]] instead — it ships with the right field structure baked in.

- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit)
- **Figma documentation:** Section `1781:9573` "List with Actions Pattern — Documentation" on the `----- Patterns` page

---

## Anatomy

A list with actions is a vertical stack of rows. Each row carries content + a trailing affordance.

- **Section Header (optional)** — [[Components/Action Section|Action Section]] or a `Section/Title` text block above each group of rows
- **Row** — [[Components/List|List]] (View=List for compact, View=Preview Row when thumbnails matter), composed of:
  - Leading icon (24×24) — clarifies the row's intent (envelope, map pin, file)
  - [[Components/Row Text|Row Text]] — primary label + optional helper line
  - [[Components/Trailing (Content Row)|Trailing (Content Row)]] swap — the row's action
- **Divider** between rows — [[Components/Divider|Divider]] (Horizontal) at `Width/XS`, color `Border/Subtle` for hairlines or `Border/Primary` for section breaks
- **Empty state** (no rows) — falls into the [[Empty State Pattern]]

---

## Trailing affordance — pick by intent

| Row's purpose | Trailing variant |
|---|---|
| Navigates to a detail screen | `Type=Trailing-Icon` with a chevron |
| Toggles a setting on/off | `Type=Toggle` (Toggle instance) |
| Picks a value from a list / picker | `Type=Picker` (opens [[Components/Menu\|Menu]] or system sheet) |
| Binary choice without leaving | `Type=Segment` (Yes/No) |
| Adjusts an integer inline | `Type=Count` (Counter instance) |

One affordance per row. Mixing two (e.g., chevron + toggle) confuses the user about what tapping does.

---

## Composition rules

| Rule | Value |
|---|---|
| Screen horizontal margin | `Space/L` (16pt) |
| Row height — minimum | `Space/TapTarget` (44pt) — enforced by List |
| Gap inside a row | `Space/S` (8pt) — between icon, text, trailing |
| Divider between rows | Visible by default (`Show Divider=true`); hide on the **last row** of a section to avoid a stray line above a section break |
| Gap between sections | `Space/2XL` (32pt) — section header → next section |
| Section Header padding | `Space/L` × `Space/S` |
| Long content | Truncate the primary label with `…`; show the helper line for context |

### When to use which `List View`

| View | Use for |
|---|---|
| `List` | Default — dense single-line rows (settings, simple lists) |
| `Preview Row` | Rows with a leading thumbnail or extended content (file pickers, receipt previews) |

---

## Section structure

For lists with more than ~7 rows, group rows under a header:

```
[Section Header: "Notifications"]
  Row 1  ←─ Toggle
  Row 2  ←─ Toggle
  Row 3  ←─ Toggle
[gap: Space/2XL]
[Section Header: "Privacy"]
  Row 4  ←─ Trailing-Icon (chevron)
  Row 5  ←─ Trailing-Icon (chevron)
```

The last row inside each section hides its divider; the gap to the next header provides the visual break.

---

## Empty state inside a list

When the list has zero rows in production, fall back to the [[Empty State Pattern]] — icon + headline + body + optional CTA. Don't render an empty container.

---

## Real Driver App screens using this pattern

Verified against the Driver App DS page on 2026-05-21. See [[_Pattern Evidence Map]] for the full list.

- **Sibebar menu (Done)** — Sidebar section `662:30757` · navigation list with chevrons
- **Settings (Done)** — Settings section `667:31696` · Toggles, Pickers, Trailing-Icon
- **Notifications List (Done)** — Notifications section `662:30691`
- **Receipts list (Done)** — Receipts section `662:30759` · uses [[Components/Content Row|Content Row]] (Receipts variant)
- **Truck Service (Done)** — Truck Service section `662:30875` · [[Components/Content Row|Content Row]] (Truck Service variant)
- **FIles (Done)** + **File (Done)** — Files `667:31228` / My Files `667:31699`
- **Notes List (Done)** — Notes section `667:31700`
- **Request List (Done)** — Requests section `667:31704`
- **Safety List (Done)** — Safety section `667:31706`
- **Trip List / Completed / Archived (Done)** — Trips section `1:28891`
- **Trip Order List Pickup / Delivery / Completed (Done)** — Trips section · uses [[Components/Content Row|Content Row]] (Stops variant) + [[Components/Vertical Badge|Vertical Badge]]
- **Routes List (Done)** + **List of stops (Done)** — Routes section `1:29825`

---

## Do

- ✅ Pick one Trailing affordance per row — match it to the row's actual behaviour.
- ✅ Show `Show Divider=true` for all rows except the last in a section.
- ✅ Group long lists (>7 rows) under section headers.
- ✅ Use the leading icon to clarify row intent at a glance.
- ✅ Fall back to the [[Empty State Pattern]] when the list has zero rows — never an empty container.

## Don't

- ❌ Don't stack two Trailing affordances in one row (e.g., Toggle + Chevron).
- ❌ Don't use plain [[Components/List|List]] for domain-specific rows that have a [[Components/Content Row|Content Row]] variant — use the variant.
- ❌ Don't put multiline labels in single-line `View=List` rows — switch to `View=Preview Row` if content needs more space.
- ❌ Don't tighten the row height below `Space/TapTarget` (44pt) — breaks iOS HIG minimum tap target.

---

Back to [[Patterns]] · [[Design System]].
