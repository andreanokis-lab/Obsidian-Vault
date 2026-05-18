# Trailing (Action Section)

Trailing pill button used inside an [[Action Section]] — a small inline action attached to a row header. One of three button styles: icon-only, text label, or icon-with-chevron.

Note: four different components share the name "Trailing" across the UIKit. This one belongs to Action Section. See also [[Trailing (Content Row)]], [[Trailing (Sheets)]], [[Trailing (Image Content)]].

- **Component set node:** `475:1102`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=475-1102)
- **Figma section:** `----- Action Section` → "Trailing"

---

## Composition

`Type=Icon` — horizontal pill with leading 24×24 icon.

| Layer | Bindings |
|---|---|
| Container (FRAME) | padding `Space/L` × `Space/XS` · radius `Radius/Pill` · gap `Space/S` |
| Icon (VECTOR) | `Icon/Primary` |
| Label (TEXT, Text / Icon-chevron types) | text style applied per consumer |

---

## Variants — `Type`

| Type | Composition | Use for |
|---|---|---|
| `Icon` | Single icon button (pill, 44×44 tap target) | Compact action — icon-only |
| `Text` | Label-only pill button | Action with a written verb ("Edit", "Done") |
| `Icon-chevron` | Icon + trailing chevron | Action that opens a sub-sheet or expands |

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Icon` | INSTANCE_SWAP | default icon | Swap the leading icon |
| `Label` | TEXT | "Button" | Visible label (Text type) |
| `Instance` | INSTANCE_SWAP | default chevron | Trailing chevron icon (Icon-chevron type) |

---

## Do

- ✅ Use `Icon` for compact, icon-recognisable actions (close, more, share, refresh).
- ✅ Use `Text` when the action's verb is short and the screen has the space.
- ✅ Use `Icon-chevron` when the trailing action expands or navigates to a sub-detail.

## Don't

- ❌ Don't use Trailing (Action Section) outside an Action Section header — for buttons inline with content, use [[Button]].
- ❌ Don't put more than one Trailing in a single Action Section — the section header has a single trailing slot by design.

---

Back to [[Design System]] · [[Component Status]].
