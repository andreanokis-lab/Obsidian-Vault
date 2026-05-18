# File field

File attachment row — small image thumbnail + filename + optional helper text. Used in document upload flows, attachment lists, receipt rows.

- **Component node:** `960:4667`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=960-4667)
- **Figma section:** `----- Content Row` → "File field"
- **Figma documentation:** Section `1730:6750` "File field — Documentation" on the same page

---

## Composition

Horizontal row: thumbnail + text column.

| Layer | Bindings |
|---|---|
| File field (FRAME) | gap `Space/S` |
| Image (FRAME) | `Radius/S` · `Background/Subtle` |
| Text column (FRAME) | gap `Space/Zero` |
| ↳ Row Text (TEXT) | `Text/Body/*` (17pt) · `Text/Primary` |
| ↳ Helper Text (TEXT, optional) | `Meta/Caption/*` (12pt) · `Text/Tertiary` |

---

## Variants

None — single component.

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Row Text` | TEXT | "Row Text" | Filename / primary label |
| `Helper Text` | TEXT | "Helper Text" | File metadata (size, date, type) |
| `Show Helper Text` | BOOLEAN | true | Toggle the helper line |

---

## Do

- ✅ Use the Row Text slot for the filename.
- ✅ Use Helper Text for metadata that helps users identify the file (date, size, type).
- ✅ Place File field inside a List or container — it doesn't include its own divider.
- ✅ Bind the Image to the actual file thumbnail (PDF preview, photo, etc.) — the default placeholder shows a generic image icon.

## Don't

- ❌ Don't use File field for non-file rows — for plain text rows use [[Row Text]] or [[List]].
- ❌ Don't stuff long paths into Row Text — truncate filenames or use the file's display name.
- ❌ Don't hide both Image and Helper Text — the row loses its file-affordance.

---

Back to [[Design System]] · [[Component Status]].
