# Input Section

Compact two-line label pair — small caption ("Driver") above a primary value ("IOS Driver"). Used inside cards or compact data rows to show a label + value without a full [[Row Text]] layout.

- **Component node:** `356:1259`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=356-1259)
- **Figma section:** `----- Card` → "Input Section"
- **Figma documentation:** Section `1742:7216` "Input Section — Documentation" on the same page

---

## Composition

Vertical stack: caption + value.

| Layer | Bindings |
|---|---|
| Caption (TEXT, "Driver") | `Text/Body/*` (17pt Regular) · `Text/Tertiary` |
| Value (TEXT, "IOS Driver") | `Text/Secondary/*` (15pt, SF Pro Text) · `Text/Primary` |

68 × 42 default dimensions — sized for compact inline placement.

---

## Variants

None — single component.

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Name` | TEXT | "IOS Driver" | The primary value string |

---

## Do

- ✅ Use Input Section for compact "label + value" pairs inside cards or rows.
- ✅ Keep the caption short (1–2 words). The visual budget assumes a small label.
- ✅ Bind the `Name` to the actual value (driver name, ID, model, etc.).

## Don't

- ❌ Don't use Input Section for editable input — use [[Input]] (text field).
- ❌ Don't put multiline content in `Name` — the value is sized for a single line.
- ❌ Don't replicate Input Section for full rows — use [[Row Text]] or [[Content Row]] for label + value + helper layouts.

---

Back to [[Design System]] · [[Component Status]].
