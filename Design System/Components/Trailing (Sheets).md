# Trailing (Sheets)

Trailing pill button used in a [[Sheet]] header — typically a Cancel/Close action on the right side of a sheet's title bar.

Note: four different components share the name "Trailing" across the UIKit. This one belongs to Sheets. See also [[Trailing (Content Row)]], [[Trailing (Action Section)]], [[Trailing (Image Content)]].

- **Component set node:** `442:10099`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=442-10099)
- **Figma section:** `----- Sheets` → "Trailing"
- **Figma documentation:** Section `1729:6154` "Trailing (Sheets) — Documentation" on the same page

---

## Composition

Pill button — `Radius/Pill`, padding `Space/L` × `Space/XS`, gap `Space/S`.

---

## Variants — `Type`

| Type | Use for |
|---|---|
| `Circle Button` | Compact icon-only close / dismiss action (44×44 round) |
| `Text Button` | Labeled action — typically "Cancel", "Done", or "Save" in the sheet header |

---

## Instance properties

None at the component set level — text and icons live inside the nested button instance.

---

## Do

- ✅ Use `Circle Button` for icon-only dismiss in compact sheet headers.
- ✅ Use `Text Button` when the action has a verb that helps users understand the outcome ("Done" vs "Cancel").
- ✅ Always pair the trailing with a [[Title and Controls]] component that holds the sheet title.

## Don't

- ❌ Don't use Trailing (Sheets) outside a Sheet header. For buttons inside the sheet body, use [[Button]].
- ❌ Don't put both Circle Button and Text Button in the same sheet header — pick one trailing affordance.

---

Back to [[Design System]] · [[Component Status]].
