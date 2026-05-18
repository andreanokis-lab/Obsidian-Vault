# List

Generic list row — leading icon, [[Row Text]] block, optional progress bar, divider, and trailing slot. Used for simple ordered or unordered list items where the row has a single tap target. For domain-specific rows (Receipts, Trackshop) use [[Content Row]] instead.

- **Component set node:** `944:4339`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=944-4339)
- **Figma section:** `----- Content Row` → "List"
- **Figma documentation:** Section `1730:6350` "List — Documentation" on the same page

---

## Composition

`View=List` — horizontal row with optional progress bar + divider below.

| Layer | Bindings |
|---|---|
| Container (FRAME) | fill `Background/Primary` · padding `Space/S` × `Space/Zero` · gap `Space/S` · `Width/XS` bottom stroke |
| Leading icon (VECTOR) | `Icon/Primary` |
| [[Row Text]] (instance) | primary `Text/Primary` (Body 17pt) + helper `Text/Tertiary` (Caption 12pt) |
| Trailing (SLOT) | swap any Trailing variant — Picker, Toggle, Segment, Trailing-Icon, Count |
| Progress Bar (optional) | track `Background/Subtle`, filled `Background/Primary Blue` |
| Divider (Line) | `Width/XS` stroke · `Border/Primary` |

---

## Variants — `View`

| View | Use for |
|---|---|
| `List` | Default — single row of list content |
| `Preview Row` | List item with a preview thumbnail / extended content area |

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Progress` | BOOLEAN | true | Toggle the progress bar |
| `Show Divider` | BOOLEAN | true | Toggle the bottom divider |
| `Trailing` | SLOT | — | Swap any [[Trailing (Content Row)]] variant |

The Row Text label, helper, and icon are nested-instance properties — override them through the [[Row Text]] sub-instance.

---

## Do

- ✅ Use List for generic settings rows, item lists, simple data tables.
- ✅ Bind the Trailing slot to the right affordance: Toggle for settings, Picker for values, Trailing-Icon (chevron) for navigation.
- ✅ Keep Show Divider on between rows in the same group; hide it on the last row before a section break.
- ✅ Show Progress only on rows with progress semantics (upload, download, multi-step completion).

## Don't

- ❌ Don't use List for domain-specific rows that have their own variant in [[Content Row]] (Receipts, Trackshop, etc.).
- ❌ Don't combine the Progress bar with a Trailing-Count — confusing affordance pairing.
- ❌ Don't stack two Trailing slots in the row.

---

Back to [[Design System]] · [[Component Status]].
