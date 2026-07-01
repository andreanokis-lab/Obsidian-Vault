# 2026-06-29 — Native iOS 18 photo viewer wireframes

## Context

Reviewed the existing photo screens in the Driver App Figma file and called them out as un-native for iOS 18:
- `298:33837` "Image View (Done)" — portrait, single attached photo viewer
- `1:31700` "Gallery (Done)" — landscape, multi-photo gallery from the Camera Capture Flow

Specific complaints:
- Solid `Background/Primary` nav bar pushing the photo down instead of a translucent overlay
- Grey `Background/Tretiary` (#404040) backdrop behind the photo instead of pure black
- Bare chevron back button with no label
- Landscape gallery rotated system chrome 90° onto a left rail instead of putting it at the top edge of the landscape canvas
- Vertical thumbnail strip on the right (non-native — Photos.app uses a horizontal filmstrip at the bottom)
- Position Label floating as a badge over the photo instead of being promoted to subtitle in the chrome
- No `Done` / `<` labeled back, no `•••` menu, no Share / Info / Delete toolbar

## Decisions

- Adopt **native iOS 18 Apple Photos.app pattern** for both screens
- Codify as a new pattern: [[Design System/Patterns/Photo Viewer Pattern]]
- The pattern has **two variants sharing one shell**:
  - **Single photo (portrait)** — leading `< Previous`, trailing `•••`, bottom toolbar `Share · Save · Info · Delete`
  - **Gallery (landscape)** — leading `Done`, trailing `•••`, bottom toolbar with horizontal filmstrip + `Share · Heart · Info · Trash`
- For the landscape gallery specifically: chose **Path A (fully native Apple)** over Path B (HaulEx hybrid that kept a side-mounted filmstrip). The hybrid was rejected because the side strip isn't an iOS pattern — Photos.app uses a bottom filmstrip in both orientations.

## Built

Two wireframe frames placed in the Driver App Figma file on the Legacy page:

| Frame | Node | Location |
|---|---|---|
| **Gallery (Path A) — Native iOS 18 / Wireframe** | `1159:10598` | Section 737:20442 "Take a photo", at `(2184, 553)` — directly below legacy `1:31700` |
| **Image View (Path B) — Native iOS 18 / Wireframe** | `1161:10598` | Section 667:31695 "Image View", at `(553, 80)` — directly right of legacy `298:33837` |

Both are wireframe-level: primitive shapes + Inter text + unicode glyph icons (↑ ♡ ⓘ 🗑). Production builds would swap in real SF Symbol icons and UIKit Button (Ghost, Icon Only) component instances.

## Vault changes

- New: [[Design System/Patterns/Photo Viewer Pattern]]
- Updated: [[Design System/Patterns/Patterns]] index — added Photo Viewer row
- Updated: [[Hub]] — added Photo Viewer to HaulEx-specific patterns line
- Updated: [[Design System/Design System]] — added Photo Viewer to Patterns list
- Updated: [[Driver App/Take Photo Screen]] — added "Related — photo viewer" section linking to the new pattern + wireframe node IDs

## Open

- Decide whether to promote either wireframe to a full DS rebuild (move from Legacy page to DS page, use real UIKit component instances, bind to Camera tokens). Both are currently wireframe-only.
- Decide whether to actually consolidate the two variants into a single Photo Viewer component with `Orientation` and `State` variant props — feasible since 80% of the shell is shared.
