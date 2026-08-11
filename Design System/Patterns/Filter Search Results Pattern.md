# Filter / Search Results (Empty) Pattern

How to compose a search / filter screen and what to show when the search returns no results. Extends [[Empty State Pattern]] for the "No results" sub-case, with search-bar and filter-chip-specific affordances above the empty state.

The canonical Driver App example is the Company contact search (`No Contact Found (Done)`) — the user searched / filtered and nothing matched.

- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit)
- **Figma documentation:** Section `1809:10885` "Filter / Search Results Pattern — Documentation" on the `----- Patterns` page

---

## Anatomy

```
┌─────────────────────────────┐
│  Navigation Bar              │
│─────────────────────────────│
│  ┌─────────────────────┐    │
│  │ 🔍  search query  ✕ │    │  ← Search Bar (organism)
│  └─────────────────────┘    │
│  ┌Chip1┐ ┌Chip2┐ ┌Chip3┐ … │  ← Filter Chips
│─────────────────────────────│
│                              │
│                              │
│         [Icon]               │  ← Empty State Pattern (no-results sub-case)
│                              │
│      No [things] found       │
│   Try adjusting your search  │
│   or clearing your filters.  │
│                              │
│      [ Clear filters ]       │  ← Recovery CTA — always present
│                              │
└─────────────────────────────┘
```

| Region | Component / Pattern |
|---|---|
| Search Bar | iOS-style search field — uses [[Components/Input|Input]] (`State=Focused` while typing, `State=Filled` with a value, with trailing `✕` to clear). On HaulEx the search bar lives at the top of a search screen — Search Bar is an organism (planned, out of scope for individual doc) |
| Filter Chips (optional) | Horizontal scroll of [[Components/Chip|Chip]] instances — typically `Type=Default` or `Type=Numbered` showing the count of matches per filter |
| List area (populated state) | [[List with Actions Pattern]] or [[Components/Content Row|Content Row]] |
| List area (empty state) | [[Empty State Pattern]] — "No results" sub-case with **always-present recovery CTA** |

---

## Composition rules

| Rule | Value |
|---|---|
| Search Bar position | Top of the screen, below Navigation Bar, full-width |
| Search Bar horizontal margin | `Space/L` (16pt) |
| Filter Chips horizontal scroll | Below the Search Bar; padding `Space/L` left, `Space/L` right |
| Gap between chips | `Space/S` (8pt) |
| Active chips behind / below the Search Bar | Stays visible when the list is empty — the user needs them to recover |
| List area top gap | `Space/M` (12pt) below chips (or below Search Bar if no chips) |
| Empty-state centring | Centred in the **remaining available area** (below Search Bar + chips, above tab bar / safe area) — not the full screen |
| Empty-state CTA | **Required** when search / filters are active — provides the escape ("Clear filters", "Clear search") |
| Recovery CTA style | [[Components/Button|Button]] · `Size=M, Type=Ghost, Role=Link` (or `Role=Default` for neutral) |

---

## Where a clear / reset affordance goes

Added 2026-08-11 after the [[Segment Control]] `✕` review. Ranked — use the highest one that applies, and stop.

| # | Placement | When | Spec |
|---|---|---|---|
| 1 | **Inside the selection set, as the first segment: `All`** | Single-select filtering via [[Segment Control]]. This is the default answer. | **Leftmost** — widest scope leads, and `All` is the default state so it must not sit at the far edge. Matches [[Orders List]] (`All / Active / Completed`). No separate control exists — selecting `All` *is* the deselect. |
| 2 | **Empty-state recovery CTA — "Clear filters"** | The filter produced zero results. Already required by this pattern. | [[Button]] `Size=M, Type=Ghost` · centred in the remaining area · copy per [[Content Style Guide]] (`Clear filters` / `Clear search`) |
| 3 | **[[Navigation Bar]] trailing slot — `Clear`** | Several filter mechanisms are active at once (search + chips + segments) and one screen-level reset is needed. | Text label, never a glyph. `Text/Link` — tinted so it reads as a button and not as a second title. Disabled/dimmed while nothing is set. ⚠️ No Nav Bar variant supports a text trailing action yet — see [[Component Status]]. |
| 4 | **Filter sheet header, Leading slot — `Reset`** | Filters live in a [[Sheet Pattern\|sheet]]. | [[Title and Controls]] · `Reset` in [[Leading (Sheets)]], `Apply` / `Done` in [[Trailing (Sheets)]]. Reset is not the primary action, so Leading is correct here. |
| 5 | **Per-chip `✕`** | Filters are multi-select / individually removable. | [[Chip]] row, not a Segment Control. The only place a `✕` is legitimate. |

