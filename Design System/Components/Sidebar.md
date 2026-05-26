---
status: built
figma_node: 1109:1068
file_key: 3qOFF7kHsaZPfdftDb1CVz
---

# Sidebar

Slide-in drawer overlay anchored to the right edge of the screen. Houses secondary navigation rows (Outline, Receipts, Invoice, Deposit Slip, Truck Service in the default build). Sits over a dimming scrim that captures taps outside the drawer to close.

**Figma:** [HaulEx UIKit · Sidebar](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=1107-3)
**Component:** `1109:1068`
**Library key:** `81108e46034cc6d3b7aba8d907c2a26c2d8d02be`

---

## Anatomy

```
┌──────────┬────────────────────────┐
│          │ ─────── 48pt ───────── │   ← pt: Space/4XL
│          │  🗺  Outline           │
│          │  ─────────────────     │   ← Divider hairline
│  Scrim   │  📄  Receipts          │
│  rgba    │  ─────────────────     │
│  (0,0,0, │  📃  Invoice           │
│   0.4)   │  ─────────────────     │
│          │  💼  Deposit Slip      │
│          │  ─────────────────     │
│          │  🔧  Truck Service     │
│          │  ─────────────────     │
│          │                        │
└──────────┴────────────────────────┘
   ~72pt          ~321pt              total 393pt
```

- **Frame:** 393×852pt
- **Overlay scrim:** absolute fill, `rgba(0,0,0,0.4)` — taps outside the drawer dismiss
- **Sidebar Base:** anchored right edge, inset-left ~18.32% (~72pt) from the left edge → ~321pt wide
- **Container:**
  - Background: `Background/Subtle` (`#262626`)
  - Corners: top-left and bottom-left rounded `Radius/L` (16pt); right corners flat (flush with screen edge)
  - Padding: top `Space/4XL` (48pt), bottom 8pt, horizontal 8pt
  - Gap between rows: 8pt
- **Each row** (instance of [[Components/List|List]] composed with [[Components/Row Text|Row Text]]):
  - Width: 100% of container
  - Padding: `Space/S` (8pt) horizontal, 0pt vertical
  - Internal gap: `Space/S` (8pt)
  - Row Text width: 201pt
  - Icon: 32pt SF Symbol (filled), variants: `map.fill`, `receipt.fill`, `text.document.fill`, `wallet.bifold.fill`, `wrench.adjustable.fill`
  - Label: `Text/Body` (17 / 22), `Text/Primary`
  - Trailing area: 44×136pt reserved slot (chevron/count/toggle — empty in default)
  - Divider: hairline at row bottom

---

## Tokens

**Colors**
- Scrim: `rgba(0, 0, 0, 0.4)` — not yet a semantic token; flag if a `Background/Scrim` token is added.
- Container: `Background/Subtle` (`#262626`)
- Label: `Text/Primary` (`#f2f2f2`)
- Divider: `Border/Subtle`

**Spacing**
- `Space/4XL` 48pt — top padding (accommodates status bar + breathing room)
- `Space/L` 16pt — not used (compact drawer)
- `Space/S` 8pt — row padding and inter-row gap
- 8pt — bottom & side container padding

**Radius**
- `Radius/L` 16pt — top-left + bottom-left corners only

**Type**
- Row label: `Text/Body` (17 / 22, regular, letter-spacing −0.408)

---

## Composed components

- [[Components/List|List]] — each row
- [[Components/Row Text|Row Text]] — icon + label inside each list row
- [[Components/Divider|Divider]] — between rows
- Icon set: SF Symbols filled glyphs (`map.fill`, `receipt.fill`, `text.document.fill`, `wallet.bifold.fill`, `wrench.adjustable.fill`)

---

## Usage rules

- Trigger only from the leading icon button in [[Navigation Bar]] (or equivalent).
- Tap on scrim dismisses the sidebar. Provide a back/close affordance too — never rely solely on the scrim.
- Use for secondary navigation grouped by feature area. Don't put primary destinations here — those belong in [[Tab Bar]].
- Don't exceed ~6–8 rows. If you need more, switch to a full-screen menu list inside a sheet ([[Sheet Pattern]] · Variant 2).
- Animate from right edge with iOS-standard slide-in (~300ms). Spec ownership: the engineering team — annotate the motion direction in design hand-off.
- Respect bottom safe area; the container reaches the bottom of the screen but tap targets must be padded ≥44pt ([[Rules]] L1).
- The default build has no active/selected state per row — if needed, file a new variant via [[Component Status]].

---

## Known gaps

- **Scrim token** — currently a hardcoded `rgba(0,0,0,0.4)`. Open a token request for `Background/Scrim` and update both this note and the component.
- **Active row state** — no selected/pressed variant. May be needed if rows can deep-link to a current view.

---

## Related

- Trigger: leading icon in [[Components/Navigation Bar|Navigation Bar]]
- Navigation strategy: [[Navigation Patterns]]

Back to [[Design System]] · [[Component Status]].
