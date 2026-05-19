# Action Section

Pill-shaped section header with a label, optional INOP badge, optional VIN/Weight stats, and 1–2 trailing affordances. Used at the top of a screen content group — represents the "this is a thing" header (vehicle, customer, trip) with quick context and inline actions.

Pairs with [[Trailing (Action Section)]] for the trailing pill buttons.

- **Component set node:** `475:1232`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=475-1232)
- **Figma section:** `----- Action Section` → "Action Section"
- **Figma documentation:** Section `1749:8044` "Action Section — Documentation" on the same page

---

## Composition

`Type=Default` — horizontal pill: label + optional INOP badge + optional VIN/Weight + 1–2 trailing actions.

| Layer | Bindings |
|---|---|
| Container (FRAME) | fill `Background/Subtle` · radius `Radius/Pill` · padding `Space/L` left · `Space/S` top/bottom · `Space/XL` right · gap `Space/S` |
| Label (TEXT) | `Text/Body/*` (17pt) · `Text/Primary` |
| INOP Badge (FRAME) | fill `Background/Primary Red` · radius `Radius/Pill` · padding `Space/XS` all sides |
| VIN/Weight stats (TEXT) | `Text/Footnote/*` (13pt) · `Text/Tertiary` |
| Trailing × 1–2 | nested [[Trailing (Action Section)]] instances |

`Type=Clear` removes the container fill (transparent background) — used when the Action Section sits on a non-Primary surface.

---

## Variants — `Type`

| Type | Use for |
|---|---|
| `Default` | Standard header pill with `Background/Subtle` surface |
| `Clear` | Transparent header — when the section sits on a colored / contrasting background |

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Label` | TEXT | "Label Placeholder" | Primary section label (vehicle, customer name, etc.) |
| `Show Trailing 1` | BOOLEAN | true | Toggle the first trailing action |
| `Show Trailing 2` | BOOLEAN | true | Toggle the second trailing action |
| `INOP` | BOOLEAN | true | Show the INOP (inoperable) badge |
| `VIN & Weight` | BOOLEAN | false | Show the VIN / Weight stats line |

---

## Do

- ✅ Use Action Section at the top of a content group — vehicle details, customer cards, trip headers.
- ✅ Use `INOP=true` only when the vehicle is actually inoperable — the red badge is high-signal.
- ✅ Bind Trailing slots to [[Trailing (Action Section)]] (Icon, Text, Icon-chevron).
- ✅ Use `Type=Clear` when the surrounding surface already provides visual separation.

## Don't

- ❌ Don't use Action Section as a generic list row — use [[Content Row]] or [[List]].
- ❌ Don't fill both Trailing slots with conflicting actions — pick the primary and demote / drop the second.
- ❌ Don't combine `INOP=true` with content that contradicts it (active trip, healthy stats).

---

Back to [[Design System]] · [[Component Status]].
