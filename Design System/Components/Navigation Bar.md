---
status: built
figma_node: 309:2318
file_key: 3qOFF7kHsaZPfdftDb1CVz
---

# Navigation Bar

Top navigation chrome for pushed iOS screens. Composes the iOS status bar with a title + leading/trailing action area. 6 Type variants cover stack push, sheet header, search, settings header, and a wide (iPad/landscape) layout.

**Figma:** [HaulEx UIKit · Navigation Bar](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=309-2318)
**Component set:** `309:2318`
**Library key:** `0bd88b3b2f287ae3c52be13e79246374e3bf68a4`

---

## Variants — `Type`

| Type | Node | Size | Purpose |
|---|---|---|---|
| Default | `309:2316` | 393×98 | Standard pushed screen: leading icon · centered title · trailing icon |
| Search Field | `309:2317` | 393×102 | Title row replaced with a Select pill + trailing icon button |
| Order Label | `310:1092` | 393×98 | Centered title + adjacent ABBR Badge (e.g. order code) |
| Settings | `851:1044` | 393×158 | Profile-style header: 88pt circular Image + Name + Company text |
| Stack | `867:2250` | 393×129 | Sheet header: grabber + Title and Controls with leading + trailing close buttons. Used in [[Sheet Pattern]] |
| Horizontal | `1361:1111` | 765×44 | Wider tablet/landscape layout — leading + centered title + trailing |

All variants except `Stack` and `Horizontal` include the iOS Status Bar (height 54pt, pt 21pt) as the top row.

---

## Anatomy

```
┌────────────────────────────────────────────┐
│ Status Bar (54pt)            9:41  ●●●● 🔋│
├────────────────────────────────────────────┤
│ ⊙ Leading      Title         Trailing ⊙   │  ← Title and Controls (44pt)
└────────────────────────────────────────────┘
```

**Default variant:**
- Leading slot: 44pt circular icon button (`Button` component, Icon Only variant), left-aligned at x=0
- Title slot: `Screen/Title` text style, centered (`text/primary`)
- Trailing slot: 88pt wide container, right-aligned; contains a 44pt circular icon button
- Hit areas: every icon button is 44×44pt minimum (HIG L1)

**Search Field variant:**
- Row height 48pt (no fixed 44pt slot)
- Padding: `Space/L` (16pt) horizontal, `Space/L` (16pt) vertical
- Internal gap: `Space/S` (8pt)
- Search input: full-width `Select` instance (`background/subtle`, `radius/pill`)
- Trailing: 44pt circular icon button (`background/subtle`, `radius/pill`)

**Order Label variant:**
- Row 44pt, centered
- Title (`Screen/Title`) + 20pt `Badge` (`background/subtle`, caption text "ABBR")
- Gap between title and badge: `Space/S` (8pt)
- Leading icon button mirrors Default

**Settings variant:**
- Row uses `Space/L` (16pt) horizontal padding, `Space/S` (8pt) vertical, gap `Space/L` between blocks
- Leading: 88×88pt circular Image (`background/subtle`, `radius/pill`)
- Text block (width 185pt): Name (`Section/Title`, `text/primary`) + Company (`Text/Secondary`, `text/tertiary`)

**Stack variant** (sheet header):
- Top: 10pt `_Card Top` strip (`background/tretiary`, top corners rounded 10pt) — visual hint of stacked sheet underneath
- Container: `background/primary`, top corners `radius/l` would be 16pt (actual: 16pt rounded TL/TR)
- Grabber: 5×36pt pill (`background/subtle`, radius 2.5pt)
- Title and Controls row: 44pt tall, [[Title and Controls]] instance with leading + trailing `Button` (xmark icon, 44×44pt circular)

**Horizontal variant:**
- Width 765pt, height 44pt only — no status bar
- Same leading/title/trailing pattern as Default but on a wider canvas

---

## Tokens

**Colors**
- Background (most variants): `Background/Primary` → `#0d0d0d`
- Stack variant top strip: `Background/Tretiary` → `#404040`
- Stack variant grabber + Settings avatar + Search field + Search trailing: `Background/Subtle` → `#262626`
- Status bar text in Stack variant: `Background/Inverse Static 2` (`#f2f2f2`)
- All title text: `Text/Primary` (`#f2f2f2`)
- Search field placeholder: `Text/Secondary` (`#e5e5e5`)
- Settings company line: `Text/Tertiary` (`#ccc`)

**Spacing**
- `Space/L` 16pt — outer horizontal padding, gaps
- `Space/M` 12pt — Stack title row inner gap
- `Space/S` 8pt — internal gaps
- `Space/XS` 4pt — button vertical padding

**Radius**
- `Radius/Pill` 999pt — every icon button, search pill, image circle, grabber pill
- 16pt (top-only) — Stack variant container corners
- 10pt (top-only) — Stack variant `_Card Top`

**Type**
- `Screen/Title` (17 / 22, weight 590, letter-spacing −0.43) — all titles
- `Section/Title` (20 / 25) — Settings Name line
- `Text/Secondary` (15 / 20, letter-spacing −0.45) — Settings Company line
- `Form/Input` (17 / 22, letter-spacing −0.408) — Search field label
- `Meta/Caption` (12 / 16) — ABBR badge in Order Label

---

## Composed components

- [[Components/Button|Button]] — `Size=S, Type=Ghost, Icon Only=True` for every leading/trailing icon button (44×44pt)
- [[Components/Title and Controls|Title and Controls]] — used inside Stack variant (`442:9262`)
- [[Components/Leading (Sheets)|Leading (Sheets)]] + [[Components/Trailing (Sheets)|Trailing (Sheets)]] — within Stack variant's title bar
- [[Components/Select|Select]] — used inside Search Field variant for the search pill
- [[Components/Badge|Badge]] — Order Label ABBR badge
- [[Components/Image|Image]] — Settings variant avatar (88pt circle)

---

## Usage rules

- Place at the top of every pushed iOS screen ([[Navigation Patterns]]).
- Use `Stack` only inside [[Sheet Pattern]] · Variant 3 (Stack Button Sheet) — never as the screen-level chrome.
- Use `Search Field` when the screen's primary task is search (see [[Filter Search Results Pattern]]).
- Use `Settings` only on the user/profile screen.
- Use `Order Label` on order detail screens where the ABBR identifies the order.
- Use `Horizontal` for tablet/landscape only.
- Minimum touch target on every icon button is 44×44pt ([[Rules]] L1).
- Title must use the `Screen/Title` text style — never set size/weight manually ([[Rules]] T2).

---

## Component properties

Each variant exposes boolean visibility properties:
- `showLeading` — toggle leading icon slot
- `showTitle` — toggle centered title
- `showTrailing` — toggle trailing icon slot
- `showTitleAndControls` — Stack only, toggle entire title row
- `title` — string instance swap for title text
- `name` / `company` — Settings variant text fields

---

## Related

- Used by every pushed screen — see [[Navigation Patterns]]
- Sheet variant feeds [[Sheet Pattern]]
- Mode label pill ([[Component Status]] · 📋 Planned) would sit inside the title slot for Driver/Passenger View screens

Back to [[Design System]] · [[Component Status]].
