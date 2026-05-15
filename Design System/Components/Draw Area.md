# Draw Area

Signature capture / freehand drawing field with optional label, placeholder, and eraser. Used for signing forms, capturing scribbles, drawing on outlines. For single-line text use [[Input]]; for multi-line text use [[Text Area]].

- **Component set node:** `671:968`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=671-968)
- **Figma section:** `----- Inputs` → "Signature Input"
- **Figma documentation:** Section `1716:4517` "Draw Area — Documentation" on the same page

---

## Composition

`Size=S` (`671:967`) — vertical stack of two regions.

| Layer | Bindings |
|---|---|
| Label (TEXT) | font `Form/Label/*` (Subheadline 15pt) · fill `Text/Primary` |
| Draw Field (FRAME) | fill `Background/Subtle` · radius `Radius/L` (16) · padding `Space/L` all sides · gap `Space/S` |
| ↳ Placeholder (TEXT) | font `Text/Body/*` (Body 17pt) · fill `Text/Tertiary` |
| ↳ Eraser (Button instance, 44×44) | `Icons/eraser-line-dashed`, `Radius/Pill` |

Outer frame `itemSpacing` `Space/S` (8). No header/footer rows beyond Label.

---

## Variants — `Size`

| Size | Dimensions | Use for |
|---|---|---|
| `S` | 361 × 231 | Inline form signature fields (default for most forms) |
| `M` | 564 × 316 | Standalone signature capture screens / larger drawing surfaces |

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Label Text` | TEXT | "Label" | Field label string |
| `Show Label` | BOOLEAN | true | Toggles the label row |
| `Placeholder` | TEXT | "Placeholder" | Tap-to-draw hint shown inside the Draw Field |
| `Show Eraser` | BOOLEAN | true | Toggles the eraser button |

---

## Do

- ✅ Use `Size=S` for inline form signature fields.
- ✅ Use `Size=M` for standalone signature-capture screens or larger drawing surfaces.
- ✅ Keep `Show Eraser=true` for any signature-as-legal-record use — users need to retry.
- ✅ Show `Label` for named fields ("Customer signature", "Driver signature") — required for accessibility.
- ✅ Pair the field with an explicit "Clear" or "Done" affordance outside the component for actions beyond erase.

## Don't

- ❌ Don't use Draw Area for text entry — use [[Input]] or [[Text Area]].
- ❌ Don't hide the Eraser on signature flows — users mis-sign and need to redo.
- ❌ Don't rely on the placeholder to communicate context — it disappears once the user draws. Use `Label` and a separate helper line beneath if context matters.

---

Back to [[Design System]] · [[Component Status]].
