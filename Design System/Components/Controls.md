# Controls

Tiny icon glyph used inside [[Counter]], stepper compositions, and (as `xMark`) the trailing slot of [[Segment Control]]. Each variant is a single vector bound to `Icon/Primary`, in a 44×44 tap target.

- **Component set node:** `418:227`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=418-227)
- **Figma section:** `----- Segment Control` → "Controls"
- **Figma documentation:** Section `1748:7937` "Controls — Documentation" on the same page

---

## Composition

Single VECTOR per variant.

| Layer | Bindings |
|---|---|
| Vector (VECTOR) | `Icon/Primary` |

---

## Variants — `+ / - / x`

| Value | Node | Use for |
|---|---|---|
| `Plus` | `418:200` | Increment icon — typically the right side of a Counter |
| `Minus` | `418:226` | Decrement icon — typically the left side of a Counter |
| `xMark` | `2149:4518` | Dismiss / close glyph. Added later than Plus/Minus. |

⚠️ The `xMark` variant reads as **close / dismiss** on iOS (modal close, chip removal, clear-text in a search field). Don't reuse it to mean "clear the current selection."

Its only reference was the hidden trailing slot inside [[Segment Control]], which was **killed on 2026-08-11** ([[Rules#C5]]) — that slot is scheduled for deletion from all 13 variants of `321:1008`. The `xMark` variant itself stays in this set as a legitimate dismiss glyph.

---

## Instance properties

None — the variant choice is the only property.

---

## Do

- ✅ Use Controls inside compositions that need a +/− affordance ([[Counter]], custom steppers).
- ✅ Bind the variant to the matching action (Plus for increment, Minus for decrement).
- ✅ Pair both Plus and Minus side-by-side; never use just one alone (a single +/− with no opposite is ambiguous).
- ✅ Use `xMark` only where the meaning really is *close / dismiss / remove this thing* (sheet close, chip removal, clear a text field).

## Don't

- ❌ Don't use Controls as a standalone button — it's a sub-piece, not a CTA. For full-button affordances use [[Button]].
- ❌ Don't change the Icon binding — Plus, Minus, and xMark are the only intended glyphs.
- ❌ Don't enlarge Controls past their default size — they're designed for compact inline use.
- ❌ Don't use `xMark` as a "deselect / reset filter" affordance inside a mutually exclusive selection group. Add an `All` segment or a text `Clear` button instead — see [[Segment Control]].

---

Back to [[Design System]] · [[Component Status]].
