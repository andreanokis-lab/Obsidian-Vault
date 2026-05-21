# Section Header Pattern

A title above a content group. Used to break a screen into scannable sections — Settings groups, list groups within a long list, content rows within a card. Three escalating variants:

1. **Plain title** — just `Section/Title` typography. Use when no per-section action is needed.
2. **Title + trailing action** — `Section/Title` + a small inline action ("View all", "+", "Edit"). Use [[Components/Trailing (Action Section)|Trailing (Action Section)]] for the action.
3. **Action Section component** — the rich, branded version with INOP badge, VIN/weight stats, and 1–2 trailing actions. Use [[Components/Action Section|Action Section]] directly.

For expand/collapse behaviour, use [[Components/Collapse Expand|Collapse / Expand]] instead.

- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit)
- **Figma documentation:** Section `1786:10121` "Section Header Pattern — Documentation" on the `----- Patterns` page

---

## Pick the right variant

| Variant | Use when |
|---|---|
| **Plain title** | Section just needs a name. No action available. |
| **Title + trailing action** | One inline action helps users navigate / add. Examples: "View all" link, "+ Add" icon button, "Edit" link. |
| **Action Section** | Context-rich header — driver / vehicle / customer name with status (INOP) and inline actions. See [[Components/Action Section|Action Section]] component doc. |
| **Collapse / Expand** | Section is hideable / expandable. Use [[Components/Collapse Expand|Collapse / Expand]] component. |

---

## Anatomy

### Plain title

| Element | Token / Style |
|---|---|
| Title text | `Section/Title` (20pt Regular, Title 3) · `Text/Primary` |
| Container padding (above the section content) | `Space/L` horizontal, `Space/S` vertical (matches list-section header padding) |

### Title + trailing action

| Element | Token / Style |
|---|---|
| Container (FRAME, horizontal) | padding `Space/L` × `Space/S` · gap `Space/M` · counter-axis space-between |
| Title | `Section/Title` (20pt Regular) · `Text/Primary` |
| Trailing action | [[Components/Trailing (Action Section)|Trailing (Action Section)]] (Type=Icon · Text · Icon-chevron) |

### Action Section (component)

Use the component directly — full spec lives in [[Components/Action Section]].

---

## Composition rules

| Rule | Value |
|---|---|
| Horizontal margin | `Space/L` (16pt) — matches screen edge padding |
| Top padding (above the title) | `Space/S` (8pt) |
| Bottom padding (below the title, before the content) | `Space/S` (8pt) — keeps the title visually attached to its section |
| Gap to previous section | `Space/2XL` (32pt) — creates a clear break between sections |
| Title text style | Always `Section/Title` (20pt Regular, Title 3) for in-page sections; never `Screen/Title` (that's the nav bar) |
| Trailing action — min tap target | `Space/TapTarget` (44pt) — even if the visible label is small |
| Sticky on scroll? | Optional — iOS HIG supports sticky section headers in lists. Disable if the list is short |

---

## When to add a trailing action

Add one **only if** the section has a meaningful single action that benefits from being available at the section level rather than per-row:

| Trailing action | Action variant | When |
|---|---|---|
| "View all →" link | Type=Text, label "View all" | Section shows a preview; user can navigate to a full list |
| "+ Add" icon button | Type=Icon, plus icon | Section is a list user can extend (notes, files, photos) |
| "Edit" link | Type=Text, label "Edit" | Section is a list with bulk edit / reordering mode |

Don't stack two trailing actions — pick one.

---

## Real Driver App screens using this pattern

Verified against the Driver App DS page on 2026-05-21. See [[_Pattern Evidence Map]].

Section Header Pattern appears **inside** other screens — not as a standalone screen. Confirmed inside:

- **Settings (Done)** — Settings section `667:31696` · groups (Notifications, Privacy, Account) each lead with a `Section/Title` header
- **Notes List (Done)** — Notes section `667:31700` · grouped by date with section headers
- **Trip Order List Pickup / Delivery / Completed (Done)** — Trips section `1:28891` · each trip group introduced by a `Section/Title`
- **Receipts list (Done)** — Receipts section `662:30759` · grouped by month
- **Truck Service (Done)** — Truck Service section `662:30875` · grouped by category
- **Order Details (Done)** — Order Details `667:31707` · multiple `Section/Title` sub-sections
- **Sibebar menu (Done)** — Sidebar `662:30757` · uses Action Section as group headers
- **Safety List (Done)** — Safety `667:31706` · grouped sections

When a screen uses the richer Action Section component (label + INOP + VIN/Weight + trailing actions), the Section Header Pattern points at that component instead.

---

## Do

- ✅ Use `Section/Title` (20pt Regular, Title 3) for all in-page section headers — never `Screen/Title` (that's nav bar only).
- ✅ Add a trailing action only when one meaningful action belongs at the section level.
- ✅ Use [[Components/Action Section]] when the section needs status badges (INOP) or rich context.
- ✅ Use [[Components/Collapse Expand]] when the section toggles.
- ✅ Keep titles short — section headers are scannable signposts, not paragraphs.

## Don't

- ❌ Don't use `Screen/Title` (Headline 17pt Semibold) for in-page section headers — it's reserved for the nav bar.
- ❌ Don't stack multiple Section/Title headers at the same level without a `Space/2XL` gap between sections.
- ❌ Don't add a trailing action just because the slot exists — needs a real reason.
- ❌ Don't put two trailing actions in one section header — pick one.
- ❌ Don't use Section Header Pattern as a screen header — that's the Navigation Bar's job.

---

Back to [[Patterns]] · [[Design System]].
