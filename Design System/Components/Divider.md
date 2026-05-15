# Divider

Horizontal or vertical hairline used to separate list rows, content sections, or columns. One of the most-used atoms in the system.

- **Component set node:** `292:133`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=292-133)
- **Figma section:** `----- Divider` → "Divider"
- **Figma documentation:** Section `1716:4620` "Divider — Documentation" on the same page

---

## Composition

`Type=Horizontal` — a single LINE element.

| Layer | Bindings |
|---|---|
| Line 1 (LINE) | strokeWeight `Width/XS` (1pt) · stroke color `Border/Primary` |

No padding, no container — the divider is the line itself.

---

## Variants — `Type`

| Type | Use for |
|---|---|
| `Horizontal` | Default direction. Separates rows in lists, sections in scrolling content, items in a vertical stack |
| `Vertical` | Separates columns or inline groups in a horizontal layout. Used rarely (~3% of dividers in production) |

---

## Instance properties

None. The divider has no exposed instance properties — its width/height is driven by parent auto-layout constraints. Resize the instance to span the parent.

---

## Do

- ✅ Use `Horizontal` for list row separators, section breaks in vertical content, and between stacked groups.
- ✅ Use `Vertical` when separating columns in a horizontal layout — e.g. a stats row "Trips | Vehicles | Score" with two verticals between the three values.
- ✅ Resize the instance to fill its parent — divider does not auto-fit on its own. Use auto-layout with `Fill container` on the divider's primary axis.

## Don't

- ❌ Don't use Divider when whitespace between sections already creates separation. Stacked dividers + large gaps double up the visual break.
- ❌ Don't increase the stroke weight manually — the system has one divider weight (Width/XS). For a heavier separator, use a colored background row or a card boundary instead.
- ❌ Don't use Divider to imply hierarchy. A divider is a hairline; for "this section is different", use a `Section/Title` header or background color shift.

---

Back to [[Design System]] · [[Component Status]].
