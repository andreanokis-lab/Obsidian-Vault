# Components — In Progress

Component work pulled from the Camera screen frame in [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=1182-544) (node `1182:544`, section "----- Camera"). Tracked here because they are reusable design-system primitives, not screen-specific.

## Component inventory

| Component | Variants | Figma node |
|---|---|---|
| ShutterButton | `State=Default`, `State=Active` | `1182:553` |
| ZoomPill | `Active=0.5`, `Active=1`, `Active=2` | `1663:134` (set) · variants: `1663:104`, `1663:114`, `1663:124` |
| CameraBottomBar | (single symbol) | `1182:4208` |
| CameraActions | `Type=Icons` × `Count=1\|2\|3`, `Type=Text Count=1` | `1193:166` |
| CameraPhoto | `Aspect=4:3 \| 16:9 \| Square \| Full` | `1207:160` |
| [[Avatar]] | `Rank=1 \| 2 \| 3 \| None` | `1281:4432` (built) |

## Build plan (from Figma sticky `1182:624`)

1. Add missing color + spacing + radius tokens.
2. Build **ShutterButton** with variants `default`, `active`.
3. Build **IconButton / Round** — variants for flash-on, flash-off, rotate, trash via component properties.
4. Build **ZoomPill** + **NotificationBadge** + **PhotoThumbnail**.
5. Build **CameraTopBar** — composes Compas + text + Done.
6. Build **CameraBottomBar** — composes ShutterButton + PhotoThumbnail + IconButton group.
7. Build **ViewfinderOverlay** with variants.
8. Reassemble the 5 Camera screens using proper component instances.

## Screens currently using ad-hoc instances

Section "----- Camera" contains 5 frames at node `1182:554`:
- `Image Viewer` (`1182:555`)
- `Image View` (`1182:561`)
- `add photo receipts` (`1182:568`)
- `deposit slip` (`1182:592`)
- `add photo-step 4` (`1182:608`)

These should be rebuilt against the components above once the build plan is complete.

Back to [[Design System]].
