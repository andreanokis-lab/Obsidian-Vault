# Vehicle Details Screen

Full inspection data + vehicle data screen for the HaulEx Driver App.

**Figma:** `yhxCSzJrafZbqXGZOCBCKE` · page `1:2` ("DS") · wrapper node `1035:20512`
**Built:** 2026-06-25

---

## Purpose

Shows all inspection data (pickup + delivery) from all drivers, all child orders, all photos, notes, damages, and additional vehicle data. Lets drivers see upload status, retry failed photos, and download all inspection photos.

---

## Entry points

| From | Trigger | Notes |
|---|---|---|
| Order Details | Tap vehicle row (combined with Start Inspection button) | Not yet built in Order Details |
| Sync page | Tap vehicle in upload list | Not yet built in Sync page |

---

## Layout — stacked sections (393pt wide)

```
┌────────────────────────────────────────┐
│  Navigation Bar — "Vehicle Details"    │
├────────────────────────────────────────┤
│  Action Section — Vehicle header pill  │
│  2015 Porsche Cayenne · INOP badge     │
│  VIN · Weight                          │
├────────────────────────────────────────┤
│  Upload Summary Banner (Alert Base)    │
│  "Photo uploads · 8/10"  [2 FAILED]    │
│  [Retry failed]  [Download all]        │
├────────────────────────────────────────┤
│  Vehicle Data (Card)                   │
│  VIN / Year-Make-Model / Color         │
│  Lot # / Mileage / Keys / Fuel level   │
├────────────────────────────────────────┤
│  Pickup Inspection                     │
│  ▸ John D. · Order #15-1010  ∨         │
│    DAMAGES  ·  PHOTOS  ·  NOTES        │
│    ADDITIONAL INFO                     │
│  ▸ Maria K. · Order #15-1011  +        │
├────────────────────────────────────────┤
│  Delivery Inspection                   │
│  ▸ John D. · Order #15-1010  ∨         │
│    DAMAGES  ·  PHOTOS  ·  NOTES        │
│  ▸ Maria K. · Order #15-1011  +        │
├────────────────────────────────────────┤
│  [   Download all photos   ]  ← CTA   │
├────────────────────────────────────────┤
│  ✓ Toast overlay (Success)             │
└────────────────────────────────────────┘
```

---

## Section specs

### Navigation Bar
- Component: `Navigation Bar`, Type=Default
- Title: "Vehicle Details"
- Leading: back chevron button
- Trailing: action button

### Vehicle Header (Action Section)
- Component: `Action Section`, Type=Default
- INOP = true (badge visible)
- VIN & Weight = true
- Label: vehicle year/make/model
- Sub-label: VIN · lot number

### Upload Summary Banner
- Component: `Alert Section Base`, Warning stroke variant
- Header: "Photo uploads · 8/10" + `Badge` Type=Red, text "2 FAILED"
- Body: "2 photos failed to upload. Retry the failed photos or download the rest."
- Buttons: "Retry failed" (Button Size=M, Type=Ghost, Role=Negative) + "Download all" (Button Size=M, Type=Ghost, Role=Default)

### Vehicle Data Card
- Frame with `Background/Secondary` fill, `Radius/M` corner radius, `Border/Default` stroke
- 7 `Info row` instances: VIN, Year · Make · Model, Color, Lot #, Mileage, Keys, Fuel level
- Row dividers: `strokeBottomWeight=1` + `Border/Subtle` variable (not Divider component — SF Pro Text workaround)

### Inspection Sections (Pickup + Delivery)
Each section:
- Section header: `Section/Title` text + `Space/2XL` gap above
- Per driver+order group: `Collapse/Expand` (Detent=Full Detent)
  - Collapsed = "+" icon; Expanded = "∨"
  - Group label: "Driver Name · Order #XXXXX"

Per expanded group body:
- **Damages row:** `Damages` chips, `layoutWrap=WRAP`
  - Driver state (yellow), Customer state (red/orange)
  - Sub-label: count text "· N driver · M customer"
- **Photos row:** `Content` tiles 112×112pt, 3-per-row, `layoutWrap=WRAP`, 8pt gap
  - Success → green ✓ badge
  - Error → red × badge + "↺ Retry" label in `Text/Negative`
  - Default + uploading → grey tile + "Uploading…" label in `Text/Status Blue`
  - Sub-label: "PHOTOS · N of M uploaded"
- **Notes:** `Meta/Caption` label + body text in `Text/Primary`
- **Additional Info** (Pickup only): Personal items, Accessories, Drivable rows

### Download CTA
- Component: `Button`, Size=L, Type=Primary, Role=Inverse, Icon Only=False
- Label: "Download all photos"
- `layoutSizingHorizontal=FILL` inside content column
- Node: `1052:20748`

### Toast
- Component: `Toast`, Message=Success
- Text: "Photo re-uploaded successfully"
- Absolute positioned overlay, centered horizontally, 32pt above bottom
- Node: `1052:20766`

---

## Design rules applied

- **Single frame + semantic variables only** — user switches Light/Dark in Figma mode switcher
- Colors Semantic · Light modeId `110:0` forced on wrapper via `setExplicitVariableModeForCollection`
- All spacing: `Space/*` semantic tokens
- All colors: Semantic collection only (no primitives)
- No `textStyleId` from library — manual typography to avoid SF Pro Text deletion bug
- Safe area: top 54pt (status bar), bottom 34pt inset
- 44pt minimum tap targets on all interactive elements
- `Space/L` (16pt) screen margins; `Space/2XL` (32pt) section gaps

---

## Known gaps / next steps

- [ ] Install SF Pro Text in Driver App file → re-link `textStyleId` for all text nodes
- [ ] Build Order Details → Vehicle Details navigation entry point
- [ ] Build Sync page → Vehicle Details navigation entry point
- [ ] Add BOL Sets / vehicle outline diagram with Damage Markers on damage positions
- [ ] Fill photo tiles with real image hashes (currently grey placeholders)
- [ ] Add Maria K. expanded group content (currently collapsed/stub)

---

Back to [[Driver App]] · [[Sessions/2026-06-25 10-00 vehicle-details-screen|Session note]]
