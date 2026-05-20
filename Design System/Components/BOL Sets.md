# BOL Sets

Vehicle outline sprites used for Bill of Lading inspections — full-vehicle silhouettes that drivers annotate with [[Damage-Marker]] pins to record damage location. Two variants cover the two vehicle classes the app supports.

- **Component set node:** `1581:725`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=1581-725)
- **Figma section:** `----- Outlines` → "BOL Sets"
- **Figma documentation:** Section `1756:8549` "BOL Sets — Documentation" on the same page

---

## Composition

`Type=Vehicle Set` — a group of vector outlines showing the vehicle from multiple angles (front, back, sides, top).

| Layer | Bindings |
|---|---|
| Container (FRAME) | gap `Space/L` between outline tiles |
| Vector × N (outline strokes) | `Icon/Primary` |

The outlines are static SVG-style art — drivers tap on them at the consumer level to place [[Damage-Marker]] instances.

---

## Variants — `Type`

| Type | Use for |
|---|---|
| `Vehicle Set` | Standard 4-wheel vehicle outlines (cars, SUVs, trucks) — used on most BOL inspections |
| `Motorcycle-Set` | Motorcycle outlines — used for motorcycle BOL inspections |

---

## Instance properties

None — the variant choice is the only property. Damage placement happens at the consumer / screen level by overlaying [[Damage-Marker]] instances.

---

## Do

- ✅ Use `Vehicle Set` for cars, SUVs, trucks, and any 4-wheel vehicle.
- ✅ Use `Motorcycle-Set` specifically for motorcycle inspections — the outlines are oriented and proportioned differently.
- ✅ Overlay [[Damage-Marker]] (Driver yellow / Customer red) on the outlines to record damage locations.
- ✅ Keep the BOL Set as a background — damages should sit on top, not replace the outline.

## Don't

- ❌ Don't use BOL Sets outside vehicle-inspection / Bill of Lading contexts — they carry domain meaning.
- ❌ Don't substitute generic vehicle imagery — these outlines are tuned for inspection placement.
- ❌ Don't edit the vector strokes — the silhouette is the established BOL inspection canvas.

---

Back to [[Design System]] · [[Component Status]].
