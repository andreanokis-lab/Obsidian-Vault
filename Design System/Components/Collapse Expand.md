# Collapse / Expand

Header row with a label and an expand/collapse chevron — used to toggle the visibility of a section below. Two detent variants distinguish whether the header sits at full section level or nested inside another section.

- **Component set node:** `1410:2236`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=1410-2236)
- **Figma section:** `----- Heading + Expanding/Collapsing` → "Collapse/Expand"
- **Figma documentation:** Section `1748:7780` "Collapse / Expand — Documentation" on the same page

---

## Composition

`Detent=Full Detent` — horizontal row with leading glyph + label + trailing chevron.

| Layer | Bindings |
|---|---|
| Container (FRAME) | gap `Space/2XL` |
| Leading glyph (TEXT) | `Text/Secondary/*` (15pt, SF Pro Text) · `Text/Primary` |
| Label (TEXT) | `List/Title/*` (17pt) · `Text/Primary` |
| Trailing chevron (TEXT/glyph) | `List/Title/*` · `Text/Primary` |

---

## Variants — `Detent`

| Detent | Use for |
|---|---|
| `Full Detent` | Top-level section header (e.g., page section) |
| `In Section` | Nested expandable group inside an already-open section |

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Label` | TEXT | "Label" | Section title text |
| `Leading` | TEXT | "+" glyph | Leading symbol (e.g., add / status glyph) |
| `Trailing` | TEXT | chevron | Trailing chevron glyph (up / down) |
| `Show Trailing` | BOOLEAN | true | Toggle the trailing chevron |

---

## Do

- ✅ Use Collapse/Expand for sections that toggle to reveal/hide content.
- ✅ Swap the `Trailing` glyph based on state — chevron-down when collapsed, chevron-up when expanded.
- ✅ Use `Full Detent` for top-level page headers; `In Section` for nested expandable groups.
- ✅ Keep the Label short — section headers are scannable, not paragraphs.

## Don't

- ❌ Don't use Collapse/Expand for navigation between screens — use a list row with a trailing chevron.
- ❌ Don't hide the trailing chevron unless the section has no expand/collapse behavior — without it the affordance is unclear.
- ❌ Don't put more than one Collapse/Expand at the same detent level next to each other without a divider.

---

Back to [[Design System]] · [[Component Status]].
