# Title and Controls

Sheet header bar — title in the middle, optional [[Leading (Sheets)]] and [[Trailing (Sheets)]] pill buttons on either side. Used at the top of every Sheet to anchor the title and provide cancel/back/done affordances.

- **Component node:** `442:9262`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=442-9262)
- **Figma section:** `----- Sheets` → "Title and Controls"
- **Figma documentation:** Section `1756:8495` "Title and Controls — Documentation" on the same page

---

## Composition

Horizontal row: leading slot + title + trailing slot.

| Layer | Bindings |
|---|---|
| Container (FRAME) | padding `Space/L` left/right · `Space/Zero` top/bottom |
| Title (TEXT) | `Screen/Title/*` (Headline 17pt Semibold) · `Text/Primary` |
| Leading button (pill) | `Radius/Pill` · padding `Space/L` × `Space/XS` · gap `Space/S` — nested [[Leading (Sheets)]] |
| Trailing button (pill) | `Radius/Pill` · padding `Space/L` × `Space/XS` · gap `Space/S` — nested [[Trailing (Sheets)]] |

---

## Variants

None — single component.

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Title` | TEXT | "Title" | Sheet title text |
| `Show Title` | BOOLEAN | true | Toggle the title visibility |
| `Show Leading` | BOOLEAN | true | Toggle the leading button slot |
| `Show Trailing` | BOOLEAN | true | Toggle the trailing button slot |

---

## Do

- ✅ Use Title and Controls at the top of every Sheet — it's the sheet's identity row.
- ✅ Show a `Title` that names the sheet's purpose in 1–3 words.
- ✅ Pair `Show Leading=true` with a Back / Close affordance; `Show Trailing=true` with a Cancel / Done / Save affordance.
- ✅ Hide either slot when no action belongs on that side — both slots are optional.

## Don't

- ❌ Don't use Title and Controls outside a Sheet header — it's specifically the Sheet's title bar.
- ❌ Don't stuff a paragraph into `Title` — sheet headers are scannable, single-line.
- ❌ Don't put primary actions in Leading — Leading is for navigation (Back / Close). Use Trailing or the Sheet body for the primary action.

---

Back to [[Design System]] · [[Component Status]].
