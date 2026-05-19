# Segment Control

iOS-style segmented control — a row of 2–4 [[Tab Item]] pills inside a `Background/Subtle` container, with one item selected at a time. Scrollable variant available when segments overflow the screen width.

For a single pill (not part of a segment group) use [[Tab Item]] alone.
For drop-down value picking use [[Select]] + [[Menu]].

- **Component set node:** `321:1008`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=321-1008)
- **Figma section:** `----- Segment Control` → "Segment Control"
- **Figma documentation:** Section `1748:7889` "Segment Control — Documentation" on the same page

---

## Composition

`Selected=1, Segments=3, Scrollable=No` — horizontal pill containing 3 Tab Items.

| Layer | Bindings |
|---|---|
| Container (FRAME) | fill `Background/Subtle` · radius `Radius/Pill` · padding `Space/XS` all sides · gap `Space/XS` |
| Selected Tab Item | fill `Background/Inverse` · `Radius/Pill` · padding `Space/Zero` × `Space/S` |
| ↳ Label | `Text/Secondary/*` (15pt, SF Pro Text) · `Text/Primary Inverse` |
| Unselected Tab Items | no fill (transparent) · same padding |
| ↳ Label | `Text/Secondary/*` · `Text/Primary` |

---

## Variants

13 combinations across 3 axes.

| Axis | Values | Notes |
|---|---|---|
| `Segments` | `2` · `3` · `4` | How many segments are shown |
| `Selected` | `1` · `2` · `3` · `4` | Which segment is currently active |
| `Scrollable` | `No` · `Yes` | Yes when segments overflow horizontally — only at `Segments=4` |

Not every combination exists — `Scrollable=Yes` only appears with `Segments=4`.

---

## Instance properties

None at the top level — the Tab Item labels inside each segment are overridden via the inner instance.

---

## Do

- ✅ Use Segment Control to pick between 2–4 mutually exclusive views or filters.
- ✅ Match `Selected` to the currently active segment in your design.
- ✅ Use `Scrollable=Yes` for 4-segment groups where labels are long and would overflow the row.
- ✅ Keep segment labels short (1–2 words) — Apple HIG: segments are scannable at a glance.

## Don't

- ❌ Don't use Segment Control for more than 4 segments — readability collapses. Use [[Select]] + [[Menu]] for 5+ options.
- ❌ Don't use Segment Control for binary on/off — use [[Toggle]].
- ❌ Don't mix Tab Item Role colors (Pickup, Deliver, Complete) with generic segments — pick one taxonomy.

---

Back to [[Design System]] · [[Component Status]].
