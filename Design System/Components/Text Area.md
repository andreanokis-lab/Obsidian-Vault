# Text Area

Multi-line text input with optional label and helper text. Used for free-form longer text — notes, comments, descriptions, addresses. For single-line entry use [[Input]]; for signatures use Draw Area.

- **Component set node:** `257:836`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=257-836)
- **Figma section:** `----- Inputs` → "Text Area"
- **Figma documentation:** Section `1713:4397` "Text Area — Documentation" on the same page

---

## Composition

`State=Default` (`257:837`) — vertical stack of three regions.

| Layer | Bindings |
|---|---|
| Title (label) | font `Form/Label/*` (Subheadline 15pt) · fill `Text/Primary` |
| Container | fill `Background/Subtle` · radius `Radius/L` (16) · padding `Space/M` all sides · gap `Space/S` · ~88pt tall (≈3 lines) |
| ↳ Subtitle (placeholder / value) | font `Form/Input/*` (Body 17pt) · fill `Text/Disabled` (placeholder) |
| Footer (helper) | font `Text/Footnote/*` · fill `Text/Tertiary` |

Outer frame `itemSpacing` `Space/S` (8). No leading/trailing icons.

---

## Variants — `State`

| State | Container stroke | Placeholder fill | Helper fill | Use for |
|---|---|---|---|---|
| `Default` | none | `Text/Disabled` | `Text/Tertiary` | Empty field with placeholder |
| `Filled` | none | `Text/Primary` (typed) | `Text/Tertiary` | Field has typed content |
| `Negative` | `Border/Negative` | `Text/Secondary` | `Text/Negative` | Validation error — populate Helper with error |
| `Positive` | `Border/Positive` | `Text/Secondary` | `Text/Positive` | Validation success |
| `Disabled` | none | `Text/Disabled` | `Text/Disabled` | Field temporarily unavailable |

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Label` | TEXT | "Label" | Field label string |
| `Placeholder` | TEXT | "Placeholder Text" | Subtitle in Default state |
| `Helper` | TEXT | "Help Text" | Footer hint string |
| `Show Label` | BOOLEAN | true | Toggles the label row |
| `Show Helper` | BOOLEAN | true | Toggles the helper row |

---

## Do

- ✅ Use Text Area when the expected input is longer than a single line — notes, comments, addresses, descriptions.
- ✅ Use `Default` for empty fields with a placeholder.
- ✅ Pair `Negative` with the `Helper` slot populated by the error message.
- ✅ Always show `Label` for named fields — required for accessibility.

## Don't

- ❌ Don't use Text Area for single-line entry — use [[Input]] instead.
- ❌ Don't rely on the placeholder for important context — it disappears on typing. Use `Label` and `Helper` for persistent context.
- ❌ Don't pair `Negative` without populating `Helper` — error border without explanation fails a11y.
- ❌ Don't use `Disabled` for read-only display of saved text — use a Content Row or read-only layout instead.

---

Back to [[Design System]] · [[Component Status]].
