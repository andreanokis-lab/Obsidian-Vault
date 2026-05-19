# List Column Header

Compact three-column header row — small uppercase labels (UNIT · MAKE · MODEL) sitting above a tabular list. Used for vehicle inventories, data tables, and column-aligned content where each row maps to the same three fields.

- **Component node:** `1324:3`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=1324-3)
- **Figma section:** `----- Heading + Expanding/Collapsing` → "List Column Header / 3 columns"
- **Figma documentation:** Section `1748:7819` "List Column Header — Documentation" on the same page

---

## Composition

Horizontal row with three column labels.

| Layer | Bindings |
|---|---|
| Container (FRAME) | column alignment for 3 labels |
| Column label × 3 (UNIT · MAKE · MODEL) | `Text/Footnote/*` (13pt) · `Text/Tertiary` |

---

## Variants

None — single component sized for 3 columns.

---

## Instance properties

None — labels are overridden directly on each column TEXT layer.

---

## Do

- ✅ Use List Column Header above a tabular list where each row has the same 3 fields.
- ✅ Keep the column labels short and uppercase (UNIT · MAKE · MODEL · STATUS · etc.).
- ✅ Match the column alignment of the rows below — labels should sit above their respective columns.
- ✅ Use this with vehicle inventories, data tables, and other 3-field repeating row layouts.

## Don't

- ❌ Don't use List Column Header for layouts that aren't 3-column. For 2 or 4+ columns, build a custom header or detach + restructure.
- ❌ Don't use sentence-case labels — uppercase is the established header convention.
- ❌ Don't use this for hierarchical sections — use [[Collapse Expand]] instead.

---

Back to [[Design System]] · [[Component Status]].
