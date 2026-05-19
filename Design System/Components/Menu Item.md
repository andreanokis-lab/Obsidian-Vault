# Menu Item

Single row inside a [[Menu]] — label + optional symbol (check, arrow, system glyph). Composed into a [[Menu]] vertically with hairline dividers between items.

- **Component set node:** `937:4085`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=937-4085)
- **Figma section:** `----- Select + Dropdown` → "Menu Item"
- **Figma documentation:** Section `1745:7593` "Menu Item — Documentation" on the same page

---

## Composition

`Type=Default, Stroke=Default` — horizontal row with label + symbol.

| Layer | Bindings |
|---|---|
| Container (FRAME) | fill `Background/Subtle` · padding `Space/L` horizontal · `Width/XS` bottom stroke · `Border/Primary` |
| Label (TEXT) | font `Form/Label/*` (Subheadline 15pt) · fill `Text/Primary` |
| Symbol (TEXT/icon) | `Icon/Primary` (default checkmark or other system glyph) |

`Type=Destructive` swaps the Label fill to `Text/Negative`.
`Stroke=None` hides the bottom divider — use for the last item in a section.

---

## Variants

| Axis | Values | Notes |
|---|---|---|
| `Type` | `Default` · `Destructive` | Destructive turns the label red — for delete / sign-out / remove |
| `Stroke` | `Default` · `None` | Controls the bottom divider; use `None` on the last row in a section |

4 combinations total.

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Label Text` | TEXT | "Label" | Visible item label |
| `Symbol` | TEXT | "􀆅" (checkmark) | Trailing symbol glyph |
| `Show Symbol` | BOOLEAN | true | Toggle the trailing symbol |

---

## Do

- ✅ Use `Type=Default` for ordinary menu choices.
- ✅ Use `Type=Destructive` only for destructive options (Delete, Remove, Sign out).
- ✅ Hide `Show Symbol` for items that don't need a trailing affordance (toggle-like states).
- ✅ Set `Stroke=None` on the last item in a section / group to avoid double-line at the menu edge.

## Don't

- ❌ Don't use Menu Item outside a [[Menu]] container — it's a row, not a standalone control.
- ❌ Don't use `Type=Destructive` for non-destructive options just to draw attention — that breaks the user's pattern-matching.
- ❌ Don't stack two Destructive items in one menu — there's usually only one destructive choice per context.

---

Back to [[Design System]] · [[Component Status]].
