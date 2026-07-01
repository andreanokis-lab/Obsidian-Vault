---
status: proposed
type: pattern
figma_file: yhxCSzJrafZbqXGZOCBCKE
related_legacy_nodes: ["298:33837", "1:31700"]
proposed_native_nodes: ["1161:10598", "1159:10598"]
reviewed_against: iOS 18 Photos.app conventions
---

# Photo Viewer Pattern

Native iOS 18 viewer for any photo the driver has already captured or attached — single-photo view (portrait, e.g. from Order Files or Receipts list) and multi-photo gallery (landscape, the Camera Capture Flow review stage). Both orientations share one shell with two variants.

**Status:** Proposed (2026-06-29). Legacy non-native versions still in place at nodes `298:33837` and `1:31700`. Native rebuild wireframes at `1161:10598` (portrait) and `1159:10598` (landscape) on the Legacy page.

---

## Core principle — translucent chrome over a full-bleed photo

The photo is the subject. Chrome (nav bar + toolbar) overlays it as translucent dark blur so the photo extends edge-to-edge underneath. Tap the photo to toggle chrome on/off for distraction-free viewing.

```
┌─────────────────────────────────────┐
│ ▓ Top translucent chrome  ▓▓▓▓▓▓▓ │  ← UIBlurEffect dark
├─────────────────────────────────────┤
│                                     │
│         Photo (aspect-fit)          │  ← full bleed under chrome
│             bg #000                 │
│                                     │
├─────────────────────────────────────┤
│ ▓▓ Bottom translucent toolbar ▓▓▓▓ │
└─────────────────────────────────────┘
```

---

## Two variants, one shell

| Variant | Orientation | Used for | Leading | Trailing | Bottom toolbar |
|---|---|---|---|---|---|
| **Single photo** | Portrait 393×852 | Viewing one attached photo from a list (Order Files, Receipts, Adjustments) | `< Files` (real previous-screen title) | `•••` ellipsis menu | Action row: **Share · Save · Info · Delete** |
| **Gallery** | Landscape 852×393 | Reviewing multiple captured photos (Camera Capture Flow · Stage 4) | `Done` text button | `•••` ellipsis menu | Horizontal **filmstrip** above action row: **Share · Heart · Info · Trash** |

In both variants the title slot carries a two-line composition: **title** on top, **subtitle / counter** beneath.
- Single photo: `Front Hood` / `River, OR`
- Gallery: `Front Hood · 2 of 4` / `River, OR`

The Position Label that floated as a badge on the legacy gallery is **promoted into the chrome as subtitle** — no more floating badges over photos.

---

## Composition rules

| Element | Spec |
|---|---|
| Photo background | `Camera/Overlay` solid or system `#000`. Never `Background/Tretiary` (#404040) — that grey was the legacy mistake. |
| Photo fit | **aspect-fit**, edge-to-edge. Never aspect-fill / crop. Letterbox bars are pure black. |
| Top chrome fill | `Camera/Controls Background` at ~60% opacity, with `UIBlurEffect dark` material in code |
| Bottom chrome fill | Same — same blur material, same 60–65% opacity |
| Top chrome height | Portrait: 98pt (status bar 54 + title row 44). Landscape: ~58pt total. |
| Bottom toolbar height | Portrait: 100pt. Landscape: 90pt (filmstrip + action row). |
| Title style | `Screen/Title` (17 / 22 / 590) for the title line, `Text/Secondary` for the subtitle line, both on `Text/Primary` (#F2F2F2) |
| Filmstrip thumb | 30×26pt regular, 38×32pt when selected with 1.5pt white inside stroke. 6pt gap. |
| Action row icon | 44pt hit area; icon glyph 22pt, label 11pt `Text/Secondary` beneath |
| Home indicator | Native bottom safe area; chrome extends underneath, action row sits above it |

---

## Behaviors

- **Tap photo** → toggles both chrome strips together (auto-hide for distraction-free viewing)
- **Swipe horizontal** → next / previous photo in the gallery (landscape variant)
- **Pinch / double-tap** → zoom
- **Swipe down on photo** → dismiss (modal pattern, single-photo variant)

---

## Tokens

Uses [[Foundations/Camera Tokens|Camera Tokens]] because this is a viewer of camera-captured content and is locked to dark regardless of system appearance — same rationale as [[Camera Capture Flow]] · "Camera tokens — always dark UI".

Do not use mode-aware tokens (`Background/Subtle`, `Text/Primary`) inside the photo viewer — they break the locked-dark behaviour the way they would inside the camera screen.

---

## Real Driver App entry points

| From | Variant | Why this variant |
|---|---|---|
| Order Files row → tap photo | Single photo (portrait) | One specific document to view |
| Receipts list → tap a receipt photo | Single photo (portrait) | Same |
| Camera Capture Flow · multi-photo batch · "Done" | Gallery (landscape) | Driver needs to scrub through the batch |
| Truck Service · Multiple Photos | Gallery (landscape) | Same |

The **single-photo** variant replaces legacy node `298:33837` "Image View (Done)".
The **gallery** variant replaces legacy node `1:31700` "Gallery (Done)".

---

## Why this is the native pattern

Mirrors Apple Photos.app exactly:
- Translucent dark blur top + bottom over a full-bleed photo
- Top chrome: leading text button · centered title + subtitle · trailing `•••`
- Bottom: filmstrip (when there are siblings) + standard 4-action toolbar (Share / Heart / Info / Trash)
- Tap to toggle chrome

The legacy screens broke from this in three ways: solid (non-translucent) chrome that pushed the photo down, grey `#404040` photo backdrop, and a rotated-portrait status bar / nav rail in landscape. All three are corrected in the proposed wireframes.

---

## Do

- ✅ Use translucent dark blur chrome (`UIBlurEffect dark`) over a full-bleed photo
- ✅ Use Camera tokens — the viewer is locked-dark like the camera
- ✅ Promote photo metadata (position label, date, location) into the title/subtitle slot
- ✅ In landscape, put the filmstrip horizontally at the bottom — not as a side rail
- ✅ Use `Done` (modal dismissal) for the post-capture review; `< Previous` (push dismissal) for attached-photo view from a list

## Don't

- ❌ Don't use solid `Background/Primary` for the chrome — it stops being a viewer and becomes a screen with a header
- ❌ Don't use `Background/Tretiary` (#404040) behind the photo — pure black only
- ❌ Don't aspect-fill the photo — drivers need the whole frame visible
- ❌ Don't rotate system chrome 90° onto a side rail in landscape — the chrome stays at the actual top edge of the landscape canvas
- ❌ Don't float metadata as a badge over the photo — it competes with the photo. Promote it into the chrome.

---

## Related

- [[Camera Capture Flow]] — this pattern is the Review stage (Stage 4) of that flow when the gallery variant is used
- [[Take Photo Screen Pattern]] — the camera screen this flow originates from
- [[Foundations/Camera Tokens]] — the always-dark token set used here

Back to [[Patterns]] · [[Design System]].
