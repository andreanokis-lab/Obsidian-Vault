# Button

The primary interactive control across the app — confirm/submit actions, navigation triggers, toolbar buttons, and icon-only headers. Composed of a label and up to two icons.

- **Component set node:** `246:161`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=246-161)
- **Figma section:** `----- Button` → "Button"
- **Figma documentation:** Section `1713:4245` "Button — Documentation" on the same page

---

## Composition

`Size=L, Type=Primary, State=Default, Icon Only=False, Role=Default` (`236:90`) — horizontal stack of label and up to two icons.

| Layer | Bindings |
|---|---|
| Container | height `Space/4XL` · padding `Space/XS` × `Space/L` · gap `Space/S` · radius `Radius/Pill` · fill `Background/Subtle` (per Role) |
| Leading icon (24×24) | `Icon/Primary` (per Role) |
| Label (TEXT) | `Form/Label/*` (Subheadline 15pt Regular) · `Text/Primary` (per Role) |
| Trailing icon (24×24) | `Icon/Primary` (per Role) |

Other Role and Type combinations swap the container fill, label color, and icon color. `Size=M` / `S` adjust height + padding proportionally.

---

## Variant axes

5 axes — combine to pick the right button.

| Axis | Values | Default | What it drives |
|---|---|---|---|
| `Size` | `L` · `M` · `S` | `L` | Container height + padding |
| `Type` | `Primary` · `Secondary` · `Tertiary` · `Ghost` · `Tile` | `Primary` | Visual weight + fill style |
| `State` | `Default` · `Pressed` · `Disabled` · `Outline` | `Default` | Interactive state + outline style |
| `Icon Only` | `False` · `True` | `False` | Toggles label visibility |
| `Role` | `Default` · `Link` · `Yellow` · `Green` · `Red` · `Blue` · `Inverse` · `Text` | `Inverse` | Color treatment (fill/text/icon) |

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Label` | TEXT | "Button" | Visible label string |
| `Show Leading Icon` | BOOLEAN | true | Toggles the leading 24×24 icon |
| `Leading Icon` | INSTANCE_SWAP | `Icons/circle` | Swap source for the leading icon |
| `Show Trailing Icon` | BOOLEAN | true | Toggles the trailing 24×24 icon |
| `Trailing Icon` | INSTANCE_SWAP | `Icons/circle` | Swap source for the trailing icon |
| `Icon` | INSTANCE_SWAP | `Icons/circle` | Swap source for icon-only mode |

---

## When to use

| Use case | Pick |
|---|---|
| Main screen CTA (confirm, submit) | `Size=L, Type=Primary, Role=Inverse` |
| Toolbar / nav-bar icon (close, settings, more) | `Size=S, Type=Ghost, Icon Only=True, Role=Default` |
| Inline text link ("View all") | `Size=S, Type=Ghost, Icon Only=False, Role=Link` or `Role=Text` |
| Secondary action ("Cancel") | `Size=M, Type=Secondary, State=Outline` |
| Destructive action ("Delete") | `Size=L, Type=Primary, Role=Red` |
| Caution action ("Mark as exception") | `Size=L, Type=Primary, Role=Yellow` |
| Card grid tile ("Add photo") | `Size=M, Type=Tile, Icon Only=True` |

---

## Do

- ✅ Use `Size=L, Type=Primary, Role=Inverse` for the single primary action per screen. iOS HIG: one prominent CTA per view.
- ✅ Use `Size=S, Type=Ghost, Icon Only=True, Role=Default` for toolbar / nav-bar icon buttons.
- ✅ Use `Role=Red` only for destructive actions (delete, reject, dismiss).
- ✅ Use `Role=Yellow` only for caution / warning actions. Yellow reads as "proceed carefully".
- ✅ For "Cancel" paired with a confirm CTA, use `Type=Secondary, State=Outline` — visual hierarchy without competing with the primary.

## Don't

- ❌ Don't stack two `Type=Primary` buttons in the same view — visual weight competes. Demote one to `Secondary` or `Ghost`.
- ❌ Don't use `Role=Blue` for a destructive action because it "looks calm" — destructive is `Role=Red`.
- ❌ Don't use `Role=Yellow` for a default CTA — users read yellow as caution.
- ❌ Don't reach for `State=Outline` on `Type=Primary` — the combination is impossible. Use `Type=Tertiary` or `Type=Secondary` with `State=Outline`.
- ❌ Don't use `Type=Tile` for general actions — it's for card-grid contexts ("Add photo", "Add receipt") where buttons act as drop targets.

---

Back to [[Design System]] · [[Component Status]].
