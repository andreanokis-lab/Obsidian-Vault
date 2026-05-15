# Image

Square or circular image container — used for avatars, photo thumbnails, driver photos, vehicle photos. Shows the bound image or a placeholder icon when empty.

- **Component set node:** `449:2627`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=449-2627)
- **Figma section:** `----- Image Content`
- **Figma documentation:** Section `1724:5648` "Image — Documentation" on the same page

---

## Composition

`Size=S, Format=Square` — frame containing an image fill or placeholder icon.

| Layer | Bindings |
|---|---|
| Container (FRAME) | fill `Background/Subtle` · radius `Radius/S` (Square) or full pill (Circle) |
| Placeholder icon (VECTOR) | `Icon/Disabled` (shown when no image bound) |

---

## Variants

| Axis | Values | Notes |
|---|---|---|
| `Size` | `S` (56) · `M` (88) · `L` (112) | Square dimensions |
| `Format` | `Square` · `Circle` | Square uses `Radius/S`; Circle is fully rounded |

6 variants total (3 × 2).

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Icon` | INSTANCE_SWAP | default icon | Placeholder glyph shown when no image is set |
| `Placeholder` | BOOLEAN | false | Toggle the placeholder icon visibility |

---

## Do

- ✅ Use `Circle` for avatars, profile photos, driver portraits.
- ✅ Use `Square` (with `Radius/S` corners) for photo thumbnails, vehicle photos, receipt thumbnails.
- ✅ Match `Size` to context: S (56) for inline list rows, M (88) for cards, L (112) for hero / detail screens.
- ✅ Show the `Placeholder` icon when no image is loaded yet — better than an empty container.

## Don't

- ❌ Don't use Image for icons — use the `Icons/*` set or a sized SVG instead.
- ❌ Don't override the container size manually — use the right `Size` variant. Custom sizes break alignment.
- ❌ Don't put text inside the Image container — overlays go in a parent frame above the Image.

---

Back to [[Design System]] · [[Component Status]].
