# Row Text

Two-line text block used inside list rows — a primary label + optional helper line. Used inside [[Content Row]], [[Sidebar]], and other row-based components.

- **Component set node:** `448:2970`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=448-2970)
- **Figma section:** `----- Content Row` → "Row Text"
- **Figma documentation:** Section `1729:5970` "Row Text — Documentation" on the same page

---

## Composition

`Tone=Default` — horizontal stack: leading icon + text column.

| Layer | Bindings |
|---|---|
| Container (FRAME) | itemSpacing `Space/S` (8) · horizontal layout |
| Leading icon (24×24, optional) | `Icon/Primary` |
| Text column (FRAME) | itemSpacing `Space/Zero` (vertical stack) |
| ↳ Row Text (TEXT) | font `Text/Body/*` (17pt Regular) · fill `Text/Primary` |
| ↳ Helper Text (TEXT, optional) | font `Meta/Caption/*` (12pt) · fill `Text/Tertiary` |

---

## Variants — `Tone`

| Tone | Use for |
|---|---|
| `Default` | Standard row text — neutral primary label |
| `Destructive` | Row representing a destructive action (e.g., "Delete account") — primary text turns red |

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Row Text` | TEXT | "Row Text" | Primary label string |
| `Helper Text` | TEXT | "Helper Text" | Secondary helper line |
| `Show Helper` | BOOLEAN | true | Toggle the helper line |
| `Show Leading Icon` | BOOLEAN | true | Toggle the leading icon |

---

## Do

- ✅ Use `Default` for most list-row labels.
- ✅ Use `Destructive` only for rows that lead to a destructive action (Delete, Remove, Sign out).
- ✅ Hide `Show Helper` when the row only needs a single label — the helper slot defaults to visible.
- ✅ Keep the leading icon (24×24) bound to a semantic icon that clarifies the row's purpose.

## Don't

- ❌ Don't use Row Text outside a row context — it's a composition piece, not a standalone block.
- ❌ Don't put longer paragraphs into Row Text — single-line labels only. For paragraph content, use a [[Card]] or Section Header.
- ❌ Don't bind primary text to anything other than `Text/Primary` (or `Text/Negative` for Destructive) — the row label is the visual anchor of every row.

---

Back to [[Design System]] · [[Component Status]].
