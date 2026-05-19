# Controls

Tiny + / − icon pair used inside [[Counter]] and similar stepper compositions. Each variant is a single icon glyph — Plus or Minus — bound to `Icon/Primary`.

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

## Variants — `+ / -`

| Value | Use for |
|---|---|
| `Plus` | Increment icon — typically the right side of a Counter |
| `Minus` | Decrement icon — typically the left side of a Counter |

---

## Instance properties

None — the variant choice is the only property.

---

## Do

- ✅ Use Controls inside compositions that need a +/− affordance ([[Counter]], custom steppers).
- ✅ Bind the variant to the matching action (Plus for increment, Minus for decrement).
- ✅ Pair both Plus and Minus side-by-side; never use just one alone (a single +/− with no opposite is ambiguous).

## Don't

- ❌ Don't use Controls as a standalone button — it's a sub-piece, not a CTA. For full-button affordances use [[Button]].
- ❌ Don't change the Icon binding — Plus and Minus are the only intended glyphs.
- ❌ Don't enlarge Controls past their default size — they're designed for compact inline use.

---

Back to [[Design System]] · [[Component Status]].
