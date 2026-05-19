# Select

Tappable pill that opens a [[Menu]] or picker — shows the current selection + trailing chevron icon. Used wherever a single value is chosen from a list (sort order, filter value, status picker, mode switch).

For free-text entry use [[Input]]. For inline binary toggles use [[Toggle]].

- **Component set node:** `307:1122`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=307-1122)
- **Figma section:** `----- Select + Dropdown` → "Select"
- **Figma documentation:** Section `1745:7513` "Select — Documentation" on the same page

---

## Composition

`State=Default` — horizontal pill with label + trailing icon.

| Layer | Bindings |
|---|---|
| Container (FRAME) | fill `Background/Subtle` · radius `Radius/Pill` · padding `Space/L` × `Space/S` · height `Space/4XL` (48) |
| Label (TEXT) | font `Form/Input/*` (Body 17pt) · fill `Text/Secondary` |
| Trailing icon (VECTOR) | `Icon/Primary` — chevron / disclosure indicator |

`State=Focused` swaps the container to indicate keyboard focus or the open state.

---

## Variants — `State`

| State | Use for |
|---|---|
| `Default` | Idle / closed — shows the current selected value |
| `Focused` | Open / active — tap target currently has focus or the dropdown is showing |

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Label` | TEXT | "Label" | Current selection label |
| `Trailing Icon` | INSTANCE_SWAP | chevron-down | Swap the trailing icon (typically up/down chevron toggling with State) |

---

## Do

- ✅ Use Select when the user picks one value from a known list.
- ✅ Show the **current selection** as the Label — not "Choose…" or placeholder text.
- ✅ Pair with a [[Menu]] component to show the options after tap.
- ✅ Use `Focused` while the menu is open or the field is keyboard-focused.

## Don't

- ❌ Don't use Select for free-form text — use [[Input]].
- ❌ Don't use Select for binary on/off settings — use [[Toggle]].
- ❌ Don't leave the Label empty — show the current value or a sensible default.

---

Back to [[Design System]] · [[Component Status]].
