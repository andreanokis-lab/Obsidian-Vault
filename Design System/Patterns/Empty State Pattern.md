# Empty State Pattern

How to fill a screen or list region when there's no data to show. Compose [[Components/Image|Image]] (or an icon), `Section/Title` typography, `Text/Body` typography, and an optional [[Components/Button|Button]] into a centred, scannable empty state.

Covers two sub-cases:
- **Default empty** — user has no data yet (no trips, no loads, no notifications)
- **No results** — user searched / filtered and nothing matched

For loading placeholders see [[Loading Skeleton Pattern]]. For error / offline screens see [[Error State Pattern]]. For search-specific empty results see [[Filter Search Results Pattern]].

- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit)
- **Figma documentation:** Section `1785:9679` "Empty State Pattern — Documentation" on the `----- Patterns` page

---

## Anatomy

Vertical stack, centred in the available content area (below nav bar, above tab bar).

| Element | Component / Style |
|---|---|
| Icon / illustration | SF Symbol or [[Components/Image|Image]] · 56–80pt visual size · fill `Icon/Subtle` |
| Headline | `Screen/Title` (17pt Semibold) text style · fill `Text/Primary` |
| Supporting message | `Text/Body` (17pt Regular) text style · fill `Text/Secondary` · max width 280pt |
| Optional CTA | [[Components/Button|Button]] — Size=M, Type=Primary or Ghost (depending on emphasis) |

---

## Composition rules

| Rule | Value |
|---|---|
| Vertical centring | Centred in available content area (between Navigation Bar and Tab Bar / Safe Area) |
| Icon → Headline gap | `Space/XL` (24pt) |
| Headline → message gap | `Space/S` (8pt) |
| Message → CTA gap | `Space/XL` (24pt) |
| Max message width | 280pt — keep copy comfortable, not edge-to-edge |
| Horizontal margin | `Space/L` (16pt) minimum from screen edges |
| Icon size | 56–80pt — anything bigger takes over the screen |

If the screen has a Search Bar or filter chips above the list, the empty state sits **below** those controls — never replaces them.

---

## Sub-pattern content

### Default empty (no data yet)

- **Icon** — content-type relevant (`tray.fill` for empty inbox, `doc.fill` for no loads, `truck.box` for no trips)
- **Headline** — "No [things] yet" (short, clear)
- **Message** — explain what will appear here or what the user can do
- **CTA** (optional) — show only if there's a clear next action ("Create", "Add", "Invite")

### No results (after search / filter)

- **Icon** — `magnifyingglass` or content-type icon
- **Headline** — "No [things] found" (acknowledges the search context)
- **Message** — "Try adjusting your search or clearing your filters."
- **CTA** — "Clear filters" or "Clear search" — Button Size=M, Type=Ghost, Role=Link. Must meet `Space/TapTarget` (44pt) min height. **Always include — never leave the user stuck with no escape from a failed search.**

For deeper Search Bar + Chip composition rules, see [[Filter Search Results Pattern]].

---

## Vertical positioning rule

Empty states centre in the **available content area**, not the whole screen. Account for:
- Top: status bar + nav bar
- Bottom: safe area + tab bar (if present)

If a search bar or filter chips sit above the list, they remain visible — the empty state lives in the scrollable area below them.

---

## Real Driver App screens using this pattern

- **Company Filter** — Default empty + No results (active search + filters)
- **Load list** — Default empty when no loads assigned
- **Trip history** — Default empty when no completed trips
- **Messages / Notifications** — Default empty when inbox is clean
- **Photo gallery** — Default empty before any photos taken on a trip
- **My Files** — Default empty before any files attached

---

## Do

- ✅ Centre the empty state in the available content area (not the full screen).
- ✅ Use SF Symbols — they scale with Dynamic Type and match system aesthetics.
- ✅ Keep copy short — users skim empty-state messages quickly.
- ✅ Always provide an escape from "No results" — a Clear filters / Clear search CTA.
- ✅ Test in both Light and Dark mode — `Icon/Subtle` can disappear in one mode if untested.
- ✅ Distinguish "no data yet" from "no results" — they call for different copy and CTAs.

## Don't

- ❌ Don't render an empty container — every zero-state needs an explicit empty pattern.
- ❌ Don't make the icon larger than 80pt — it dominates the screen.
- ❌ Don't show an empty state while data is still loading — use [[Loading Skeleton Pattern]] first.
- ❌ Don't use humorous or playful copy for the "no results" case — drivers are working under time pressure.
- ❌ Don't hide the Search Bar or filter chips when the list is empty — the user needs them to recover.
- ❌ Don't put two CTAs in one empty state — pick the single most useful next action.

---

Back to [[Patterns]] · [[Design System]].
