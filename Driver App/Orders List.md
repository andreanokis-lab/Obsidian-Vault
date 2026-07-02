---
status: in-progress
type: screen-spec
figma_node: "782:20481"
figma_file: yhxCSzJrafZbqXGZOCBCKE
---

# Orders List

Dev-ready iPhone screen (393×852) inside Section 1 on Page 5 of the Driver App file. Top-level Orders list with status bar, nav bar, segment control filter, scrollable order cards, and tab bar.

**Figma:** https://www.figma.com/design/yhxCSzJrafZbqXGZOCBCKE/HaulEx-Driver-App?node-id=782-20481

## Structure

| Region | Component | Notes |
|---|---|---|
| Status bar | Status Bar - iPhone (DS instance) | 9:41, default iOS treatment |
| Nav bar | Navigation Bar (DS instance) | Title "Orders", back chevron + hamburger menu (back is legacy from cloned screen — confirm with dev whether top-level tab should hide it) |
| Segment control | Segment Control (DS instance) | 3 segments: **All** / **Active** (selected) / **Completed** |
| Content | Order List (vertical FRAME, 361 wide, 706 tall) | 5 Order cards, gap = `Space/L` (16) |
| Order card | [[Card]] component set, `Role=Orders` variant | Detached frames (see Font workaround) |
| Tab Bar | Tab Bar (DS instance) | Home (selected) / Notifications / Profile |

## Cards

Row data — all values plain text inside the card; no per-card variant override.

| # | Vehicle | Origin → Destination | Pickup | Delivery | Ref | Badges | Amount |
|---|---|---|---|---|---|---|---|
| 1 | 2015 Porsche Cayenne | Orchards, WA → Springfield, MA | 9/6 - 9/8 | 9/8 | #10421 | ENCL | $1,540 COD |
| 2 | 2022 Tesla Model Y | Austin, TX → Phoenix, AZ | 9/7 - 9/9 | 9/9 | #10422 | EXP | $1,280 |
| 3 | 2019 BMW X5 | Seattle, WA → Denver, CO | 9/8 - 9/11 | 9/11 | #10423 | ENCL · EXP | $2,150 COD |
| 4 | 2024 Ford F-150 | Dallas, TX → Atlanta, GA | 9/9 - 9/12 | 9/12 | #10424 | EXP | $1,990 |
| 5 | 2020 Audi Q7 | Miami, FL → Newark, NJ | 9/10 - 9/14 | 9/14 | #10425 | ENCL | $1,720 COD |

5th card overflows behind the tab bar — intentional scroll affordance (matches iOS behavior).

## Origin

Built by cloning `Trip Order List Delivery (Done)` (node `1:29438`) from the DS page and adapting:
- Nav title `Trip 15-1013` → `Orders`
- Segment labels `Pickup / Delivery / Completed` → `All / Active / Completed`
- Toast banner removed (no error state on a vanilla list)
- Card list expanded from 3 → 5 with distinct vehicles, routes, dates, payment
- All `SF Pro Text Regular` references rewritten to `SF Pro Regular`

## Font workaround — SF Pro Text not available locally

13 text nodes in the reference screen used **SF Pro Text Regular**, which is not installed on the build host (only `SF Pro` is available — Apple ships `SF Pro Text` and `SF Pro Display` as part of the SF font system; only the unified `SF Pro` family was present). Fresh `createInstance` + `appendChild` failed font validation.

Workaround used:

1. `clone()` reference screen on the DS page (cloning doesn't validate fonts).
2. Walk every TEXT descendant; for each `getStyledTextSegments(['fontName'])` segment with `family === "SF Pro Text"`, call `setRangeFontName(start, end, { family: "SF Pro", style })` after loading SF Pro Regular/Semibold/Medium. `setRangeFontName` requires only the *new* font to be loaded.
3. `section.appendChild(clonedScreen)` — now passes validation because every text node uses `SF Pro`.
4. Customize text via `node.characters = …` (instance text nodes accept direct edits when the new font is loaded).

**Consequence:** the screen is a detached frame, NOT a live composition of DS instances. Nested DS instances (Nav Bar, Tab Bar, Segment Control, Cards) remain live instances *internally*, but the outer screen frame is no longer linked to its source.

## Token & system compliance

| Property | Token |
|---|---|
| Order List `itemSpacing` | `Space/L` (imported via key `d3ef8a06aa255880f408fbb46ecd765b9d2b2a10`) |
| Card surface, divider, icon, text | Inherited from [[Card]] variant — semantic colors via [[Colors - Semantic]] |
| Nav Bar, Tab Bar materials | DS instances — iOS Materials + semantic colors |

No hardcoded hex values.

## Curb weight (2026-07-02)

The `Role=Orders` [[Card]] now carries a **curb weight** field, centered between the pickup/delivery clusters, backed by `Curb Weight` (TEXT) + `Show Weight` (BOOLEAN) props. Order cards in the Driver App are remote library instances of the UIKit component, so this appears here only after the UIKit library is **republished + updates accepted** (pending). See [[Sessions/2026-07-02 orders-card-curb-weight|session note]].

> ⚠️ Node `782:20481` (recorded above) no longer resolves in the Driver App file; Order-card instances now live on screens like "Trips" (`1:28891`) on the DS page. Re-audit this screen's node ref.

## Follow-ups

- **Font**: install `SF Pro Text` on the build host *or* migrate the DS Card / Segment / Nav text styles to use the unified `SF Pro` family. After that, this screen can be rebuilt as live DS instances.
- **Nav back chevron**: confirm with dev whether the Orders top-level tab should hide the back affordance (currently shows the cloned screen's `<` icon).
- **Empty / loading / error states**: not designed yet. See [[Empty State Pattern]], [[Loading Skeleton Pattern]], [[Error State Pattern]] for variants to add.
- **Per-card interaction**: row tap → Order Details. Long-press behavior?
- **Segment behavior**: `All / Active / Completed` are placeholder filters; confirm canonical filter set with PM.

Back to [[Driver App]] · [[Design System]] · [[Card]].
