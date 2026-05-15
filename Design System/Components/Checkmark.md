# Checkmark

Radio indicator for single selection within a group. Pick exactly one option. Used for picking from a list of mutually exclusive choices (mode, language, sort order, etc.).

For multi-select where multiple options can be chosen, use [[Checkbox]] instead.

- **Component set node:** `260:1772`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=260-1772)
- **Figma section:** `----- Forms`
- **Figma documentation:** Section `1720:5071` "Checkmark — Documentation" on the same page

---

## Composition

`State=Selected` — horizontal stack of indicator + label.

| Layer | Bindings |
|---|---|
| Container (FRAME) | itemSpacing `Space/M` (12pt) |
| Indicator (VECTOR) | fill `Icon/Blue` when Selected; outline only when Unselected |
| Label (TEXT) | font `Text/Body/*` (Body 17pt) · fill `Text/Secondary` |

---

## Variants — `State`

| State | Indicator | Label fill | Use for |
|---|---|---|---|
| `Unselected` | Empty outline | `Text/Secondary` | Option available but not chosen |
| `Selected` | Filled `Icon/Blue` checkmark | `Text/Secondary` | Currently chosen option |
| `Disabled` | Muted | `Text/Disabled` | Option not available in current context |

Only one Checkmark in a group should be `Selected` at a time.

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Label` | TEXT | "Label" | Label string next to the indicator |
| `Show Text` | BOOLEAN | true | Toggle label visibility |

---

## Do

- ✅ Use Checkmark for single-select choices where only one option can be active.
- ✅ Ensure exactly one option is `Selected` when the user opens the group — default to a sensible value, never "all unselected".
- ✅ Stack multiple Checkmarks vertically with `Space/M` gap between rows.
- ✅ Always show the `Label` unless the meaning is obvious from a nearby image.

## Don't

- ❌ Don't use Checkmark for multi-select — use [[Checkbox]] (square) instead.
- ❌ Don't allow zero selections — single-select means *one* must always be active.
- ❌ Don't mix Checkbox and Checkmark in the same group — pick one paradigm.

---

Back to [[Design System]] · [[Component Status]].
