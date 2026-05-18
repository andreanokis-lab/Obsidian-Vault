# View

Payment / amount display block — large primary amount + supporting label, optionally with a "Collected Amount" detail row. Used in invoices, deposit slips, payment confirmations, and trip-amount summaries.

- **Component set node:** `389:2245`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=389-2245)
- **Figma section:** `----- Card` → "View"

---

## Composition

`View=Extended` — vertical stack with parent amount, breakdown items, and collected amount.

| Layer | Bindings |
|---|---|
| Container (FRAME) | gap `Space/XS` |
| Parent Amount (TEXT) | `Form/Input/*` (17pt) · `Text/Primary` |
| Item label (TEXT, e.g. "Additional items - charge delivery") | `Text/Secondary/*` (15pt, SF Pro Text) · `Text/Tertiary` |
| Item amount (TEXT, e.g. "$200.00") | `Text/Secondary/*` (15pt) · `Text/Positive` (green) |
| Collected Amount (TEXT, "$1,700.00") | `Form/Input/*` (17pt) · `Text/Primary` |

---

## Variants — `View`

| View | Use for |
|---|---|
| `Basic` | Single amount display — primary value only |
| `Extended` | Primary amount + itemised breakdown + collected total |

---

## Instance properties

The visible amounts and labels are inner text instances — override by selecting the text layer and editing its content directly, or wire to data per consumer.

---

## Do

- ✅ Use `Basic` for simple amount displays (one total).
- ✅ Use `Extended` when the amount has a breakdown (subtotal + add-ons + total).
- ✅ Place View inside a [[Card Base]] or [[Card]] for consistent surface treatment.
- ✅ Use `Text/Positive` (green) for amounts that are added / collected; keep `Text/Primary` for neutral totals.

## Don't

- ❌ Don't use View for non-amount content — it's tuned for monetary / numeric displays.
- ❌ Don't mix currency symbols within one View — pick one format per instance.
- ❌ Don't manually change the amount text style — use the variant's bound `Form/Input` / `Text/Secondary` style.

---

Back to [[Design System]] · [[Component Status]].
