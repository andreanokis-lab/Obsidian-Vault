# 2026-06-25 — Vehicle Details Screen

**Session:** ~3 hours (two context windows)
**File:** HaulEx Driver App (`yhxCSzJrafZbqXGZOCBCKE`), page `1:2` ("DS")
**Wrapper node:** `1035:20512`
**Content column:** `1035:20513`

---

## What was built

A full **Vehicle Details** screen for the HaulEx Driver App. Single frame, stacked-section layout. User flips Light/Dark via Figma mode switcher (one frame, semantic variables only).

**Sections from top to bottom:**

1. **Navigation Bar** (Default, Type=Default) — "Vehicle Details" title, back + action trailing
2. **Action Section** (Type=Default) — vehicle header pill with INOP badge, VIN & Weight visible; vehicle name "2015 Porsche Cayenne · FLA58356731034563 · 2342"
3. **Upload Summary Banner** — `Alert Section Base` (Warning variant) with `2 FAILED` badge; "Retry failed" (Ghost/Negative) + "Download all" (Ghost/Default) buttons
4. **Vehicle Data** card — 7 `Info row` items (VIN, Year/Make/Model, Color, Lot #, Mileage, Keys, Fuel level); `strokeBottomWeight=1` dividers with `Border/Subtle` variable instead of Divider component
5. **Pickup Inspection** section — `Collapse/Expand` header per driver+order group. Each group body has:
   - `Damages` chips (Driver state = yellow, Customer state = red/orange)
   - Photo grid: `Content` (Status=Success/Error/Default) tiles in `layoutWrap=WRAP` rows, 3-per-row at 112pt
   - Error tile label: "↺ Retry" in `Text/Negative`; Default tile label: "Uploading…" in `Text/Status Blue`
   - Notes body text block
   - Additional Info rows (Personal items, Accessories, Drivable/INOP)
6. **Delivery Inspection** section — same structure as Pickup
7. **Download all photos** button — `Button` Size=L, Type=Primary, Role=Inverse, full-width at content column bottom
8. **Toast** — `Message=Success`, text "Photo re-uploaded successfully", absolute overlay at screen bottom

---

## Components used

| Component | Key | Notes |
|---|---|---|
| Navigation Bar | `0bd88b3b2f287ae3c52be13e79246374e3bf68a4` | Type=Default |
| Action Section | resolved from UIKit `475:1232` | Type=Default, INOP=true |
| Alert Section Base | resolved from UIKit `659:440` | Warning stroke variant |
| Button | `f84c0725806ab00f8adeafe077733ea60c27af7a` | Multiple sizes/roles |
| Collapse/Expand | resolved from UIKit `1410:2236` | Detent=Full Detent |
| Content | resolved from UIKit `535:721` | Status=Default/Success/Error |
| Damages | resolved from UIKit `607:2217` | State=Driver/Customer |
| Toast | `257259a5df4025579182c542bdc1144318fcb2fb` | Message=Success |
| Section Base | `5895cda17f750f1ec4d0aaca86323ce448623c6e` | Single COMPONENT (not set), UIKit page "----- Section Base", node `802:599`. Used for Vehicle Data, Notes (Pickup + Delivery), and Additional Info blocks. |

---

## Key patterns established

### SF Pro Text workaround
"SF Pro Text" font family is not installed in the Driver App file. All UIKit components that use it fail on `appendChild` with an unloaded font error. Fix: `remap(inst)` before and after every `appendChild` and `setProperties()` call. Rewrites all text segments from "SF Pro Text" → "SF Pro" at equivalent weight.

```js
async function remap(inst) {
  for (const t of inst.findAll(n => n.type === "TEXT")) {
    let segs;
    try { segs = t.getStyledTextSegments(["fontName"]); } catch(e) { continue; }
    for (const seg of segs) {
      if (seg.fontName.family !== "SF Pro" && seg.fontName.family !== "SF Pro Rounded") {
        const st = ["Regular","Medium","Semibold","Bold"].includes(seg.fontName.style) ? seg.fontName.style : "Regular";
        try {
          await figma.loadFontAsync({ family: "SF Pro", style: st });
          t.setRangeFontName(seg.start, seg.end, { family: "SF Pro", style: st });
        } catch(e) {}
      }
    }
  }
}
```

**Flag for later:** re-link textStyleId for all text nodes once SF Pro Text is added to the Driver App file.

### Manual typography (no textStyleId)
`t.textStyleId = style.id` silently deletes orphan text nodes when the style references SF Pro Text. All typography set manually: `fontSize`, `lineHeight`, `letterSpacing`, `fontName` in SF Pro at exact semantic spec values.

### Row dividers without Divider component
`frame.strokeBottomWeight = 1` with `Border/Subtle` variable bound via `setBoundVariableForPaint` → applied as `strokes`. Avoids placing the Divider component (which also has SF Pro Text issues).

### Wrapping photo grid
```js
row.layoutMode = "HORIZONTAL";
row.layoutWrap = "WRAP";
row.counterAxisSpacing = 8;
row.itemSpacing = 8;
```
Photo tiles are 112×112pt + 8pt gap = 3 columns fit in 361pt content width (16pt margins each side).

### Upload state per photo tile
- **Success:** `Content` Status=Success (green checkmark badge)
- **Error:** `Content` Status=Error (red × badge) + manual text "↺ Retry" in `Text/Negative` color
- **Uploading:** `Content` Status=Default + manual text "Uploading…" in `Text/Status Blue` color

---

## Token bindings used

- Colors Semantic collection · Light modeId: `110:0`
- `setExplicitVariableModeForCollection()` on wrapper to force Light mode
- All fills via `figma.variables.setBoundVariableForPaint()`
- Key semantic tokens: `Background/Primary`, `Background/Secondary`, `Background/Subtle`, `Text/Primary`, `Text/Secondary`, `Text/Tertiary`, `Text/Negative`, `Text/Status Blue`, `Border/Subtle`, `Border/Default`

---

## Entry points (documented only, not built)

- **Order Details** → tap vehicle row: opens Vehicle Details
- **Sync page** → tap vehicle: opens Vehicle Details (focused on upload status)

---

## Section Base usage (third context window)

Four manual label+content pairs replaced with `Section Base` instances via `importComponentByKeyAsync`. Pattern: create instance before the label node using `parent.insertChild(idx, inst)`, then move content node(s) into the inner `Slot` frame via `slot.appendChild(contentNode)`, then `labelNode.remove()`.

| Replacement | New node | Slot content |
|---|---|---|
| "Vehicle Data" title text + card wrapper | `1067:20790` | 7 `Info row` frames moved directly into slot (card wrapper removed — slot provides the card bg) |
| Pickup "NOTES" label + notes body text | `1067:20821` | Notes body text moved into slot |
| Pickup "ADDITIONAL INFO" label + rows frame | `1067:20827` | Additional info rows frame moved into slot |
| Delivery "NOTES" label + notes body text | `1067:20842` | Notes body text moved into slot |

**Key implementation detail:** For Vehicle Data, rows were placed directly into the slot (not the card wrapper frame) to avoid nested `Background/Subtle` backgrounds. The card wrapper was then deleted; the Section Base slot frame provides the rounded card appearance.

**Slot discovery:** `inst.findOne(n => n.name === "Slot")` reliably finds the slot frame inside each Section Base instance.

---

## What was NOT built this session

- Order Details modification (vehicle row → tap → push Vehicle Details)
- Sync page modification (vehicle list item → tap)
- Actual photo image fills (placeholder grey tiles)
- BOL Sets / vehicle outline diagrams with Damage Markers

---

Back to [[Driver App/Driver App|Driver App]] · [[Sessions]]
