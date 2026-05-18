# Card Base

Empty card surface — `Background/Subtle` fill, `Radius/L` corners, `Space/L` padding. The foundation that [[Card]] and other compositions build on top of. Use directly when you need a generic card container without preset fields.

- **Component node:** `339:2467`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=339-2467)
- **Figma section:** `----- Card` → "Card Base"
- **Figma documentation:** Section `1737:6873` "Card Base — Documentation" on the same page

---

## Composition

Single FRAME with one slot for inner content.

| Layer | Bindings |
|---|---|
| Card Base (FRAME) | fill `Background/Subtle` · radius `Radius/L` (16) · padding `Space/L` all sides · gap `Space/XS` |
| Slot | swap-in zone for content (any nested instance or layout) |

---

## Variants

None — single component.

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Slot` | SLOT | — | Inner content of the card |

---

## Do

- ✅ Use Card Base when you need a card surface and the prebuilt [[Card]] variants don't match your data shape.
- ✅ Compose by swapping the Slot for any content layout — rows, forms, charts, custom layouts.
- ✅ Keep the padding (`Space/L`) — it's the standard card inset across the system.

## Don't

- ❌ Don't use Card Base when a [[Card]] variant already exists for the domain (Company, Invoices, etc.) — use the variant.
- ❌ Don't override the corner radius — `Radius/L` is the system standard for cards.
- ❌ Don't use Card Base as a screen background — for full-screen surfaces use `Background/Primary` directly.

---

Back to [[Design System]] · [[Component Status]].
