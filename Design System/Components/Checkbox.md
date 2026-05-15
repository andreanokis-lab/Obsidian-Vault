# Checkbox

Square check control for binary selection where multiple selections are allowed in a group. Used in multi-select lists, agreement forms, filter sets, and option groups.

For single-select (radio-style) use [[Checkmark]] instead.

- **Component set node:** `260:1717`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=260-1717)
- **Figma section:** `----- Forms`
- **Figma documentation:** Section `1720:4988` "Checkbox — Documentation" on the same page

---

## Composition

`State=Selected` — horizontal stack of check square + label.

| Layer | Bindings |
|---|---|
| Container (FRAME) | itemSpacing `Space/M` (12pt) |
| Square (VECTOR) | fill `Icon/Blue` when Selected; outline only when Unselected |
| Label (TEXT) | font `Text/Body/*` (Body 17pt) · fill `Text/Secondary` |

---

## Variants — `State`

| State | Square | Label fill | Use for |
|---|---|---|---|
| `Unselected` | Empty outline | `Text/Secondary` | Default — option available but not chosen |
| `Selected` | Filled `Icon/Blue` with check | `Text/Secondary` | Option is currently selected |
| `Disabled` | Muted | `Text/Disabled` | Option not available in current context |

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Label` | TEXT | "Label" | Label string next to the check square |
| `Show Text` | BOOLEAN | true | Toggle the label visibility (icon-only mode) |

---

## Do

- ✅ Use Checkbox for multi-select groups where any combination of options is valid.
- ✅ Use `Disabled` when an option is contextually unavailable (e.g., depends on another selection).
- ✅ Stack multiple Checkboxes vertically with `Space/M` gap between rows.
- ✅ Always show the `Label` unless the meaning is obvious from a nearby image / icon.

## Don't

- ❌ Don't use Checkbox for single-select choices — use [[Checkmark]] (radio indicator) instead.
- ❌ Don't pair Checkbox with a Toggle in the same group — pick one selection paradigm per screen.
- ❌ Don't hide the Label without an adjacent visual context — bare check squares fail accessibility.

---

Back to [[Design System]] · [[Component Status]].
