---
status: built
figma_node: 421:1573
file_key: 3qOFF7kHsaZPfdftDb1CVz
---

# Toast

Transient, non-blocking feedback. 4 Message variants cover the standard status spectrum (Success, Error, Warning, Info). Used by [[Error State Pattern]] for non-blocking failures (e.g. photo upload, save) and by success acknowledgements that don't require a confirmation step.

**Figma:** [HaulEx UIKit · Toast](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=421-1601)
**Component set:** `421:1573`
**Library key:** `257259a5df4025579182c542bdc1144318fcb2fb`

---

## Variants — `Message`

| Message | Node | Icon | Icon color |
|---|---|---|---|
| Success | `421:1569` | `checkmark.circle.fill` | Status Green |
| Error | `421:1571` | `xmark.circle.fill` | Status Red |
| Warning | `421:1570` | `exclamationmark.circle.fill` | Status Yellow |
| Info | `421:1572` | `exclamationmark.circle.fill` | Status Blue |

Each variant: 361×50pt pill.

---

## Anatomy

```
┌──────────────────────────────────────────────────────┐
│ ⊙ Short title is best right here       │  Close      │  ← 50pt height
└──────────────────────────────────────────────────────┘
   ↑                                       ↑
   Icon 24pt + label                       Divider + Close button
   Space/S (8) gap                         Space/M (12) gap
```

- **Container:** 361×50pt, `background/subtle`, `radius/pill`
- **Padding:** `Space/L` (16pt) all sides
- **Inner row:** flex space-between, full width (329pt content area)
- **Leading group:** icon (24pt) + message text — gap `Space/S` (8pt)
- **Trailing group:** vertical divider (full height) + Close text button — gap `Space/M` (12pt)
- **Close button:** 32pt high, `Space/XS` (4pt) vertical padding, `radius/pill`

---

## Tokens

**Colors**
- Container: `Background/Subtle` (`#262626`)
- Message text + Close label: `Text/Primary` (`#f2f2f2`)
- Icon tints (status colors, see [[Colors - Semantic]]):
  - Success → `Status/Green` (filled circle background)
  - Error → `Status/Red`
  - Warning → `Status/Yellow`
  - Info → `Status/Blue`
- Divider: hairline, `Border/Subtle`

**Spacing**
- `Space/L` 16pt — container padding
- `Space/M` 12pt — divider/Close gap
- `Space/S` 8pt — icon/text gap
- `Space/XS` 4pt — Close button vertical padding

**Radius**
- `Radius/Pill` 999pt — container and Close button

**Type**
- Message text: `Text/Secondary` (15 / 20, regular, letter-spacing −0.45)
- Close button label: `Form/Label` (15 / 20, regular, letter-spacing −0.45)

**Icons** — 24pt SF Symbols filled circle glyphs

---

## Composed components

- [[Components/Divider|Divider]] — vertical hairline between message and Close
- Inline icon (SF Symbol) + inline Close button (no [[Components/Button|Button]] component instance — text-only Ghost-style action)

---

## Usage rules

- Toast is **non-blocking**. Use only for feedback that doesn't require user action; if a decision is required, use a Sheet ([[Sheet Pattern]]) or inline Alert ([[Alert Section Base]]) instead.
- One toast at a time. Stack only when actions are unrelated (rare).
- Default dismiss timer: 4s for Success/Info, 6s for Warning/Error. Tap Close to dismiss earlier.
- Position above the [[Tab Bar]] (or bottom safe area) with `Space/L` (16pt) margin from screen edges.
- Message text must be a single line — copy must be short. See [[Content Style Guide]] for tone.
- Color alone is not enough — every variant pairs a status color with an icon shape so colorblind users can distinguish ([[Rules]] A1).
- Don't use Toast for destructive confirmations or anything requiring an action — those need a Sheet.

---

## Component properties

- `message` — `Success \| Error \| Warning \| Info`
- `information` — message text (default: "Short title is best right here")

---

## Related

- Pattern owner: [[Error State Pattern]] (non-blocking failure tier)
- Decision matrix for inline vs modal vs toast: [[Error State Pattern]]

Back to [[Design System]] · [[Component Status]].
