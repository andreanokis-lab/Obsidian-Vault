# Content Row

Domain-specific list row with multiple HaulEx-flavoured variants — Receipts, Trackshop, Adjustments, Truck Service, Deposit slip. Each variant includes a section header, image thumbnail, primary/secondary text, tags, and contextual fields (date, amount, mileage).

For generic list rows without HaulEx semantics, use [[List]] instead.

- **Component set node:** `1008:3542`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=1008-3542)
- **Figma section:** `----- Content Row` → "Content Row"

---

## Composition

`Variant=Receipts, Long Press=False` — vertical stack of section header + row content.

| Layer | Bindings |
|---|---|
| Container (FRAME) | fill `Background/Primary` · `Width/XS` bottom stroke · `Border/Primary` divider |
| Section header (FRAME) | fill `Background/Subtle` · padding `Space/L` × `Space/S` · gap `Space/S` |
| ↳ Section label (TEXT) | `Meta/Caption/*` (12pt) · `Text/Secondary` |
| Row content (FRAME) | padding `Space/Zero` × `Space/M` · gap `Space/M` |
| ↳ Thumbnail (Image) | `Radius/S` · `Background/Subtle` |
| ↳ Text content (FRAME) | gap `Space/2XS` |
| ↳↳ Primary text (TEXT) | `List/Title/*` (17pt) · `Text/Primary` |
| ↳↳ Secondary text (TEXT) | `Text/Secondary/*` (15pt, SF Pro Text) · `Text/Tertiary` |
| ↳ Tags stack (FRAME) | gap `Space/XS` |

---

## Variants

| Axis | Values | Default |
|---|---|---|
| `Variant` | `Receipts` · `Trackshop` · `Adj.` · `Truck Service` · `Deposit slip` | `Receipts` |
| `Long Press` | `False` · `True` | `False` |

7 built combinations (not all Variant × Long Press combinations exist).

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Section Header` | TEXT | "❖ Section Header" | Top header label |
| `Leading Row Name` | TEXT | "Short title is best here" | Primary label on the leading side |
| `Trailing Row Name` | TEXT | "Short title is best here" | Primary label on the trailing side |
| `Date` | TEXT | "􀉉 3/17/23" | Date stamp |
| `Amount` | TEXT | "$ 1,234.00" | Monetary amount |
| `Mileage` | TEXT | "􂚛 254950" | Mileage value (Truck Service / Adj. variants) |
| `Truck __Icon` | INSTANCE_SWAP | default | Truck icon (Truck Service / Adj. variants) |
| `Trailer __Icon` | INSTANCE_SWAP | default | Trailer icon (Trackshop / Trailer variants) |
| `Show Thumbnail` | BOOLEAN | true | Toggle the leading thumbnail |
| `Has Count` | BOOLEAN | true | Show count indicator |
| `Show _TrailerLine` | BOOLEAN | true | Show the trailer line indicator |
| `hasTags` | BOOLEAN | true | Toggle the tags stack |

---

## Do

- ✅ Pick the `Variant` that matches the domain — Receipts for receipt lists, Trackshop for parts, Truck Service for maintenance.
- ✅ Use `Long Press=True` to show the long-press state (selection / action) for any variant.
- ✅ Fill all relevant text properties — the row is information-dense by design.
- ✅ Use the Section Header to group rows by category (date, type, etc.).

## Don't

- ❌ Don't use Content Row for generic list rows — use [[List]].
- ❌ Don't mix variants in the same list section — pick one Variant per group.
- ❌ Don't hide both Thumbnail and Tags — the row collapses to text-only which looks broken.

---

Back to [[Design System]] · [[Component Status]].
