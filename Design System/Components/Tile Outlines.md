# Tile Outlines

Five rectangular vehicle outline tiles (Tile1 through Tile5) used inside the damage / inspection workflows as compact, equal-size canvases for grouped damage markers. Each tile contains a different vehicle perspective.

For full-vehicle BOL outlines, use [[BOL Sets]]. For damage pins on outlines, use [[Damage-Marker]].

- **Component set node:** `1487:67`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=1487-67)
- **Figma section:** `----- Damages` → "Tile Outlines"
- **Figma documentation:** Section `1756:8670` "Tile Outlines — Documentation" on the same page

---

## Composition

`Tile=Tile5` — bordered rectangle containing a vehicle outline vector group.

| Layer | Bindings |
|---|---|
| Container (FRAME) | fill `Background/Primary` · stroke `Width/XS` · `Border/Primary` |
| Outline vectors (VECTOR × N) | `Icon/Primary` |

---

## Variants — `Tile`

| Tile | Use for |
|---|---|
| `Tile1` … `Tile5` | Each tile represents a different vehicle perspective (front, rear, sides, top) — composed into a grid for inspection workflows |

---

## Instance properties

None — the variant choice is the only property.

---

## Do

- ✅ Use Tile Outlines when the inspection workflow needs equal-size tiles for grouped damage placement.
- ✅ Compose multiple tiles side-by-side or in a grid to cover all vehicle angles.
- ✅ Overlay [[Damage-Marker]] instances onto each tile to record location-specific damages.

## Don't

- ❌ Don't use Tile Outlines for full-vehicle silhouettes — use [[BOL Sets]] for the larger canvas.
- ❌ Don't substitute generic photos — these tiles are tuned for the inspection grid layout.
- ❌ Don't use Tile Outlines outside damage / inspection contexts.

---

Back to [[Design System]] · [[Component Status]].