### Never

- ❌ Inside the [[Segment Control]] container — see [[Rules#C5]].
- ❌ Icon-only anywhere in a filter context. `✕` reads as *close the screen*.
- ❌ Immediately adjacent to the control with a tight gap — even outside the container it reads as a segment. If it must sit on the same row, minimum `Space/M` (12pt) outside the container, and it must be a word.
- ❌ Styled destructive (`Text/Negative`). Clearing a filter destroys nothing — use `Text/Link`. Red in an iOS nav bar promises a consequence that a filter reset doesn't have.
- ❌ Enabled in the pristine state. Disable or hide `Clear` / `Reset` until at least one criterion is set.

Worked example with all of this applied (and the mistakes it started with): [[Order Search Screen]].

---

## Three flavours of empty

| Flavour | Trigger | What to show |
|---|---|---|
| **No data yet** (initial) | User hasn't searched / filtered, dataset is genuinely empty | [[Empty State Pattern]] · *Default empty* sub-case · optional CTA ("Add", "Invite") |
| **No results from search** | Search query returned nothing | Empty State Pattern · *No results* sub-case · CTA = "Clear search" |
| **No results from filters** | One or more filter chips active, returning nothing | Empty State Pattern · *No results* sub-case · CTA = "Clear filters" |

The Search Bar + active filter chips remain visible in all three — the user needs context to recover.

---

## Real Driver App screens using this pattern

Verified against the Driver App DS page on 2026-05-21. See [[_Pattern Evidence Map]].

| Screen | Section | State |
|---|---|---|
| **No Contact Found (Done)** | Company `667:31705` | Canonical no-results state — search returned empty |
| **Company File List (Done)** | Company `667:31705` | Populated state for contrast |
| **Company Placeholder (Done)** | Company `667:31705` | Default empty — no companies yet |

The Company screen is the clearest example. Other lists in the app (Receipts, Files, Trips) also use search / filter affordances but rely on [[Empty State Pattern]] alone for their empty cases.

---

## Search Bar behaviour (HIG)

The Search Bar's interactive behaviour is owned by iOS / [[Components/Input|Input]] (`State=Focused`). Key HIG rules:

- **Live search** (filter as the user types) is preferred for short result sets
- **Submit-on-enter** for expensive queries (server-side searches)
- **Trailing `✕`** clears the query and returns to the un-filtered state
- **Cancel** (text button above the keyboard or via the Search Bar) exits search mode entirely
- **Recent searches** can appear as a list below the Search Bar when the field is focused and empty

The Driver App should debounce live-search input by ~300ms to avoid flooding the server.

---

## Do

- ✅ Always keep the Search Bar + active filter chips **visible** when the list is empty — the user needs them to recover.
- ✅ Show the **Clear** CTA in the empty state — never strand the user with no escape.
- ✅ Distinguish "no data yet" from "no results" — different copy, different CTAs.
- ✅ Use [[Components/Chip|Chip]] `Type=Numbered` for filter chips that show match counts ("Receipts (12)").
- ✅ Debounce live-search input (~300ms) to avoid hammering the server.
- ✅ Use the `Type=Filled` state on the Search Bar's Input when a query is active — and show the trailing `✕`.

## Don't

- ❌ Don't hide the Search Bar or filter chips when the list is empty — that's exactly when the user needs them to fix the query.
- ❌ Don't show an empty state without a recovery CTA when filters / search are active.
- ❌ Don't put more than ~5 filter chips visible at once — if more are needed, wrap to a second row or open a [[Sheet Pattern|sheet]] filter picker.
- ❌ Don't auto-submit search on the first keystroke — debounce or wait for submit.
- ❌ Don't reuse "no data yet" copy ("No companies yet") for a no-results state — they're different situations.

---

Back to [[Patterns]] · [[Design System]].
