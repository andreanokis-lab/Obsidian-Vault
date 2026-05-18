# Info row

Compact horizontal label with leading + trailing icons. Used for inline data display — phone numbers, IDs, contact details, status pairs. Typically appears inside a [[Card]] or details panel.

- **Component node:** `342:4031`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=342-4031)
- **Figma section:** `----- Card` → "Info row"

---

## Composition

161 × 20 horizontal row.

| Layer | Bindings |
|---|---|
| Container (FRAME) | gap `Space/S` |
| Leading icon (VECTOR, optional) | `Icon/Primary` |
| Label (TEXT) | `Text/Secondary/*` (15pt, SF Pro Text) · `Text/Secondary` |
| Trailing icon (VECTOR, optional) | `Icon/Primary` |

---

## Variants

None — single component.

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Label` | TEXT | "000-000-0000" | Visible label (e.g., phone number, ID) |
| `Swap Icon` | INSTANCE_SWAP | default chevron | Trailing icon |
| `Leading Icon` | BOOLEAN | true | Toggle the leading icon |
| `Trailing Icon` | BOOLEAN | true | Toggle the trailing icon |

---

## Do

- ✅ Use Info row for inline data display inside a [[Card]] or details list.
- ✅ Bind the leading icon to clarify the content type (phone, email, ID, calendar).
- ✅ Use the trailing icon for navigation or copy/dial affordance (chevron, copy icon).
- ✅ Keep the Label short — the row is sized for compact inline data (~25 characters).

## Don't

- ❌ Don't use Info row for long-form content — use a [[Content Row]] or [[Row Text]] instead.
- ❌ Don't stack multiple Info rows without a divider — they'll visually run together.
- ❌ Don't hide both Leading and Trailing icons — the row reads as plain text without affordance.

---

Back to [[Design System]] · [[Component Status]].
