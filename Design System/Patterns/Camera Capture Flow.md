# Camera Capture Flow

The user-facing flow for capturing one or more photos inside the Driver App — entry point → camera screen → review → attach. Used wherever the driver needs to attach photographic evidence (receipts, deposit slips, BOL damages, profile picture, VIN scan, truck service photos).

For the static composition of the camera screen itself (top bar, viewfinder, bottom bar layout), see [[Take Photo Screen Pattern]].
For the visual tokens used by camera UI, see [[Foundations/Camera Tokens|Camera Tokens]].

- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit)
- **Figma documentation:** Section `1798:10288` "Camera Capture Flow — Documentation" on the `----- Patterns` page

---

## Flow stages

The flow is **5 stages**. Not every entry uses every stage — single-photo flows skip Multi-photo.

```
1. Entry point  →  2. Camera screen  →  3. Capture  →  4. Review (+ Crop)  →  5. Attach to record
                                            ↓
                                     [Multi-photo loop]
```

| Stage | Components / Patterns |
|---|---|
| 1. Entry point | Action Section trailing button · Trailing-Icon list row · "+ Add" floating action |
| 2. Camera screen | [[Take Photo Screen Pattern]] · uses `ShutterButton`, `ZoomPill`, `CameraActions`, `CameraPhoto` |
| 3. Capture | Tap `ShutterButton` (single) or tap repeatedly (multi-photo batch) |
| 4. Review (+ Crop) | `CropOverlay` molecule · accept / retake actions |
| 5. Attach | Confirmation toast + return to originating screen |

---

## Camera tokens — always dark UI

Camera UI is **locked to dark** regardless of system appearance — see [[Foundations/Camera Tokens|Camera Tokens]] for the rationale (viewfinder contrast, OLED battery, lens-flare avoidance).

| Surface | Token |
|---|---|
| Backdrop scrim behind controls | `Camera/Overlay` (50% black) |
| Top / bottom bar fill | `Camera/Controls Background` (#0D0D0D) |
| Capture pill / mode chip surface | `Camera/Surface` (#1A1A1A) |
| Primary icons (shutter, flash, switch) | `Camera/Icon Primary` (white) |
| Disabled / secondary icons | `Camera/Icon Secondary` (mid-grey) |

Don't use mode-aware tokens (`Background/Subtle`, `Text/Primary`) inside the camera screen — they break the always-dark behaviour.

---

## Entry points — match to the originating context

| Originating context | Entry pattern | Where |
|---|---|---|
| Single photo (e.g., profile picture) | Action row tap → camera | `Picture (Done)` — Profile |
| Photo evidence in a list | Trailing "+ Add" or "+" icon button | Receipts list, Adjustments, Damages |
| Required step in a workflow | Push from the workflow step | Receipts Add COP/COD → Take a Photo, BOL inspection → Take a photo |
| Scan-with-recognition (VIN, barcode) | Push from scan trigger; falls back to manual input on failure | Scan VIN flow |
| Multi-photo batch | "Add photos" entry that opens camera in multi-capture mode | Add Photo Receipts, Multiple Photos |

---

## Single-photo vs multi-photo

| Mode | Behaviour |
|---|---|
| **Single-photo** | One capture → Review screen → Accept → return to originator with the photo attached |
| **Multi-photo batch** | One capture → thumbnail appended to a strip → camera stays open for next capture → "Done" returns the batch |

Multi-photo flows are appropriate when the driver collects related evidence quickly (e.g., damage walk-around). Single-photo is appropriate when each capture is meaningful on its own (profile picture, VIN, receipt).

---

## Library picker — alternative entry

Some flows offer a library picker alongside the camera entry. The library is the iOS system picker (`PHPicker`), not a designed component.

Pair the library with the camera when:
- The driver may have a pre-existing photo (e.g., a previous receipt scanned earlier)
- Field conditions make camera capture unreliable

Don't offer library picker for VIN scan or live evidence (BOL damages must be captured live — the integrity rule).

---

## Permissions

iOS requires camera + photo library permission grants. The Driver App should:
- Show the OS permission prompt **only on first capture attempt**, not on app launch
- If denied, show an inline [[Error State Pattern]] explaining how to enable in Settings
- Permission denied is not "feature broken" — provide library picker as a fallback when possible

---

## Real Driver App screens using this flow

Verified against the Driver App DS page on 2026-05-21. See [[_Pattern Evidence Map]].

| Screen | Section | Flow type |
|---|---|---|
| Take a Photo (Done) | Receipts `662:30759` | Single-photo, attached to receipt |
| Аdd Photo Receipts (Done) | Receipts `662:30759` · Adjustments `737:21382` | Multi-photo batch |
| Camera (Done) | Truck Service `662:30875` | Single-photo, attached to service entry |
| Multiple Photos (Done) | Truck Service `662:30875` | Multi-photo batch |
| Add Photo (Done) | Adjustments `737:21382` | Photo evidence for adjustments |
| Сhoose from Library (Done) | Adjustments `737:21382` | Library picker alternative |
| Picture (Done) | Profile `667:31697` | Single-photo, profile avatar |
| Scan VIN (Done) | Scan VIN `736:40323` | Recognition capture with fallback |
| Scan VIN + Input (Done) | Scan VIN `736:40323` | Manual fallback after scan failure |

---

## Do

- ✅ Use `Camera/*` semantic tokens for everything inside the camera UI — never mode-aware tokens.
- ✅ Match the flow mode (single vs multi) to the driver's collection intent.
- ✅ Provide library picker as a fallback for receipt-style evidence, but not for live integrity captures (BOL, VIN).
- ✅ Request camera permission only on first attempt — not on app launch.
- ✅ After capture, route to the review / crop stage before attaching — give the driver one chance to retake.
- ✅ On scan failure (VIN), provide a clear manual-input fallback ([[Scan VIN + Input]]).

## Don't

- ❌ Don't reuse mode-aware tokens inside the camera screen — `Camera/*` tokens exist precisely so the UI stays dark.
- ❌ Don't skip the review stage for single-photo captures — drivers need a retake escape hatch.
- ❌ Don't request camera permission proactively — wait for the first capture.
- ❌ Don't trap the user when permission is denied — provide the library picker fallback or an inline error with a Settings link.
- ❌ Don't mix single-photo and multi-photo modes in the same entry point without making the difference clear.

---

Back to [[Patterns]] · [[Design System]].
