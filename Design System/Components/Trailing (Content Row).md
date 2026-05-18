# Trailing (Content Row)

Trailing slot for [[Content Row]] — fills the right edge of a row with one of five common affordances: date picker, toggle, segment, plain trailing icon, or numeric counter.

Note: four different components share the name "Trailing" across the UIKit. This one belongs to Content Row. The others are documented separately ([[Trailing (Action Section)]], [[Trailing (Sheets)]], [[Trailing (Image Content)]]).

- **Component set node:** `416:222`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=416-222)
- **Figma section:** `----- Content Row` → "Trailing"

---

## Variants — `Type`

| Type | What it shows | Use for |
|---|---|---|
| `Picker` | Pill with `Background/Subtle` + blue `Text/Link` date text | Date / time pickers — tap opens a sheet picker |
| `Toggle` | Green/gray iOS switch ([[Toggle]] instance) | Row controlling an on/off setting |
| `Segment` | Compact Yes/No segment ([[Tab Item]] pair) | Row offering a binary choice without leaving |
| `Trailing-Icon` | Single icon (e.g., chevron, more dots) | Row that navigates / has a single trailing action |
| `Count` | Counter component | Row controlling a numeric value inline |

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Icon` | INSTANCE_SWAP | default icon | Swap the trailing icon (Trailing-Icon type) |

---

## Do

- ✅ Pick the Type that matches the row's primary affordance. One affordance per row.
- ✅ Use `Picker` for tappable values (dates, times, multi-option selects that open in a sheet).
- ✅ Use `Toggle` for instant on/off settings.
- ✅ Use `Trailing-Icon` with a chevron for rows that navigate to a detail screen.

## Don't

- ❌ Don't combine two Trailing types in one row — pick one affordance per row.
- ❌ Don't use `Count` for values that aren't bounded integers — use a Picker that opens a numeric input instead.
- ❌ Don't use `Picker` for fixed read-only display — it implies the value is tappable.

---

Back to [[Design System]] · [[Component Status]].
