# Photo Row

Full-bleed horizontal strip of photo thumbnails with an add-photo tile. Used wherever a driver attaches photos to a record — receipts, truck service requests, claims, adjustments, deposit slips.

Its reason to exist is **interaction headroom**, not layout: a photo tile scales up when iOS lifts it for a context menu on long-press, and it needs slack inside its scroll container or the lift gets clipped. That slack lives here, in the row — never inside [[Components/Image|Image]]. See [[Rules#L6]].

- **Component set node:** `2259:4198`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=2259-4198)
- **Figma section:** `Photo Row — Documentation` (`2259:4111`) on `----- Image Content`
- **Status:** ✅ built & published — **16 live instances** in the Driver App (2026-09-17). See [[Component Status]].

---

## Composition

Horizontal auto-layout frame containing [[Components/Image|Image]] instances (`Format=Square`). The first tile is the add-photo affordance; the rest are photos.

| Layer | Bindings |
|---|---|
| Container (FRAME) | padding `Space/L` leading + trailing · `Space/S` top + bottom · gap `Space/S` · clip content **off** · no fill |
| Add Tile ([[Components/Image\|Image]]) | `Placeholder=true` · `Icon` swapped to `Icons/camera-fill` (md, 32) |
| Photo 1…6 ([[Components/Image\|Image]]) | image fill per instance; empty shows `Background/Subtle` |

The asymmetric padding is deliberate:

| Edge | Token | Why |
|---|---|---|
| Leading / trailing (`Inset=Screen`) | `Space/L` (16) | doubles as the screen margin — the first tile still lands on the 16pt grid ([[Rules#L2]]) while the scroll container runs edge to edge |
| Top / bottom | `Space/S` (8) | pure headroom — absorbs a lift up to ~1.18× on an 88pt tile, ~1.14× on a 112pt tile. Apple publishes no lift factor, so this is a DS-chosen margin, not an HIG number ([[Rules#L6]]) |

---

## Variants

| Axis | Values | Notes |
|---|---|---|
| `Tile` | `M` (88pt tiles) · `L` (112pt tiles) | Matches the two [[Components/Image\|Image]] sizes used for photo thumbnails |
| `Inset` | `Screen` · `Column` | **Where the row lives.** `Screen` = full-bleed, 393 wide, `Space/L` leading/trailing. `Column` = inside the 361pt content column, hug width, **no** horizontal padding — the column's own 16pt margin already does that job. |

4 variants. There is no `S` variant — 56pt tiles are list-row thumbnails, not photo strips.

Pick `Inset` by asking where the row sits: directly under the nav bar, free of the content column → `Screen`; nested in a form column or bound to a caption → `Column`. Getting it wrong shows immediately — `Screen` inside the column pushes tiles to 32pt, `Column` at screen level pulls them to 0.

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Show Add Tile` | BOOLEAN | true | The camera tile that opens capture / library |
| `Show Photo 1` | BOOLEAN | true | Photo slot |
| `Show Photo 2` | BOOLEAN | true | Photo slot |
| `Show Photo 3…6` | BOOLEAN | false | Additional slots — same 6-slot convention as [[Components/Menu\|Menu]] |

Set image fills directly on the nested [[Components/Image\|Image]] instances. Don't detach ([[Rules#C2]]).

---

## Placement

Place as a **full-width child of the screen stack** (`Width=Fill`), not inside the 16pt-inset content column. The row supplies its own 16pt inset, so the tiles line up with everything else while the scroll container keeps room on every edge.

Because the row carries 8pt of its own vertical inset, **reduce the surrounding stack gap by 8** to keep the optical rhythm — a stack gap of `Space/S` (8) around this row reads as the usual 16.

When the row is bound to a caption or a section title that must travel with it (e.g. "Damage Photos", "Press and hold the image to remove it."), keep it inside the labelled group and apply the vertical inset only — the column's existing 16pt margin already supplies the horizontal room.

---

## Code contract

Hand this to engineering with the screen:

- Horizontal `ScrollView`, **full screen width**, `clipsToBounds = true`
- `contentInset` / content margins: **16 horizontal, 8 vertical**
- Tile `cornerRadius` 8 (`Radius/S`), tile clips its own image
- The context-menu lift happens on the tile; the inset is what keeps it inside the scroll bounds

Reported by engineering 2026-09-17: *"The photo container requires internal padding to give the element enough room to scale up on context menu trigger without clipping. All similar screens need to follow this pattern."*

---

## Do

- ✅ Use for any horizontal strip of attached photos.
- ✅ Keep the add tile first — it's the only tile without a context menu, so the leading edge never needs lift room.
- ✅ Place full-bleed with `Width=Fill`; let the component own the 16pt margin.
- ✅ Drop the surrounding stack gap to `Space/S` so the 8pt inset doesn't read as extra space.

## Don't

- ❌ Don't put the headroom inside [[Components/Image\|Image]] — padding there is *visible*, inflates the gap between tiles from 8 to 24, and grows all ~197 unrelated instances (list thumbnails, avatars).
- ❌ Don't nest this row inside the 16pt content column and then add horizontal padding — the tiles end up at 24pt and break [[Rules#L2]].
- ❌ Don't turn on clip content. The row must not clip; only the scroll view does, in code.
- ❌ Don't use it for the vertical camera film strips (`Image View`, `Take a photo`) — different shape, different pattern.

---

## Known gaps vs reference / HIG

- **No HIG basis for the 8pt.** Apple's HIG covers context menus qualitatively — system gesture, shows a preview of the item — and specifies nothing about how far the preview lifts or how containers should reserve room. The inset here is derived from the `Space/*` ladder and from the engineering report, not from Apple. Checked 2026-09-17.
- **HIG rules this component does satisfy:** 44pt minimum touch target (tiles are 88/112pt), `Space/L` screen margin preserved in both `Inset` modes, and "leverage system gestures, don't reinvent them" — long-press on a content object is the system gesture, which is also why [[Patterns/Context Menu Pattern|Context Menu Pattern]] was amended.
- **No add-tile type option.** The add affordance is hardcoded as an [[Components/Image|Image]] with `Placeholder=true`. `Claims · Filled Information` uses a [[Components/Button|Button]] (`Type=Tile, Icon Only`) instead and therefore could not be swapped.
- **375pt width — checked 2026-09-17 ([[Rules#L3]]).** `Inset=Screen` instances are set to `Width=Fill`, so they track the screen down to 375pt. `Tile=L` is the constraint: three 112pt tiles + two 8pt gaps = 352pt against 343pt of available column at 375pt, so the third tile falls off-screen on an iPhone SE / mini. That is **correct for a scroll strip** — the row scrolls and the clipped third tile is the scroll affordance — but it only works if engineering actually implements the horizontal ScrollView in the Code contract above. If a screen renders this row as a static stack, it breaks at 375pt. The Figma frames are 393pt so the overflow is invisible in the mock.
- **Not validated in Dark mode** — the instances inherit semantic tokens so no drift is expected, but it hasn't been eyeballed ([[Rules]] QA checklist).

## Follow-ups

- [ ] Add an add-tile type option (Image placeholder / Button tile) so `Claims · Filled Information` can be swapped.
- [ ] Build `Photo Grid` for the Content-based inspection grids — they carry the insets by hand today ([[Component Status]]).
- [ ] Ask engineering for the measured lift factor and replace the estimate in [[Rules#L6]].
- [ ] Re-publish the UIKit library — the `componentPropertyReferences` wiring on the `Inset=Column` variants was repaired after the first publish.
- [ ] QA the 16 instances in Dark mode.
- [ ] Confirm with engineering that every `Tile=L` row is a real horizontal ScrollView — it overflows by 9pt at 375pt width and depends on scrolling to degrade correctly.

## Not this component: the inspection photo grids

Five screens show photos as a **grid of [[Components/Content|Content]] instances** (112pt tile + caption + status badge), not as a strip of bare [[Components/Image|Image]] tiles: `BOL (Done)`, `Inspection Review (Done)`, `Inspection (Splits) (Done)`, `Customer Review`, `Vehicle Details`.

They have the same long-press problem and got the same **`Space/S` vertical inset** treatment on their row containers (2026-09-17), plus `clipsContent` turned **off** on the Vehicle Details `photo grid` wrappers and their `cell` frames — those were clipping their own tiles outright.

Photo Row does **not** cover them — it nests Image, they nest Content. A `Photo Grid` component (Content-based, wrap layout, same insets) is the proper home for that rule. Filed as 📋 Planned in [[Component Status]].

---

## Screens using it

Applied across the Driver App `DS` page 2026-09-17 — **35 photo containers in ~21 screens**.

**Photo strips (2–3 tiles):** Truck Service · Multiple Photos · Collect Payment (Photo) · Receipts ×5 (Add COP/COD, Payment Type, Orders, Category, Take a Photo) · Deposit Slip · Claims · Filled Information · Adjustments ×2 · Adjustment (Done).

**Single photo tiles** — same rule, a lone tile is still long-pressable: Truck Service · Add Truck Services · Sheet · Photo Actions · Receipts · Accepted Receipt · Receipts · Deleting Image (Long Press).

**Inspection grids** (Content-based, see above): BOL ×2 · Customer Review ×2 · Inspection (Splits) ×6 · Inspection Review ×6 · Vehicle Details ×2.

**Not swapped — `Claims · Filled Information` (`206:21776`).** Its add affordance is a [[Components/Button|Button]] (`Type=Tile, Icon Only`), not an Image placeholder, and Photo Row only models an Image-based add tile. Swapping would silently replace a Button with a camera tile, so that row keeps the headroom insets by hand. Decided 2026-09-17 — fixing it properly means an add-tile type option on this component; file it before the next photo screen is built.

**Deliberately left alone:**
- The vertical camera film strips — `Image View` (`1189:31937`) and `Take a photo` (`645:20663`). Different shape, camera context, own decision.
- The floating photo on `Deleting Image (Long Press) (Done)` (`186:15458`) — that tile is already *in* the lifted state, sitting above the Overlays scrim next to its Menu. It's the preview layer, so nothing clips it.

Related: [[Components/Image|Image]] · [[Components/Content|Content]] · [[Components/File field|File field]] · [[Patterns/Context Menu Pattern|Context Menu Pattern]] · [[Patterns/Camera Capture Flow|Camera Capture Flow]] · [[Patterns/Photo Viewer Pattern|Photo Viewer Pattern]].

Back to [[Design System]] · [[Component Status]].
