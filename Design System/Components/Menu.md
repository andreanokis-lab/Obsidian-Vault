# Menu

Vertical container of up to 12 [[Menu Item]] rows + 1 destructive item — appears on tapping a [[Select]] or as a contextual popover anchored to a control. Items are toggleable via `Show Item N` instance properties.

- **Component node:** `937:4113`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=937-4113)
- **Figma section:** `----- Select + Dropdown` → "Menu"
- **Figma documentation:** Section `1745:7656` "Menu — Documentation" on the same page

---

## Composition

Vertical stack of [[Menu Item]] rows inside a rounded container.

| Layer | Bindings |
|---|---|
| Menu (FRAME) | radius `Radius/M` (12) on all four corners |
| Row 1…N (Menu Item instances) | each: fill `Background/Subtle` · `Width/XS` bottom stroke · `Border/Primary` · padding `Space/L` horizontal · `Form/Label/*` text style |

The visual flow: stacked rows where each row is a Menu Item instance. Dividers between rows come from each item's bottom stroke; the last visible item should have `Stroke=None` to avoid a stray line at the menu edge.

---

## Variants

None — single component.

---

## Instance properties

13 BOOLEAN toggles — show/hide each row:

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Show Item 1` … `Show Item 12` | BOOLEAN × 12 | true | Toggle visibility of each menu row |
| `Show Destructive` | BOOLEAN | true | Toggle the destructive item at the end of the menu |

Override each visible row's inner `Label Text` / `Symbol` through the row's nested [[Menu Item]] instance.

---

## Do

- ✅ Use Menu when a [[Select]] or a more / overflow button opens a list of options.
- ✅ Show only the items relevant to the current context — hide the rest via `Show Item N=false`.
- ✅ Keep menus short — Apple HIG recommends 5–7 options for scannability. The 12-item ceiling is for edge cases.
- ✅ Use the Destructive item at the end of the menu and only when a destructive action is contextually available.
- ✅ Override the last visible row's `Stroke=None` to remove the trailing divider line.

## Don't

- ❌ Don't use Menu for navigation between screens — use a sheet, tab bar, or list row with chevron.
- ❌ Don't fill all 12 slots just because they exist — fewer choices = better usability.
- ❌ Don't put multi-line content in menu items — Menu Items are sized for single labels.
- ❌ Don't anchor the Menu to nothing — every menu should have a clear trigger ([[Select]], an icon button, a long-press target).

---

Back to [[Design System]] · [[Component Status]].
