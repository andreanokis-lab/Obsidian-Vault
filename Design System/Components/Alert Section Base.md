# Alert Section Base

Inline alert container — tinted background + optional border for inline status messages. Six variants combining alert severity (Positive · Negative · Info) with an optional stroke. Holds any content via its Slot property.

- **Component set node:** `659:440`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=659-440)
- **Figma section:** `----- Info Alert` → "Alert Section Base"
- **Figma documentation:** Section `1761:8774` "Alert Section Base — Documentation" on the same page

---

## Composition

`Alert=Negative, Stroke=True` — rounded rect with tinted fill, optional border, padding, and a content slot.

| Layer | Bindings |
|---|---|
| Container (FRAME) | radius `Radius/L` · padding `Space/S` × `Space/XS` · gap `Space/XS` · stroke `Width/XS` (when Stroke=True) |
| Slot (FRAME) | padding `Space/XS` · gap `Space/XS` |
| Slot content | any nested instance / layout |

Container fill and stroke change per Alert variant — see below.

---

## Variants

| Alert | Fill | Stroke (when Stroke=True) | Use for |
|---|---|---|---|
| `Positive` | `Background/Subtle Green` | `Border/Positive` | Success / approval alerts |
| `Negative` | `Background/Error` (legacy — kept by decision) | `Border/Negative` | Error / destructive alerts |
| `Info` | `Background/Subtle Yellow` | `Border/Yellow` | Caution / informational alerts — yellow by brand choice |

`Stroke=False` removes the border for a softer, fill-only appearance.

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Slot` | SLOT | — | Inner content of the alert (icon, text, buttons, etc.) |

---

## Do

- ✅ Use `Positive` for success alerts (action completed, validation passed).
- ✅ Use `Negative` for error / destructive alerts (validation failed, action blocked).
- ✅ Use `Info` for caution / informational alerts — yellow is the brand's "heads up" colour.
- ✅ Use `Stroke=True` when the alert needs visual emphasis or sits on a similar-tinted surface; `Stroke=False` when the fill alone is enough.
- ✅ Compose content inside the Slot — icon + text, or text + button, etc.

## Don't

- ❌ Don't use Alert Section Base for full-screen errors / dialogs — use a Sheet or Toast pattern instead.
- ❌ Don't override the fill / stroke colors manually — pick the variant that matches the severity.
- ❌ Don't stuff a paragraph into the slot without a clear primary message — alerts should be scannable.

---

Back to [[Design System]] · [[Component Status]].
