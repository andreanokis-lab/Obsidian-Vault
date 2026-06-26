# 2026-06-26 — Vehicle Details: BOL Outlines, Photo Cleanup, C/E Refactor

**Session:** ~2 hours (context continuation from 2026-06-25)
**File:** HaulEx Driver App (`yhxCSzJrafZbqXGZOCBCKE`), page `1:2` ("DS")
**Wrapper node:** `1035:20512` (3719pt tall after fixes)

---

## Changes made

### 1. BOL Sets vehicle outline in Damages blocks

Both Pickup and Delivery damage areas now show a 4-view vehicle outline (front / rear / left side / top) using the `BOL Sets` DS component.

**Pattern:**
- Create a plain FRAME (absolute layout, no auto-layout), 361×609pt
- Import `BOL Sets` Type=Vehicle Set → append at (0,0)
- Import `Damage-Marker` instances → `appendChild` at absolute x/y within the wrapper
- Set `wrapper.layoutSizingHorizontal = "FILL"` after appending to parent body

**Component keys:**
| Component | COMPONENT_SET key | Variant key |
|---|---|---|
| BOL Sets | `7779808908547ec48d7e6c405dd85362da1283ae` | Type=Vehicle Set: `873b07a79b7c9b7d28e13418488a63abd20d5d8b` |
| Damage-Marker (Driver, yellow) | `be7ad9bb1d0e903165fb8964f8c289a6df9d0621` | `4da0762c81edecde4dc4d7fd5a327c5b837a2f99` |
| Damage-Marker (Customer, red) | same set | `fd4c72ea67e37b4aed60b1a00f7a34334910b1a3` |

**BOL Sets 361×609 layout (for marker positioning):**
```
y=0–140:   rear view (x 0–180) | front view (x 181–361)
16pt gap
y=156–609: left-side view | top view | right-side view (~151pt each)
```

**Pickup markers (node `1081:20792`):**
- Driver "S" at (248, 14) — front bumper on front view
- Customer "S" at (120, 218) — left door on left-side view
- Customer "S" at (178, 360) — roof scuff on top view

**Delivery markers (node `1081:20898`):**
- Driver "S" at (62, 80) — rear scuff on rear view

Marker positions are approximate; designer should fine-tune x,y per damage.

---

### 2. Photo tiles — removed upload state overlay labels

`1051:508` ("Uploading…") and `1051:541` ("↺ Retry") text nodes removed from Delivery photo grid (`1051:432`). Upload and retry state now handled exclusively by long-press contextual menu — no overlay labels on tiles. Pickup tiles were already clean.

---

### 3. Collapse/Expand headers — split-order format, no "+"

All 4 C/E instances updated:
- `Leading#1584:3` = `" "` (space) — suppresses the "+" icon; no `Show Leading` boolean exists on this component
- `Label#1410:0` = split-order format: "Driver · #ORDERNO.N"

| Node | Label |
|---|---|
| Pickup John D. `1046:422` | "John D. · #15-1010.1" |
| Pickup Maria K. `1046:428` | "Maria K. · #15-1010.2" |
| Delivery John D. `1050:422` | "John D. · #15-1010.1" |
| Delivery Maria K. `1050:428` | "Maria K. · #15-1010.2" |

---

### 4. Additional Info — plain BOL-style rows (no card)

Replaced the `Section Base` instance (`1067:20827`) with hand-built rows matching the BOL reference (`1073:21615`):
- "Additional Info" title text: `Section/Title` style, `Text/Primary`, FILL width. Node `1079:20805`
- Rows frame: VERTICAL auto-layout, transparent fills, no border radius. Node `1079:20806`
- Row anatomy: HORIZONTAL, `Space/M` (12pt) vertical padding, label FILL (`Text/Tertiary`, 12pt) + value HUG (`Text/Primary`, 14pt, right-aligned)
- Rows: Personal items → "None" / Accessories → "Cargo cover · 2 mats" / Drivable → "No — INOP"

**Variable keys used:**
- `Text/Primary`: `aff383653238592d63787aeb0efa79dce669730f`
- `Text/Tertiary`: `007d33b101a95ffe1488d4d6897a60e2f2999c72`
- `Space/M`: `8787f94d341867410acf6fa6b7e451cd652f226a`

---

### 5. Pickup body height fix (critical bug)

Pickup body frame (`1046:426`) had `primaryAxisSizingMode = "FIXED"` from original build, clipping all content below the 754pt mark after the 609pt outline was inserted.

**Fix:** Set `primaryAxisSizingMode = "AUTO"` + `layoutSizingVertical = "HUG"` on:
- Pickup body `1046:426` → expanded 754pt → 1408pt
- Pickup group `1046:421`, Pickup inspection `1046:419`, content column `1035:20513`, wrapper `1035:20512`

Final heights: pickup body 1408pt · content column 3621pt · wrapper 3719pt.

---

## Components discovered this session

| Component | COMPONENT_SET key | Notes |
|---|---|---|
| BOL Sets | `7779808908547ec48d7e6c405dd85362da1283ae` | UIKit page "----- Outlines" |
| Tile Outlines | `55dc441e5b673e86649c37a77e3d31fd52716e33` | UIKit page "----- Damages" — NOT used; BOL Sets used instead |
| Damage-Marker | `be7ad9bb1d0e903165fb8964f8c289a6df9d0621` | UIKit page "----- Damages"; `Letter#608:2` TEXT property |
| Section/Title text style | `5d2dabf43d150caa206dbe73784ea6b0e2597f6b` | Used for Additional Info title |

---

## Patterns confirmed

### No `Show Leading` on Collapse/Expand
The component has no `Show Leading` boolean property. To suppress "+" set `Leading#1584:3 = " "` (space), not empty string.

### Absolute-layout wrapper for outline + markers
BOL outline wrapper must be a plain FRAME (not `createAutoLayout`) so markers can be placed at absolute x/y. Set `layoutSizingHorizontal = "FILL"` after appending to the auto-layout parent body.

### Always check `primaryAxisSizingMode` after inserting tall content
Any body frame that was built with a fixed height will clip new tall children (like a 609pt outline). After inserting: set `primaryAxisSizingMode = "AUTO"` + `layoutSizingVertical = "HUG"` up the ancestor chain until the wrapper.

---

Back to [[Driver App/Driver App|Driver App]] · [[Driver App/Vehicle Details Screen|Vehicle Details Screen]] · [[Sessions]]
