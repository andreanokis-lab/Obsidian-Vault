# Empty State Patterns

Guide for designing empty, no-results, loading, and error states in the Driver App. Every screen that can show a list or query result must have all relevant states designed.

---

## The four states every list screen needs

| State | When it appears |
|---|---|
| **Default empty** | User arrives and no data exists yet (no loads assigned, no trips started) |
| **No results** | User searched or filtered and nothing matched |
| **Loading** | Data is being fetched |
| **Error / Offline** | Network error or server failure |

Do not design only the populated state and assume the rest is "obvious." Each requires its own frame.

---

## Anatomy of an empty state

```
          [Icon — SF Symbol]
          
         Headline (no data)
         
     Supporting message explaining
       why and what to do next.
       
        [ Optional CTA button ]
```

| Element | Token / Style |
|---|---|
| Icon | SF Symbol, 56–80pt visual size, `Icon/Subtle` color |
| Headline | `Text/Body` (17pt) or custom `Headline` (17pt Semibold), `Text/Primary` |
| Supporting message | `Text/Body` (17pt Regular), `Text/Secondary` color |
| CTA button | Secondary or Primary button style — see Button rules |
| Vertical centering | Center the group in the available content area (below nav, above tab bar) |
| Icon → Headline gap | `Space/XL` (24pt) |
| Headline → message gap | `Space/S` (8pt) |
| Message → CTA gap | `Space/XL` (24pt) |
| Max content width | 280pt (keep copy comfortable, not edge-to-edge) |

---

## State-specific content

### Default empty (no data)
- Icon: something relevant to the content type (e.g., `tray.fill` for empty inbox, `doc.fill` for no loads)
- Headline: "No [things] yet" — short, clear
- Message: Explain what the user can do or what will appear here
- CTA: Optional — if there's a clear action (create, add, invite), offer it

### No results (after search/filter)
- Icon: `magnifyingglass` or content-type icon
- Headline: "No [things] found" — acknowledge the search context
- Message: "Try adjusting your search or clearing your filters"
- CTA: "Clear filters" or "Clear search" — styled as a `Text/Link` button or secondary button. Must meet 44×44pt touch target.
- **This is a HIG P0 issue if missing** — do not ship a search screen without a no-results state

### Loading
- Use an activity indicator (system spinner) in `Icon/Subtle` color
- Optional: skeleton placeholders for list rows (more polished)
- No text needed for fast loads (< 1s); add "Loading…" message for longer waits
- `Meta/Caption` text style if message is shown, `Text/Tertiary` color

### Error / Offline
- Icon: `wifi.slash` for offline, `exclamationmark.triangle.fill` for server error — use `Icon/Negative` color
- Headline: "Couldn't load [things]" — honest, not alarming
- Message: "Check your connection and try again" (network) or "Something went wrong" (server)
- CTA: "Try again" — Primary button

---

## Vertical positioning

Empty states should be vertically centered in the **available content area** (between navigation bar and tab bar), not the full screen height.

If the screen has a search bar or filter controls, the empty state sits below those controls — the controls remain visible even when empty.

---

## Driver App — specific states to design

| Screen | States needed |
|---|---|
| Company Filter | Default empty · No results (active search + filters) · Loading · Error |
| Load list | Default empty · No results · Loading · Error |
| Trip history | Default empty · Loading · Error |
| Messages | Default empty · Loading · Error |
| Photo gallery | Default empty (no photos taken yet) |

---

## Do / Don't

✅ Always pair "No results" state with a clear path to fix it (clear filter, try different search)
✅ Use SF Symbols — they scale with Dynamic Type and match system aesthetics
✅ Keep copy short — users read empty state messages quickly while frustrated
✅ Test empty states in both Light and Dark mode (subtle tokens like `Icon/Subtle` can disappear in one mode if not tested)
❌ Don't use humorous or overly playful copy for error states — drivers are working under time pressure
❌ Don't make the empty state icon too large (> 80pt) — it takes over the screen
❌ Don't show an empty state while data is still loading — show loading state first

---

## Reference

Existing HaulEx example: [[Company Filter Not Found - Sprint Checklist]] — P0 HIG issues identified in the current no-results design.

---

Back to [[Design System]] · [[Patterns]] · [[Getting Started]].
