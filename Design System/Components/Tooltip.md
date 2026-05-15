# Tooltip

Small floating label that explains an adjacent UI element on hover/tap, or a larger info popover with a title and body. Anchored to a target with a directional arrow.

- **Component set node:** `294:221`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=294-221)
- **Figma section:** `----- Tooltip` → "Tooltip"
- **Figma documentation:** Section `1716:4676` "Tooltip — Documentation" on the same page

---

## Composition

`Point=Top, Type=Default` (`294:219`) — vertical stack of content bubble + directional arrow.

| Layer | Bindings |
|---|---|
| Content (FRAME) | radius `Radius/L` (16) — wraps the popover body |
| ↳ popover-header (FRAME) | fill `Background/Subtle` · padding `Space/M` × `Space/L` |
| ↳↳ Tooltip label (TEXT) | `Text/Secondary/*` (Subheadline 15pt, SF Pro Text) · fill `Text/Primary` |
| Arrow (FRAME) | Vector pointer · fill `Background/Subtle` matching the body |

The `Info` variant replaces the single Tooltip label with a Title + Text body for richer popover content.

---

## Variants

Two axes — direction and content type.

| Axis | Values | Notes |
|---|---|---|
| `Point` | `Top` · `Down` · `Right` · `Left` · `Info Tooltip` | Arrow direction. `Info Tooltip` has no directional arrow — it's the rich popover layout |
| `Type` | `Default` · `Info` | `Default` is the small label tooltip; `Info` adds a Title + Text body |

Practical combinations:
- `Point=Top, Type=Default` — tooltip with arrow pointing up at a target below
- `Point=Down, Type=Default` — arrow pointing down at a target above
- `Point=Right, Type=Default` — arrow pointing right (target to the left)
- `Point=Left, Type=Default` — arrow pointing left (target to the right)
- `Point=Info Tooltip, Type=Info` — Title + Text card

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Label` | TEXT | "Tooltip" | Tooltip text (Default type) |
| `Title` | TEXT | "Title" | Title text (Info type only) |
| `Text` | TEXT | "Text" | Body text (Info type only) |

---

## Do

- ✅ Use `Default` for short labels explaining an icon or affordance (1–3 words).
- ✅ Match `Point` direction to the target — arrow always points at the element being explained.
- ✅ Use `Info` (Title + Text) for context that needs more than a few words — e.g. an inline explainer triggered by an "?" icon.
- ✅ Keep the Tooltip near its target — Apple HIG: connection between trigger and tooltip should be unambiguous.

## Don't

- ❌ Don't use Tooltip for primary content — tooltips are temporary/hover affordances, not where critical info lives.
- ❌ Don't stuff a paragraph into `Default` — use `Info` for multi-line context.
- ❌ Don't rely on Tooltip on touch-only devices for required information — there's no hover; users may miss it.
- ❌ Don't pick a `Point` direction without a target. Tooltips with no anchor lose their meaning.

---

Back to [[Design System]] · [[Component Status]].
