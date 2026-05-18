# Trailing (Image Content)

Small status badge attached to image-content rows — green Success or red Error indicator. Appears on photo lists, upload rows, or capture confirmations.

Note: four different components share the name "Trailing" across the UIKit. This one belongs to Image Content. See also [[Trailing (Content Row)]], [[Trailing (Action Section)]], [[Trailing (Sheets)]].

- **Component set node:** `535:669`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=535-669)
- **Figma section:** `----- Image Content` → "Trailing"
- **Figma documentation:** Section `1729:6238` "Trailing (Image Content) — Documentation" on the same page

---

## Composition

Pill badge with a single status icon.

| Layer | Bindings |
|---|---|
| Badge (FRAME) | fill per Status (`Background/Primary Green` / `Background/Primary Red`) · radius `Radius/Pill` · padding `Space/XS` all sides · gap `Space/S` |

---

## Variants — `Status`

| Status | Container fill | Use for |
|---|---|---|
| `Success` | `Background/Primary Green` | Upload complete, capture confirmed, verified |
| `Error` | `Background/Primary Red` | Upload failed, capture invalid, error state |

---

## Instance properties

None — the Status variant controls everything.

---

## Do

- ✅ Use `Success` on image rows that have completed upload / capture / processing.
- ✅ Use `Error` on image rows that failed — pair with a row-level helper line explaining the error.

## Don't

- ❌ Don't use this Trailing for non-image-content contexts. For inline status badges elsewhere, use [[Badge]] with `Role=Status`.
- ❌ Don't rely on color alone — pair with descriptive helper text for accessibility.

---

Back to [[Design System]] · [[Component Status]].
