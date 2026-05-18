# Leading (Sheets)

Leading pill button used in a [[Sheet]] header — typically a Back/Close action on the left side of a sheet's title bar. Mirror of [[Trailing (Sheets)]].

- **Component set node:** `442:10216`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=442-10216)
- **Figma section:** `----- Sheets` → "Leading"

---

## Composition

Pill button — `Radius/Pill`, padding `Space/L` × `Space/XS`, gap `Space/S`.

---

## Variants — `Type`

| Type | Use for |
|---|---|
| `Circle Button` | Compact icon-only back / close action (44×44 round) |
| `Text Button` | Labeled action — typically "Back" or a step indicator in a multi-step sheet |

---

## Instance properties

None at the component set level — content lives inside the nested button instance.

---

## Do

- ✅ Use `Circle Button` for icon-only navigation (back chevron) in compact sheet headers.
- ✅ Use `Text Button` for explicit "Back" / step labels in multi-step flows.
- ✅ Pair with [[Trailing (Sheets)]] and [[Title and Controls]] for a complete sheet header.

## Don't

- ❌ Don't use Leading (Sheets) outside a Sheet header.
- ❌ Don't put both Circle Button and Text Button in the same leading slot — pick one.
- ❌ Don't use Leading as a sheet's primary action — it's navigation only. Primary actions go in [[Trailing (Sheets)]] or in the sheet body.

---

Back to [[Design System]] · [[Component Status]].
