# Page Control

iOS-style dot indicator showing position in a paginated horizontal scroll — onboarding screens, image carousels, multi-step flows. The row of dots represents pages; the active page is implied by the consumer (not a variant in this component).

- **Component node:** `1489:54`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=1489-54)
- **Figma section:** `----- Stepper`
- **Figma documentation:** Section `1724:5470` "Page Control — Documentation" on the same page

---

## Composition

Horizontal row of dot ellipses centered in a 393×44 container.

| Layer | Bindings |
|---|---|
| Container (FRAME) | fill `Background/Primary` |
| Dot (ELLIPSE × N) | fill `Background/Inverse` |

The component ships with 5 dots, all the same style. Detach and modify if you need a different count or want to mark an active dot.

---

## Variants

None.

---

## Instance properties

None.

---

## Do

- ✅ Use Page Control beneath a paginated horizontal scroll to communicate "there are more pages this direction".
- ✅ Center the component horizontally beneath the scroll area.
- ✅ Detach and override one dot's opacity / fill to mark the current page (the component itself doesn't model the active state).

## Don't

- ❌ Don't use Page Control with more than ~10 dots — iOS HIG: it stops being scannable. Use a numeric indicator ("3 of 14") for long sequences.
- ❌ Don't use Page Control for non-page content — it implies horizontal pagination.
- ❌ Don't rely on Page Control alone to communicate progress through a flow — pair with a clear "Next" button.

---

Back to [[Design System]] · [[Component Status]].
