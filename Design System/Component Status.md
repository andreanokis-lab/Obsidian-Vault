# Component Status

Single source of truth for what exists in the HaulEx UIKit library. Check this before drawing anything.

**UIKit Figma:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit)

---

## Status legend

| Icon | Meaning |
|---|---|
| ✅ Built | Component set exists in Figma, documented, ready to use |
| 🔄 In Progress | Being built — specs exist, not yet published to library |
| 📐 Pattern | Composition rule, not a component — documented in [[Patterns]] |
| 📋 Planned | Needed, not started — file a request if you need it sooner |
| 📋 Native iOS | Use the system control — no DS component planned |
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
| Row Text | ✅ Built | `448:2970` | 2 Tone variants (Default, Destructive). Primary + helper text block for list rows. See [[Components/Row Text\|Row Text]]. |
| Trailing (Content Row) | ✅ Built | `416:222` | 5 Types (Picker, Toggle, Segment, Trailing-Icon, Count). See [[Components/Trailing (Content Row)\|Trailing (Content Row)]]. |
| Trailing (Action Section) | ✅ Built | `475:1102` | 3 Types (Icon, Text, Icon-chevron). See [[Components/Trailing (Action Section)\|Trailing (Action Section)]]. |
| Trailing (Sheets) | ✅ Built | `442:10099` | 2 Types (Circle Button, Text Button). See [[Components/Trailing (Sheets)\|Trailing (Sheets)]]. |
| Trailing (Image Content) | ✅ Built | `535:669` | 2 Status variants (Success, Error). See [[Components/Trailing (Image Content)\|Trailing (Image Content)]]. |
| Leading (Sheets) | ✅ Built | `442:10216` | 2 Types (Circle Button, Text Button). Mirror of Trailing. See [[Components/Leading (Sheets)\|Leading (Sheets)]]. |
| List | ✅ Built | `944:4339` | 2 Views (List, Preview Row). Generic list row with Row Text + Trailing slot. See [[Components/List\|List]]. |
| Content Row | ✅ Built | `1008:3542` | 7 variants × Receipts/Trackshop/Adj./Truck Service/Deposit slip with Long Press states. See [[Components/Content Row\|Content Row]]. |
| List / Grid | ✅ Built | `939:4248` | Card-style grid tile with image + title + helper + progress. See [[Components/List Grid\|List / Grid]]. |
| Leaderboard Row | ✅ Built | `1297:250` | Rank + avatar + name + stats. For positions 4+. See [[Components/Leaderboard Row\|Leaderboard Row]]. |
| File field | ✅ Built | `960:4667` | Thumbnail + filename + helper. For uploads / attachments. See [[Components/File field\|File field]]. |
| Info row | ✅ Built | `342:4031` | Inline label with leading + trailing icons. Used inside Cards. See [[Components/Info row\|Info row]]. |
| Card | ✅ Built | `389:2319` | 7 Role variants (Company, Invoices, Deposit Slip, Stops, Trip-Routes, Requests, Orders). See [[Components/Card\|Card]]. |
| View | ✅ Built | `389:2245` | 2 Views (Basic, Extended) — payment / amount display block. See [[Components/View\|View]]. |
| Range | ✅ Built | `379:716` | 2 State variants (Default, Disabled) — From / To range display. See [[Components/Range\|Range]]. |
| Input Section | ✅ Built | `356:1259` | Compact caption + value pair. See [[Components/Input Section\|Input Section]]. |
| Payment Amount | ✅ Built | `389:862` | Boxed payment breakdown (method + amount rows). See [[Components/Payment Amount\|Payment Amount]]. |
| Select | ✅ Built | `307:1122` | 2 State variants (Default, Focused). Pill that opens a Menu. See [[Components/Select\|Select]]. |
| Menu Item | ✅ Built | `937:4085` | 4 variants (Type × Stroke). Single row inside a Menu. See [[Components/Menu Item\|Menu Item]]. |
| Menu | ✅ Built | `937:4113` | Up to 12 items + 1 destructive. Vertical menu container. See [[Components/Menu\|Menu]]. |
| Collapse / Expand | ✅ Built | `1410:2236` | 2 Detent variants (Full Detent, In Section). Expandable section header. See [[Components/Collapse Expand\|Collapse / Expand]]. |
| List Column Header | ✅ Built | `1324:3` | 3-column header (UNIT · MAKE · MODEL). See [[Components/List Column Header\|List Column Header]]. |
| Segment Control | ✅ Built | `321:1008` | 13 combinations (Selected × Segments × Scrollable). iOS-style segmented control. See [[Components/Segment Control\|Segment Control]]. |
| Controls | ✅ Built | `418:227` | Plus / Minus icon pair for steppers. See [[Components/Controls\|Controls]]. |
| Action Section | ✅ Built | `475:1232` | 2 Type variants (Default, Clear). Section header pill with label + INOP badge + trailing actions. See [[Components/Action Section\|Action Section]]. |
| Content | ✅ Built | `535:721` | 3 Status variants (Default, Success, Error). Image tile + caption + status badge. See [[Components/Content\|Content]]. |
| Titles | ✅ Built | `1282:4616` | 3 Place variants (1st Place, 2nd-3nd Places, Skeleton). Podium name block. See [[Components/Titles\|Titles]]. |
| Places Segments | ✅ Built | `1282:4757` | 2 Place variants (First place, 2-3 Places). Leaderboard podium block. See [[Components/Places Segments\|Places Segments]]. |
| Title and Controls | ✅ Built | `442:9262` | Sheet header bar — title + leading + trailing slots. See [[Components/Title and Controls\|Title and Controls]]. |
| BOL Sets | ✅ Built | `1581:725` | 2 Type variants (Vehicle Set, Motorcycle-Set). BOL inspection outlines. See [[Components/BOL Sets\|BOL Sets]]. |
| Damages | ✅ Built | `607:2217` | 3 State variants (Idle, Driver, Customer). Damage entry chip. See [[Components/Damages\|Damages]]. |
| Tile Outlines | ✅ Built | `1487:67` | 5 Tile variants (Tile1–Tile5). Compact inspection tile canvases. See [[Components/Tile Outlines\|Tile Outlines]]. |
| Alert Section Base | ✅ Built | `659:440` | 6 variants (3 Alert × 2 Stroke). Inline tinted alert container with Slot. See [[Components/Alert Section Base\|Alert Section Base]]. |
| Form Field (labeled input) | 📐 Pattern | — | Owned by [[Form Pattern]] — composes [[Components/Input\|Input]] + Label + Helper. Not a separate component. |
| Section Header | 📐 Pattern | — | Owned by [[Section Header Pattern]] — Plain title, Title + trailing action, or [[Components/Action Section\|Action Section]]. |
| Empty State | 📐 Pattern | — | Owned by [[Empty State Pattern]] — Image + Section/Title text + Body + optional [[Components/Button\|Button]]. |
| Navigation Bar | 📋 Planned (organism) | `299:1823` (instance) | Title + back + trailing action. Used in every pushed screen. Organism note pending. |
| Tab Bar | 📋 Planned (organism) | — | 3–5 tab items, active/default state. See [[Navigation Patterns]] for usage rules. |
| Search Bar | 📋 Planned (organism) | — | Referenced by [[Filter Search Results Pattern]]. Composes [[Components/Input\|Input]] in search variant + leading magnifier + trailing clear. |
| Toast | 📋 Planned (organism) | — | Referenced by [[Error State Pattern]] for non-blocking failures (photo upload, save). |
| Activity Indicator | 📋 Native iOS | — | System spinner per [[Loading Skeleton Pattern]]. No DS component — use `UIActivityIndicatorView`. |
| Date Picker / Time Picker | 📋 Planned | — | Multi-step form flows need this (Order Creation, ETA). Currently composed via [[Components/Input\|Input]] + sheet. |
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

The Sheet itself is an organism with no individual component note — composition is documented at the pattern level. Header slot components ([[Components/Title and Controls|Title and Controls]], [[Components/Leading (Sheets)|Leading (Sheets)]], [[Components/Trailing (Sheets)|Trailing (Sheets)]]) are documented individually.

| Variant | Status | Doc |
|---|---|---|
| Half Sheet (medium detent) | 📐 Pattern | [[Sheet Pattern]] · Variant 1 |
| Full Sheet (large detent) | 📐 Pattern | [[Sheet Pattern]] · Variant 2 |
| Stack Button Sheet | 📐 Pattern | [[Sheet Pattern]] · Variant 3 |
| Action Sheet | 📐 Pattern | [[Sheet Pattern]] · Variant 4 (uses iOS native `UIAlertController`) |

---

## Requesting a new component

When you need something that isn't in this list:
1. Add a row here with status `Planned`
2. Describe what you need in the Note column (variants, states, usage context)
3. Tag it in the next design system sync

---

Back to [[Design System]] · [[Getting Started]].
