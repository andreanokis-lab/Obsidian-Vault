# List / Grid

Card-style grid tile — image + title + helper text + progress bar — designed for grid layouts (2-up, 3-up) where each cell needs visual weight and a thumbnail. Distinct from [[List]] (horizontal row) and [[Content Row]] (domain-specific row).

- **Component node:** `939:4248`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=939-4248)
- **Figma section:** `----- Content Row` → "List/Grid"

---

## Composition

Vertical card with image on top, text below, optional progress bar.

| Layer | Bindings |
|---|---|
| Image (FRAME) | `Radius/S` · `Background/Subtle` (image fill or placeholder) |
| Progress Bar (optional) | track `Background/Subtle` · filled `Background/Primary Blue` |
| Content (FRAME) | fill `Background/Subtle` · padding `Space/XS` × `Space/S` · gap `Space/S` · bottom corners `Radius/M` |
| ↳ Short Title (TEXT) | `Text/Secondary/*` (15pt, SF Pro Text) · `Text/Primary` |
| ↳ Helper Label (TEXT) | `Meta/Caption/*` (12pt) · `Text/Tertiary` |
| Trailing (SLOT) | swap any [[Trailing (Content Row)]] variant |

---

## Variants

None — single component.

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Short Title...` | TEXT | "Short Title is Best here..." | Card title |
| `Helper` | TEXT | "Helper Label" | Secondary caption |
| `Action/Placeholder` | BOOLEAN | false | Show as action/placeholder card (e.g., "+ Add new") |
| `Show Progress Bar` | BOOLEAN | true | Toggle the progress bar |
| `Show Divider` | BOOLEAN | true | Toggle the divider line |
| `Progress` | BOOLEAN | true | Toggle the progress indicator |
| `Trailing` | SLOT | — | Swap any Trailing variant |

---

## Do

- ✅ Use List/Grid for image-led grid layouts (photo galleries, document grids, vehicle tiles).
- ✅ Pair `Show Progress Bar=true` with content that has measurable progress (uploads, downloads, multi-step capture).
- ✅ Use `Action/Placeholder=true` for "Add new" cells that sit alongside content cells.
- ✅ Keep the Helper label short — the card is narrow.

## Don't

- ❌ Don't use List/Grid for text-only rows — use [[List]] or [[Content Row]] instead.
- ❌ Don't stack multiple Trailing variants — pick one affordance per card.
- ❌ Don't override the title font to use SF Pro Display — at 15pt it should stay SF Pro Text per HIG.

---

Back to [[Design System]] · [[Component Status]].
