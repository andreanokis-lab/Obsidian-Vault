# Damages

Rounded chip showing a damage entry — label + colored badge encoding who recorded it (Driver yellow, Customer red). Idle state is the default placeholder; Customer/Driver states show the recorded entry with its origin badge.

For the standalone vehicle-outline pin, use [[Damage-Marker]].

- **Component set node:** `607:2217`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=607-2217)
- **Figma section:** `----- Damages` → "Damages"
- **Figma documentation:** Section `1756:8622` "Damages — Documentation" on the same page

---

## Composition

`State=Idle` — rounded rectangle with label + optional badge.

| Layer | Bindings |
|---|---|
| Container (FRAME) | radius `Radius/S` · stroke `Width/XS` · padding `Space/S` × `Space/2XS` · gap `Space/S` |
| Label (TEXT, "Damage Name") | `Text/Primary` |
| Badge (FRAME, Customer / Driver states) | fill per state (`Background/Primary Yellow` for Driver, Red for Customer) · `Radius/Pill` · padding `Space/S` × `Space/XS` |
| Badge letter (TEXT) | `Text/Footnote/*` · mode-static fill for AA contrast on the badge color |

---

## Variants — `State`

| State | Use for |
|---|---|
| `Idle` | Empty damage slot — waiting for an entry |
| `Driver` | Damage recorded by the driver — yellow origin badge |
| `Customer` | Damage recorded by the customer — red origin badge |

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Label` | TEXT | "Damage\nName" | Damage description / label text |

---

## Do

- ✅ Use `Idle` for empty damage rows before any entry is recorded.
- ✅ Use `Driver` when the driver records the damage during pickup / in-trip inspection.
- ✅ Use `Customer` when the customer reports the damage.
- ✅ Keep the Label short (2–3 words). The chip is sized for compact descriptions.

## Don't

- ❌ Don't swap the colors — Yellow = Driver, Red = Customer is fixed across the app.
- ❌ Don't use Damages outside damage / inspection contexts — it carries domain semantics.
- ❌ Don't stuff a paragraph into Label — for detail, link to a damage detail screen.

---

Back to [[Design System]] · [[Component Status]].
