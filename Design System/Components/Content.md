# Content

Image tile + caption + status badge. Used inside photo lists, inspection rows, and capture confirmations to show a thumbnail with its label and capture / upload status.

Pairs with [[Trailing (Image Content)]] for the row-level status badge when used inside a list.

- **Component set node:** `535:721`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=535-721)
- **Figma section:** `----- Image Content` → "Content"
- **Figma documentation:** Section `1751:8255` "Content — Documentation" on the same page

---

## Composition

`Status=Error` — vertical stack: image tile + caption + status badge.

| Layer | Bindings |
|---|---|
| Image (FRAME) | fill `Background/Subtle` · radius `Radius/S` · stroke `Width/XS` · stroke color per Status (e.g. `Border/Negative`) |
| Caption (TEXT, "Right front hood") | `Text/Footnote/*` (13pt) · `Text/Primary` |
| Badge (FRAME, optional) | fill per Status (`Background/Primary Red` for Error) · `Radius/Pill` · padding `Space/XS` |

Other Status variants swap the stroke color and badge fill.

---

## Variants — `Status`

| Status | Stroke / Badge | Use for |
|---|---|---|
| `Default` | no stroke / no badge | Image not yet captured / pending |
| `Success` | `Border/Positive` / `Background/Primary Green` badge | Successfully captured & uploaded |
| `Error` | `Border/Negative` / `Background/Primary Red` badge | Capture failed, retry required |

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Label Text` | TEXT | "Right front hood" | Caption beneath the image |
| `Image Placeholder` | BOOLEAN | true | Toggle the placeholder icon when no image bound |
| `Text` | BOOLEAN | true | Toggle the caption visibility |

---

## Do

- ✅ Use `Default` for image tiles awaiting capture.
- ✅ Use `Success` once the image has been captured and uploaded.
- ✅ Use `Error` for failed captures — pair with retry messaging at the row / list level.
- ✅ Keep captions short (1–3 words) — the tile is sized for compact labels.

## Don't

- ❌ Don't use Content for full-size image displays — use [[Image]] (atom) directly.
- ❌ Don't rely on the colored border alone for accessibility — pair Error states with descriptive text.
- ❌ Don't hide both the placeholder icon and the caption — the tile loses context entirely.

---

Back to [[Design System]] · [[Component Status]].
