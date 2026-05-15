# Counter

Numeric stepper — minus, count, plus. Used for adjusting a small integer value inline (quantity, photo count, item count). Tap minus to decrement, plus to increment.

- **Component node:** `418:252`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=418-252)
- **Figma section:** `----- Segment Control`
- **Figma documentation:** Section `1724:5332` "Counter — Documentation" on the same page

---

## Composition

Horizontal pill with minus icon, count, plus icon.

| Layer | Bindings |
|---|---|
| Container (FRAME) | fill `Background/Subtle` · radius `Radius/Pill` · gap `Space/L` (16) |
| Minus icon (VECTOR) | `Icon/Primary` |
| Count (TEXT) | font `Text/Body/*` (17pt Regular) · fill `Text/Primary` |
| Plus icon (VECTOR) | `Icon/Primary` |

132 × 44 dimensions. No state variants — single visual state.

---

## Variants

None. Single component.

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `#` | TEXT | "1" | The count number |

---

## Do

- ✅ Use Counter for adjustable integer values (quantity, photo count, pages).
- ✅ Pair with a label outside the component ("Photos", "Quantity") so the value has context.
- ✅ Enforce min/max at the consumer level — Counter doesn't constrain values.

## Don't

- ❌ Don't use Counter for free-form numeric entry (large numbers, decimals) — use [[Input]] with a numeric keyboard instead.
- ❌ Don't use Counter for boolean choices — use [[Toggle]].
- ❌ Don't bind Counter to a value with no defined range — visually it suggests +/- 1 increments.

---

Back to [[Design System]] · [[Component Status]].
