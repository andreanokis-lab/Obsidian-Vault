# Card

Composite card with seven domain-specific variants — Company, Invoices, Deposit Slip, Stops, Trip-Routes, Requests, Orders. Each variant lays out HaulEx-specific fields (driver, trip number, vehicle, dates, amounts) on top of a [[Card Base]] container.

For a plain card surface without any field structure, use [[Card Base]] directly.

- **Component set node:** `389:2319`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=389-2319)
- **Figma section:** `----- Card` → "Card"
- **Figma documentation:** Section `1737:7034` "Card — Documentation" on the same page

---

## Composition

`Role=Company` — vertical stack inside the [[Card Base]] surface.

| Layer | Bindings |
|---|---|
| Card Base (FRAME) | fill `Background/Subtle` · radius `Radius/L` · padding `Space/M` all sides · gap `Space/XS` |
| Slot (FRAME) | gap `Space/S` — swap-in zone for any header content (e.g., status badge row) |
| Primary text (TEXT) | `Text/Body/*` (17pt) · `Text/Primary` — main label (employee name, trip number, etc.) |
| Secondary text (TEXT) | `Text/Footnote/*` (13pt) · `Text/Primary` — role / position / context |
| Divider (Line) | `Width/XS` · `Border/Primary` |
| Info row (instance) | nested [[Info row]] — phone / contact / inline data |

Other Role variants swap the text properties and slot composition (Trip number, Mileage, Stops, etc.).

### `Role=Orders` — curb weight

The Orders variant's pickup/delivery row (`SPACE_BETWEEN` horizontal) carries a **third, centered** cluster for curb weight, matching the P/D icon+value treatment:
- Icon: `Icons/scalemass` (Size=sm) · Value: `Text/Secondary` 15pt · `Text/Tertiary` color · `Space/S` icon→value gap.
- Added `2026-07-02`. Value bound to `Curb Weight` TEXT prop; group visibility bound to `Show Weight` BOOLEAN (default on).
- Reads left→right as **pickup date · curb weight · delivery date**. The `scalemass` icon disambiguates it from the date clusters.

---

## Variants — `Role`

| Role | Use for |
|---|---|
| `Company` | Driver / company contact card — name + role + contact |
| `Invoices` | Invoice card — amount + due date + status |
| `Deposit Slip` | Deposit slip card — bank info + amount |
| `Stops` | Trip stop card — pickup / delivery info |
| `Trip-Routes` | Route card — trip number + miles + duration |
| `Requests` | Request card — submitted requests with status |
| `Orders` | Order card — order details + amount |

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Employee` | TEXT | "Full Name Employee" | Primary name |
| `Role1` | TEXT | "Role/Position" | Position / role label |
| `Name` | TEXT | "Full Name" | Driver / contact name |
| `Trip` | TEXT | "63-07-29-24 Artem Y" | Trip identifier |
| `Trip# / Route#` | TEXT | "#15-1010" | Trip or route number |
| `Trip/Day Off` | TEXT | "Day Off" | Trip name or status |
| `Car` | TEXT | "2015 Porsche Cayenne" | Vehicle string |
| `mi` | TEXT | "655 mi" | Mileage |
| `Show Contact Item` | BOOLEAN | true | Toggle the Info row |
| `INOP` | BOOLEAN | true | Show INOP (inoperable) status |
| `Payment Amount` | BOOLEAN | true | Toggle payment row |
| `Has Trip` | BOOLEAN | true | Toggle trip section |
| `Show Progress` | BOOLEAN | true | Toggle progress section |
| `Show Grabber` | BOOLEAN | true | Toggle the drag grabber |
| `Curb Weight` | TEXT | "4,398 lb" | Orders variant — curb weight value |
| `Show Weight` | BOOLEAN | true | Orders variant — toggle the curb weight group |
| `Slot`, `Slot 2`, `Slot 3` | SLOT × 3 | — | Swap-in zones for badges / status |

---

## Do

- ✅ Pick the `Role` that matches the domain — Company for driver/contact cards, Invoices for invoice rows, Stops for trip stops.
- ✅ Use the SLOT properties to attach status badges, action buttons, or other contextual content.
- ✅ Hide properties that don't apply (e.g., `Show Contact Item=false` if a Company card has no phone).
- ✅ Keep the card surface as `Background/Subtle` — that's the standard card visual against `Background/Primary` screens.

## Don't

- ❌ Don't use Card for generic content surfaces — use [[Card Base]] for an empty card.
- ❌ Don't mix Role variants in the same scrollable group — pick one Role per list section.
- ❌ Don't override the radius or padding manually — those come from `Radius/L` and `Space/M`.

---

Back to [[Design System]] · [[Component Status]].
