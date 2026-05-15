# Input

Single-line text input with optional label, helper text, and leading/trailing icons. Used for all text entry, search bars, form fields, and data capture. For multi-line text use `Text Area`; for signature capture use `Draw Area`.

- **Component set node:** `230:56`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=230-56)
- **Figma section:** `----- Inputs` → "Input States"
- **Figma documentation:** Section `1713:4078` "Input — Documentation" on the same page

---

## Composition

`State=Default` (`230:2`) — vertical stack of three regions.

| Layer | Bindings |
|---|---|
| Title (label) | font `Form/Label/*` (Subheadline 15pt) · fill `Text/Primary` |
| Container (the pill) | fill `Background/Subtle` · radius `Radius/Pill` (999) · padding `Space/XS` × `Space/L` · gap `Space/S` · stroke `Width/XS` |
| ↳ Leading icon (24×24) | `Icon/Primary` |
| ↳ Subtitle (placeholder / value) | font `Form/Input/*` (Body 17pt) · fill `Text/Tertiary` (placeholder) |
| ↳ Trailing icon (24×24) | `Icon/Primary` |
| Footer (helper) | font `Text/Footnote/*` · fill `Text/Tertiary` |

---

## Variants — `State`

| State | Container stroke | Placeholder | Helper fill | Use for |
|---|---|---|---|---|
| `Default` | none | `Text/Tertiary` | `Text/Tertiary` | Empty field with placeholder |
| `Focused` | `Border/Blue` | `Text/Tertiary` | `Text/Tertiary` | Keyboard active on field |
| `Filled` | none | `Text/Primary` (typed) | `Text/Tertiary` | Field has a typed value |
| `Negative` | `Border/Negative` | `Text/Secondary` | `Text/Negative` | Validation error — populate Helper with error message |
| `Positive` | `Border/Positive` | `Text/Secondary` | `Text/Positive` | Validation success |
| `Disabled` | none | `Text/Disabled` | `Text/Disabled` | Field temporarily unavailable |
| `Clear` | — | — | — | Cleared / reset value |

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Label` | TEXT | "Label" | Field label string |
| `Placeholder` | TEXT | "Placeholder Text" | Subtitle in Default / Focused state |
| `Helper` | TEXT | "Help Text" | Footer hint string |
| `Show Label` | BOOLEAN | true | Toggles the label row |
| `Show Helper` | BOOLEAN | true | Toggles the helper row |
| `Show Leading` | BOOLEAN | true | Toggles the leading icon |
| `Show Trailing` | BOOLEAN | true | Toggles the trailing icon |
| `Leading Icon` | INSTANCE_SWAP | `Icons/circle` | Swap source for leading icon |
| `Trailing Icon` | INSTANCE_SWAP | `Icons/circle` | Swap source for trailing icon |

---

## Do

- ✅ Use `Default` for empty form fields with a placeholder.
- ✅ Use `Focused` when the field has keyboard focus — `Border/Blue` confirms the active field.
- ✅ Pair `Negative` with the `Helper` slot populated by the error message.
- ✅ Bind `Leading Icon` for context icons that clarify field intent (search, person, email).
- ✅ Bind `Trailing Icon` for action icons (clear ×, show/hide eye, mic).
- ✅ Always show `Label` for named fields — required for accessibility.

## Don't

- ❌ Don't rely on the placeholder for important context — it disappears on typing. Use `Label` and `Helper` for persistent context.
- ❌ Don't pair `Negative` without populating `Helper` with the error message — error border without explanation fails a11y.
- ❌ Don't use `Filled` to mean "selected". `Filled` means "has typed content".
- ❌ Don't use `Disabled` for read-only display of saved values — use a Content Row instead.
- ❌ Don't bind `Leading Icon` / `Trailing Icon` to decorative icons — those slots are for affordances.

---

Back to [[Design System]] · [[Component Status]].
