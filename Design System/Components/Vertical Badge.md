# Vertical Badge

Narrow, tall colored pill containing a map-pin icon and a count number. Used as a stop / waypoint marker on route or trip detail views — typically Green for pickup and Red for delivery.

- **Component set node:** `387:441`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=387-441)
- **Figma section:** `----- Card`
- **Figma documentation:** Section `1718:4921` "Vertical Badge — Documentation" on the same page

---

## Composition

`State=Green` (`387:440`) — vertical stack inside a tall narrow pill.

| Layer | Bindings |
|---|---|
| Badge (FRAME) | fill `Background/Primary Green` (or Red per State) · padding 10/10/10/10 |
| ↳ Map pin icon (21×21) | `Icon/Inverse Static` (white on dark fill) |
| ↳ Count number (TEXT) | `Text/Body/*` (17pt Regular) · fill `Text/Primary Inverse Static` |

Dimensions: 25 × 92 — narrow column, much taller than wide. Designed to sit inline with a route list or attach to a stop on a map.

---

## Variants — `State`

| State | Container fill | Use for |
|---|---|---|
| `Green` | `Background/Primary Green` | Pickup stop marker |
| `Red` | `Background/Primary Red` | Delivery / drop-off stop marker |

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `#` | TEXT | "0" | Stop number (1, 2, 3, ...) |

---

## Do

- ✅ Use `Green` for pickup stops, `Red` for delivery stops — follows the established colour convention across the Driver App.
- ✅ Place inline with the stop list or anchored to the relevant point on a map / route diagram.
- ✅ Keep the count number to 1–2 digits — the narrow column won't fit more.

## Don't

- ❌ Don't use Vertical Badge outside of stop / waypoint contexts — it carries domain semantics (pickup/delivery). For generic colored counters, use [[Badge]] with `Role=Count Badge`.
- ❌ Don't swap the State colors. Green ≠ delivery, Red ≠ pickup — the convention is fixed.
- ❌ Don't overlay this on an arbitrary surface — the icon uses `Icon/Inverse Static` (always-white) which only reads on the Green/Red fills.

---

Back to [[Design System]] · [[Component Status]].
