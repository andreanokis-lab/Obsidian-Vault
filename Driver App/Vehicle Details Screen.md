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
- `Section Base` instance (key `5895cda17f750f1ec4d0aaca86323ce448623c6e`), node `1067:20790`
- Title = "Vehicle Data"; `Show Title=true`
- Slot contains: 7 `Info row` instances directly (VIN, Year · Make · Model, Color, Lot #, Mileage, Keys, Fuel level)
- Rows placed directly in slot — no extra card wrapper — to avoid nested `Background/Subtle` backgrounds
- Row dividers: `strokeBottomWeight=1` + `Border/Subtle` variable (not Divider component — SF Pro Text workaround)

### Inspection Sections (Pickup + Delivery)
Each section:
- Section header: `Section/Title` text + `Space/2XL` gap above
- Per driver+order group: `Collapse/Expand` (Detent=Full Detent)
  - No "+" icon (view-only); `Leading#1584:3` property = " " (space) to suppress it
  - Only "∨" chevron in Trailing for collapse/expand
  - Group label: "Driver Name · #ORDERNO.N" (split-order format, e.g. "John D. · #15-1010.1")
  - `Label#1410:0` property holds the full label string

Per expanded group body:
- **Damages row:** `Damages` chips, `layoutWrap=WRAP`
  - Driver state (yellow), Customer state (red/orange)
  - Sub-label: count text "· N driver · M customer"
- **Vehicle outline:** `BOL Sets` (Type=Vehicle Set) instance below chips, 361×609pt
  - COMPONENT_SET key: `7779808908547ec48d7e6c405dd85362da1283ae`; Type=Vehicle Set key: `873b07a79b7c9b7d28e13418488a63abd20d5d8b`
  - Wrapped in absolute-layout FRAME (no auto-layout), `layoutSizingHorizontal=FILL`
  - `Damage-Marker` instances at absolute x/y within wrapper (COMPONENT_SET `be7ad9bb1d0e903165fb8964f8c289a6df9d0621`)
    - Driver marker key: `4da0762c81edecde4dc4d7fd5a327c5b837a2f99` (yellow); Customer key: `fd4c72ea67e37b4aed60b1a00f7a34334910b1a3` (red); 24×24pt each
    - `Letter#608:2` TEXT property = damage letter (e.g. "S")
  - Pickup outline node: `1081:20792` (3 markers); Delivery outline node: `1081:20898` (1 marker)
  - Marker positions are approximate — designer to fine-tune x,y per damage view
- **Photos row:** `Content` tiles 112×112pt, 3-per-row, `layoutWrap=WRAP`, 8pt gap
  - Success → green ✓ badge; Error → red × badge
  - Upload/retry state shown via long-press contextual menu only — no overlay labels on tiles
  - Sub-label: "PHOTOS · N of M uploaded"
- **Notes:** `Section Base` (key `5895cda17f750f1ec4d0aaca86323ce448623c6e`) — Title="Notes"; slot = notes body text. Pickup node `1067:20821`, Delivery node `1067:20842`
- **Additional Info** (Pickup only): plain BOL-style rows — no Section Base, no card background
  - "Additional Info" title: `Section/Title` text style, `Text/Primary`, FILL width. Node `1079:20805`
  - Rows frame: VERTICAL auto-layout, transparent fills, no border radius. Node `1079:20806`
  - Each row: HORIZONTAL, `paddingTop/Bottom=12` (Space/M), label FILL + value HUG
  - Label: SF Pro Regular 12pt, `Text/Tertiary`; Value: SF Pro Regular 14pt, `Text/Primary`, right-aligned
  - Row content: Personal items / Accessories / Drivable

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

- [x] Replace manual Notes labels with `Section Base` instances ✓
- [x] Replace Vehicle Data title + card wrapper with `Section Base` ✓
- [x] Add BOL Sets vehicle outline + Damage-Marker instances to damages blocks ✓
- [x] Remove photo tile overlay labels ("Uploading…" / "↺ Retry") — now long-press only ✓
- [x] Collapse/Expand headers: remove "+", use split-order label format (#XXXXX.N) ✓
- [x] Additional Info: replace Section Base card with plain BOL-style rows ✓
- [ ] Fine-tune Damage-Marker x,y positions on vehicle outline views
- [ ] Install SF Pro Text in Driver App file → re-link `textStyleId` for all text nodes
- [ ] Build Order Details → Vehicle Details navigation entry point
- [ ] Build Sync page → Vehicle Details navigation entry point
- [ ] Fill photo tiles with real image hashes (currently grey placeholders)
- [ ] Add Maria K. expanded group content (currently collapsed/stub)

---

Back to [[Driver App]] · [[Sessions/2026-06-25 10-00 vehicle-details-screen|Session note]]
