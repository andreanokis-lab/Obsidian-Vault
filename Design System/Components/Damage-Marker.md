# Damage-Marker

24 × 24 pill containing a single letter that points to a damage observation on a vehicle outline. Color encodes who recorded the damage — yellow for Driver, red for Customer.

- **Component set node:** `608:162`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=608-162)
- **Figma section:** `----- Damages`
- **Figma documentation:** Section `1724:5581` "Damage-Marker — Documentation" on the same page

---

## Composition

`Marker=Driver` — capsule with a single-letter glyph.

| Layer | Bindings |
|---|---|
| Badge (FRAME) | fill `Background/Primary Yellow` (Driver) / `Background/Primary Red` (Customer) · radius `Radius/Pill` · padding `Space/S` × `Space/XS` · gap `Space/S` |
| Letter (TEXT) | font `Text/Footnote/*` (13pt) · fill is mode-static (dark on Driver yellow, light on Customer red) for AA contrast |

24 × 24 dimensions — designed to sit atop a vehicle outline.

---

## Variants — `Marker`

| Marker | Container fill | Use for |
|---|---|---|
| `Driver` | `Background/Primary Yellow` | Damage spotted / recorded by the driver |
| `Customer` | `Background/Primary Red` | Damage spotted / recorded by the customer |

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Letter` | TEXT | "S" | Single-letter glyph (S/M/L/X for severity, or numeric for sequence — pick a convention per use case) |

---

## Do

- ✅ Use `Driver` (yellow) for any damage the driver records — pickup inspections, in-trip incidents.
- ✅ Use `Customer` (red) for damages the customer reports.
- ✅ Place on the appropriate spot of the vehicle outline (BOL Sets, suv.front/back/etc.).
- ✅ Keep the `Letter` to 1 character. The pill is sized for a single glyph.

## Don't

- ❌ Don't swap the Marker colors — Yellow = Driver, Red = Customer is fixed across the Driver App.
- ❌ Don't use Damage-Marker outside vehicle-outline contexts — it carries domain semantics.
- ❌ Don't put 2+ characters in the `Letter` field — it overflows the pill.

---

Back to [[Design System]] · [[Component Status]].
