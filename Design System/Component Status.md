# Component Status

Single source of truth for what exists in the HaulEx UIKit library. Check this before drawing anything.

**UIKit Figma:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit)

---

## Status legend

| Icon | Meaning |
|---|---|
| ✅ Built | Component set exists in Figma, documented, ready to use |
| 🔄 In Progress | Being built — specs exist, not yet published to library |
| 📋 Planned | Needed, not started — file a request if you need it sooner |
| ❓ Unknown | Referenced in designs but not confirmed in library |

---

## Atoms (primitive UI elements)

| Component | Status | Figma Node | Note |
|---|---|---|---|
| Avatar | ✅ Built | `1281:4432` | 3 Rank variants (First/Second/Third). Yellow ring on First; neutral on Second/Third. See [[Avatar]]. |
| Badge | ✅ Built | `283:90` | 47 variants across Type × Role × Accent. ~276 production instances. See [[Badge]]. |
| Image | ✅ Built | `449:2627` | 6 variants (3 Size × 2 Format). Circle/Square at 56/88/112pt. See [[Components/Image\|Image]]. |
| Button | ✅ Built | `246:161` | 143 variants. Size × Type × State × Icon Only × Role. ~474 production instances in DS. See [[Button]]. |
| IconButton / Round | 🔄 In Progress | — | Flash, rotate, trash variants. Part of Camera build plan. |
| Input | ✅ Built | `230:56` | 7 variants (Default, Focused, Filled, Negative, Positive, Disabled, Clear). ~159 production instances in DS. See [[Input]]. |
| Text Area | ✅ Built | `257:836` | 5 State variants (Default, Filled, Negative, Positive, Disabled). See [[Text Area]]. |
| Draw Area | ✅ Built | `671:968` | 2 Size variants (S, M). Signature / freehand capture with eraser. See [[Draw Area]]. |
| Divider | ✅ Built | `292:133` | Horizontal / Vertical hairline. See [[Divider]]. |
| Tooltip | ✅ Built | `294:221` | 4 directional variants (Top/Down/Right/Left) + Info popover. See [[Tooltip]]. |
| Vertical Badge | ✅ Built | `387:441` | Green/Red stop markers (pickup/delivery). See [[Vertical Badge]]. |
| Checkbox | ✅ Built | `260:1717` | 3 State variants (Unselected, Selected, Disabled). Square multi-select. See [[Components/Checkbox\|Checkbox]]. |
| Checkmark | ✅ Built | `260:1772` | 3 State variants (Unselected, Selected, Disabled). Radio indicator for single-select. See [[Components/Checkmark\|Checkmark]]. |
| Toggle / Switch | ✅ Built | `268:1861` | 2 State variants (Off, On). iOS-style on/off switch. See [[Components/Toggle\|Toggle]]. |
| Tag / Chip | ✅ Built | `288:981` | 6 variants (2 State × 3 Type). Filter/tag/action pill. See [[Components/Chip\|Chip]]. |
| Counter | ✅ Built | `418:252` | Numeric stepper (minus, count, plus). 1 instance property. See [[Components/Counter\|Counter]]. |
| Tab Item | ✅ Built | `320:3407` | 6 Role variants (Pickup, Deliver, Complete, Normal, Idle, Disabled). See [[Components/Tab Item\|Tab Item]]. |
| Page Control | ✅ Built | `1489:54` | iOS dot indicator for paginated scroll. See [[Components/Page Control\|Page Control]]. |
| Damage-Marker | ✅ Built | `608:162` | 2 Marker variants (Driver yellow, Customer red). 24×24 vehicle-outline marker. See [[Components/Damage-Marker\|Damage-Marker]]. |
| NotificationBadge | 🔄 In Progress | — | Part of Camera build plan |
| PhotoThumbnail | 🔄 In Progress | — | Part of Camera build plan |

---

## Molecules (composed elements)

| Component | Status | Figma Node | Note |
|---|---|---|---|
| List Row | 📋 Planned | — | Needs: primary label, subtitle, leading icon, trailing chevron/action |
| Form Field (labeled input) | 📋 Planned | — | Label + Input + Error message |
| Navigation Bar | 📋 Planned | — | Title + back + trailing action |
| Tab Bar | 📋 Planned | — | 3–5 tab items, active/default state |
| Search Bar | 📋 Planned | — | |
| Section Header | 📋 Planned | — | Title + optional action link |
| Empty State | 📋 Planned | — | Icon + headline + body + optional CTA |
| LeaderboardCard | 📋 Planned | — | Avatar + name + stats. Proposed follow-up on [[Avatar]]. |
| Mode Label Pill | 📋 Planned | — | "Driver View" / "Passenger View" text chip. Background/Mono bg, Text/Primary Inverse Static label, Radius/M. Needs variants: Driver View, Passenger View, Front, Rear. Identified in [[Take Photo Screen]]. |

---

## Camera Components (in progress — do not use in screens yet)

| Component | Status | Figma Node | Note |
|---|---|---|---|
| ShutterButton | 🔄 In Progress | `1182:553` | State=Default / Active |
| ZoomPill | 🔄 In Progress | `1182:737` | State=Default / Active |
| CameraBottomBar | 🔄 In Progress | `1182:4208` | Composes Shutter + Thumbnail + IconButton |
| CameraActions | 🔄 In Progress | `1193:166` | Type=Icons × Count=1/2/3, Type=Text Count=1 |
| CameraPhoto | 🔄 In Progress | `1207:160` | Aspect=4:3 / 16:9 / Square / Full |
| CameraTopBar | 🔄 In Progress | — | Compass + text + Done |
| ViewfinderOverlay | 🔄 In Progress | — | Variants for different capture modes |

See full build plan in [[Components - In Progress]].

---

## Sheets & Overlays

| Pattern | Status | Doc |
|---|---|---|
| Half Sheet (medium detent) | 📋 Planned | [[Sheet Patterns]] |
| Full Sheet (large detent) | 📋 Planned | [[Sheet Patterns]] |
| Stack Button Sheet | 📋 Planned | [[Sheet Patterns]] |
| Action Sheet | 📋 Planned | [[Sheet Patterns]] |

---

## Requesting a new component

When you need something that isn't in this list:
1. Add a row here with status `Planned`
2. Describe what you need in the Note column (variants, states, usage context)
3. Tag it in the next design system sync

---

Back to [[Design System]] · [[Getting Started]].
