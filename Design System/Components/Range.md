# Range

Two-label range display — "From" / "To" with an arrow between them. Used for date ranges, value ranges, and segment endpoints (e.g., trip start → end, time range pickers).

- **Component set node:** `379:716`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=379-716)
- **Figma section:** `----- Card` → "Range"
- **Figma documentation:** Section `1737:7166` "Range — Documentation" on the same page

---

## Composition

Horizontal layout: From label · arrow icon · To label.

| Layer | Bindings |
|---|---|
| Label (TEXT, "From" value) | `Text/Secondary/*` (15pt, SF Pro Text) · `Text/Secondary` |
| Arrow icon (VECTOR) | `Icon/Subtle` |
| Label (TEXT, "To" value) | `Text/Secondary/*` (15pt) · `Text/Secondary` |

---

## Variants — `State`

| State | Use for |
|---|---|
| `Default` | Active / editable range |
| `Disabled` | Read-only or non-tappable range |

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `From` | TEXT | "Label" | Left value (start of range) |
| `To` | TEXT | "Label" | Right value (end of range) |

---

## Do

- ✅ Use Range for any "from → to" pair: date ranges, time ranges, location pairs, value bounds.
- ✅ Bind both `From` and `To` — empty values break the visual symmetry.
- ✅ Use `Disabled` when the range is fixed / not editable (e.g., showing a historical range).

## Don't

- ❌ Don't use Range for a single date / value — use plain [[Row Text]] or a Picker [[Trailing (Content Row)]] instead.
- ❌ Don't use Range for non-ordered pairs (e.g., "Pickup vs Delivery" where one isn't strictly "before" the other) — the arrow implies sequence.
- ❌ Don't put multiline text in From / To — the range layout is sized for short values (dates, times, short labels).

---

Back to [[Design System]] · [[Component Status]].
