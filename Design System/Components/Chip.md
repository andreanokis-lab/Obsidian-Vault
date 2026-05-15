# Chip

Toggleable pill for filters, tags, or compact actions. Tap to toggle on/off (Default, Numbered types) or trigger an action (Action type). Stacked horizontally as a filter row or selection group.

- **Component set node:** `288:981`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=288-981)
- **Figma section:** `----- Forms`
- **Figma documentation:** Section `1720:5211` "Chip — Documentation" on the same page

---

## Composition

`State=On, Type=Numbered` — horizontal pill with label, count, optional helper.

| Layer | Bindings |
|---|---|
| Container (FRAME) | fill `Background/Subtle Blue` · stroke `Border/Blue` (Width/XS) · radius `Radius/M` · padding `Space/S` × `Space/M` · gap `Space/S` |
| Label (TEXT) | font `Form/Label/*` (Subheadline 15pt) · fill `Text/Primary` |
| Number (TEXT, Numbered type) | Count beside the label |
| Icon (INSTANCE_SWAP, Action type) | Leading icon |

Other Type/State combinations swap container fill, stroke, and content slots:
- `Off` states use a subtle background without the blue stroke
- `Action` type swaps the number for an icon

---

## Variants

| Axis | Values | Notes |
|---|---|---|
| `State` | `Off` · `On` | Whether the chip is selected/active |
| `Type` | `Default` · `Numbered` · `Action` | Content layout — label only, label + count, or label + icon |

6 variants total (2 × 3).

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Label` | TEXT | "Label" | Visible label string |
| `Number` | TEXT | "0" | Count number (Numbered type) |
| `Icon` | INSTANCE_SWAP | default icon | Leading icon (Action type) |
| `Helper` | BOOLEAN | true | Toggle the helper text row below |
| `Helper Text` | TEXT | " Help Text" | Helper text content |

---

## Do

- ✅ Use `Default` for plain filter / tag chips.
- ✅ Use `Numbered` for filter chips that show a count of matching items.
- ✅ Use `Action` for chips that trigger an action (with an icon affordance).
- ✅ Use `State=On` to indicate the chip is currently active / selected.
- ✅ Stack chips horizontally with `Space/S` gap for filter rows. Wrap to a second row if they overflow.

## Don't

- ❌ Don't use Chip for primary actions — it reads as a filter/tag, not a CTA. Use [[Button]].
- ❌ Don't mix `Default`, `Numbered`, and `Action` Types in the same row — pick one taxonomy per group.
- ❌ Don't enable the `Helper` slot unless the helper text adds genuine context — empty / decorative helpers add noise.

---

Back to [[Design System]] · [[Component Status]].
