# Take Photo Screen Pattern

The static composition of the camera screen — top bar + viewfinder + zoom + actions + bottom bar. This pattern defines **what's on the screen**; for the full capture flow (entry → review → attach) see [[Camera Capture Flow]]. For the always-dark visual tokens see [[Foundations/Camera Tokens|Camera Tokens]].

- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit)
- **Reference composition:** `----- Camera` page (`1182:544`) in UIKit
- **Figma documentation:** Section `1802:10457` "Take Photo Screen Pattern — Documentation" on the `----- Patterns` page

---

## Layout

Full-screen, dark, with controls layered on top of a live camera viewfinder.

```
┌─────────────────────────────┐
│  ╳   [mode label]     ⚡    │  ← Camera Top Bar
│                              │     close · mode chip · flash
│─────────────────────────────│
│                              │
│                              │
│                              │
│       [Viewfinder            │
│        Overlay]              │  ← Live camera feed + crop guides
│                              │
│                              │
│                              │
│        [Zoom Pill]           │  ← 0.5× · 1× · 2× selector
│                              │
│   ◐   [Camera Actions]   ◑   │  ← Aspect / mode chips (4:3, 16:9, Square, Full)
│─────────────────────────────│
│                              │
│   [thumb]    ⬤    [↻ flip]  │  ← Camera Bottom Bar
│   (last)  Shutter  switch    │
└─────────────────────────────┘
```

---

## Anatomy

| Region | Component (organism / molecule / atom) | Bindings |
|---|---|---|
| Top bar | Camera Top Bar (organism) | fill `Camera/Controls Background` · icons `Camera/Icon Primary` |
| ↳ Close (leading) | Icon button | `Camera/Icon Primary` (white) |
| ↳ Mode label / chip (center, optional) | Custom chip | text `Camera/Icon Primary` |
| ↳ Flash toggle (trailing) | Icon button | `Camera/Icon Primary`; `Camera/Icon Secondary` when off |
| Viewfinder | Viewfinder Overlay (organism) + CropOverlay (molecule) | Crop guides on `Camera/Overlay` scrim |
| Zoom selector (above actions) | [[Components/ZoomPill (skipped)\|ZoomPill]] (atom) | `Camera/Surface` pill · selected level highlighted with `Background/Primary Yellow` |
| Aspect / mode chips | [[Components/CameraActions (skipped)\|CameraActions]] (molecule) | Chips on `Camera/Surface` |
| Bottom bar | Buttom Bars Camera (organism) | fill `Camera/Controls Background` |
| ↳ Last-photo thumbnail (leading, optional) | [[Components/CameraPhoto (skipped)\|CameraPhoto]] (molecule) | rounded square thumbnail |
| ↳ Shutter (center) | [[Components/ShutterButton (skipped)\|ShutterButton]] (atom) | 72×72 · ring + core `Camera/Icon Primary` |
| ↳ Switch camera (trailing) | Icon button | `Camera/Icon Primary` |

The `(skipped)` markers refer to atoms / molecules from Phase 2 that were deferred — their composition appears here as a pattern even though the individual atom docs don't exist yet.

---

## Composition rules

| Rule | Value |
|---|---|
| Background | Always `Camera/Controls Background` or live viewfinder — never light |
| Top bar height | iOS standard ~94pt (status bar + 44pt) |
| Top bar padding (horizontal) | `Space/L` (16pt) |
| Bottom bar height | ~120pt + safe area |
| Bottom bar padding | `Space/L` × `Space/M` |
| Shutter button position | Centred horizontally in bottom bar |
| Thumbnail tap target | `Space/TapTarget` (44pt) — even if visible is smaller |
| Zoom pill position | Just above Camera Actions, centred |
| Camera Actions position | Above bottom bar, centred — mode chips are scannable |
| Safe area | Respect top + bottom safe areas; controls never overlap status bar / home indicator |

---

## Modes

The screen supports several capture modes selected via [[Components/CameraActions (skipped)\|CameraActions]] chips:

| Mode | Aspect | Use for |
|---|---|---|
| `4:3` | Standard photo aspect | Default — receipts, BOL, evidence |
| `16:9` | Widescreen | Document scanning, wide signs |
| `Square` | 1:1 | Profile pictures, social-style |
| `Full` | Full sensor | Maximum framing flexibility |

Mode selection is reflected in the viewfinder's CropOverlay guides.

---

## Zoom

[[Components/ZoomPill (skipped)\|ZoomPill]] supports 3 levels: 0.5× · 1× · 2× — matching iOS camera defaults. Tapping cycles through; long-press opens a fine-zoom slider (system behaviour, not a DS component).

---

## Top bar — what to put where

| Slot | Content | Notes |
|---|---|---|
| Leading | Close (`✕`) | Always present — dismisses without capturing |
| Center | Mode label / context chip | Optional — only when the capture has a domain context ("Driver signature", "VIN scan") |
| Trailing | Flash toggle | Optional — only when flash makes sense (low-light evidence). Hide for VIN / barcode scans |

Add scan-specific affordances (barcode brackets, search icon) inside the Viewfinder Overlay, not the Top Bar — the Top Bar is for system-level controls.

---

## Real Driver App screens using this pattern

Verified against the Driver App DS page on 2026-05-21. See [[_Pattern Evidence Map]].

| Screen | Section | Notes |
|---|---|---|
| Take a Photo (Done) | Receipts `662:30759` | Receipt capture — standard layout |
| Аdd Photo Receipts (Done) | Receipts `662:30759` / Adjustments `737:21382` | Multi-photo with thumbnail strip |
| Camera (Done) | Truck Service `662:30875` | Service photo capture |
| Multiple Photos (Done) | Truck Service `662:30875` | Multi-photo with thumbnail strip |
| Add Photo (Done) | Adjustments `737:21382` | Adjustments photo |
| Scan VIN (Done) | Scan VIN `736:40323` | Same layout with scanner brackets in Viewfinder |
| Scan VIN + Input (Done) | Scan VIN `736:40323` | Manual-input fallback overlay |
| Take a photo section | `737:20442` | Referenced canonical layout (empty section pointing to UIKit composition) |

---

## Do

- ✅ Always use `Camera/*` tokens — the screen is locked to dark.
- ✅ Place the Shutter button at the horizontal centre of the bottom bar — iOS HIG.
- ✅ Show the last-photo thumbnail when the user is in a multi-capture flow.
- ✅ Use the Mode label / context chip only when the capture has clear domain context.
- ✅ Show scanner brackets inside the Viewfinder for scan flows (VIN, barcode), not in the Top Bar.
- ✅ Respect the safe area — controls never overlap status bar or home indicator.

## Don't

- ❌ Don't put a Navigation Bar on the camera screen — use the Camera Top Bar with Close (`✕`).
- ❌ Don't use mode-aware tokens (`Text/Primary`, `Background/Subtle`) inside the camera — they break the always-dark behaviour.
- ❌ Don't move the Shutter button off-centre — it's the dominant interaction.
- ❌ Don't stack two affordances in the same Top Bar slot.
- ❌ Don't auto-flash without showing the flash toggle — drivers may be in a context where flash is inappropriate.

---

Back to [[Patterns]] · [[Design System]].
