---
status: done
type: screen-spec
figma_node: "1:31606"
figma_file: yhxCSzJrafZbqXGZOCBCKE
ds_rebuild_node: "626:20818"
orientation: landscape
dimensions: 852×393
reviewed_against: DS2 tokens + UIKit components
---

# Take Photo Screen

Landscape-orientation camera screen used when a driver captures a photo of a vehicle or load. The UI is designed for landscape mode (852×393). The phone is held sideways; the layout uses 90° rotated elements to position the controls correctly.

**Figma (original):** https://www.figma.com/design/yhxCSzJrafZbqXGZOCBCKE/HaulEx-Driver-App?node-id=1-31606
**Figma (DS rebuild):** node `626:20818` on DS page

---

## Layout structure

```
┌──────────┬──────────────────────────────────────────┬───────────┐
│  Left    │                                          │  Controls │
│  Panel   │         Camera Viewfinder                │  Drawer   │
│  116px   │              740×393                     │   162px   │
│          │   Cancel btn (top-left)                  │ Thumbnail │
│ Status   │   Zoom Pill (right side of viewfinder)   │  Shutter  │
│  Icons   │   Driver View pill (bottom center)       │  Actions  │
│  Flash   │                                 Handle → │           │
└──────────┴──────────────────────────────────────────┴───────────┘
```

The Controls Drawer **overlaps** the right portion of the viewfinder with a dark gradient overlay.

---

## Elements & DS token mapping

### Left Panel (Inspection Container) — 393×116 rotated 90°

| Element | Token |
|---|---|
| Panel background | `Camera/Surface` |
| Inspection icon (truck + badge) | `Background/Primary Yellow` |
| Flash icon | `Camera/Icon Primary` |
| Status bar | `Status Bar - iPhone` component (from UIKit) |

### Camera Viewfinder

| Element | Token / Note |
|---|---|
| Photo background | CameraPhoto component — `Aspect=Full` |

### Zoom Pill — 81×30 rotated 90°

| Element | Token |
|---|---|
| Pill background | Semi-transparent dark overlay |
| Active zoom label ("1x") | `Background/Primary Yellow` |
| Inactive zoom labels ("0.5", "2") | `Camera/Icon Secondary` |
| **Pending swap** | Replace with `ZoomPill` UIKit component (`46f4a223...`) once SF Pro Text font available in file |

### Cancel Button — 72×44

| Element | Token |
|---|---|
| Background | `Background/Mono` |
| Radius | `Radius/S` (8pt) |
| Label | `Text/Primary Inverse Static` |
| **Fixed from** | Wrong `var(--all/button-3, #6b7280)` → now `Background/Mono` |

### Driver View Mode Pill — 112×32

| Element | Token |
|---|---|
| Background | `Background/Mono` |
| Radius | `Radius/M` (12pt) |
| Label | `Text/Primary Inverse Static` |
| **Fixed from** | Wrong `var(--black, #101010)` → now semantic token |
| Variants needed | Driver View / Passenger View / Front / Rear (see [[Component Status]]) |

### Controls Drawer — 393×162 rotated 90°

| Element | Token / Component |
|---|---|
| Gradient overlay | Dark overlay: transparent → 85% opacity `Camera/Surface` |
| Shutter button | ShutterButton UIKit component (`abae92c1...`) — **pending font fix** |
| Photo thumbnail | Last photo taken (image fill); dark `Background/Mono` placeholder |
| Yellow action button | `Background/Primary Yellow` — **fixed from** `var(--yelow, #faca15)` typo |
| Gray action button | `Background/Mono` — **fixed from** `var(--all/button-3, #6b7280)` |

### Drag Handle — 37×393 rotated 90°

| Element | Token |
|---|---|
| Handle bar | `Text/Primary Inverse Static` (white pill) |

---

## Token violations fixed in DS rebuild

| Element | Before (wrong) | After (correct DS token) |
|---|---|---|
| Cancel button bg | `#6b7280` (not in DS neutral scale) | `Background/Mono` |
| Driver View pill bg | `var(--black, #101010)` | `Background/Mono` |
| Yellow action button | `var(--yelow, #faca15)` ← typo | `Background/Primary Yellow` |
| Gray action button | `var(--all/button-3, #6b7280)` | `Background/Mono` |
| Zoom 1x active | Raw yellow | `Background/Primary Yellow` |

---

## Component swaps pending (blocked on SF Pro Text font)

The following UIKit components should replace the ad-hoc versions once `SF Pro Text` is available in the Driver App Figma file:

| Current ad-hoc element | UIKit component to use | Component key |
|---|---|---|
| Zoom level group | `ZoomPill` | `46f4a223f2b8d8285ad8ec386eed1573174c9e0c` |
| Shutter boolean op | `ShutterButton` | `abae92c1de8aa8f034ee98394b44f5a5c698c025` |
| Bottom drawer | `CameraBottomBar` | `b7f1ce904bebbe76a6d28f1a5c75ada1e3391ab0` |

---

## New components identified (add to [[Component Status]])

- **Mode Label Pill** — "Driver View" / "Passenger View" text chip. Needs: Background/Mono bg, Text/Primary Inverse Static label, Radius/M, multiple mode variants.

---

## States to design (not yet done)

- [ ] Taking photo (shutter active, ring animation)
- [ ] Photo taken — review state (confirm/retake)
- [ ] No photos yet (empty thumbnail state)
- [ ] Flash on state
- [ ] Different mode label variants (Passenger View, Front, Rear)

Back to [[Driver App]].
