# Context Menu Pattern

How the Driver App composes a **dropdown / context menu** — a short, anchored list that appears next to the control that opened it and disappears when the user taps outside or picks a row.

Built from two DS components:
- [[Select]] — the trigger pill that shows the current value.
- [[Menu]] + [[Menu Item]] — the popover list.

- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit)
- **Figma documentation:** Section `2126:3868` "Context Menu Pattern — Documentation" on the `----- Patterns` page
- **Component docs:** Section `1745:7513` "Select — Documentation" and `1745:7656` "Menu — Documentation" on `----- Select + Dropdown`

---

## The core rule

> **1–4 items or actions → Context Menu** (anchored popover)
> **5+ items or actions → [[Action Picker Pattern|Action Picker]]** (bottom sheet with actions)

Count is the deciding factor, not intent. Both value-picks and action-lists follow the same threshold — what changes above 5 is that an anchored popover stops being comfortable to reach and scan, so the list moves to a bottom sheet where the thumb can reach it.

The count includes the destructive row. Four total visible rows is the ceiling — a menu of 3 options + 1 destructive is at the limit.

**Escape hatch:** if the rows need avatars, helper text, search, or grouping — regardless of count — go to [[Sheet Pattern]] · Half Sheet with a list. [[Menu Item]] rows are single-line only.

---

## Anatomy

```
┌────────────────────┐
│  Selected value  ⌄ │   ← Select (State=Focused while open)
└────────────────────┘
   ╭──────────────────╮
   │ Option 1       ✓ │   ← Menu Item · Type=Default · Show Symbol=true
   ├──────────────────┤
   │ Option 2         │   ← Menu Item · Type=Default · Show Symbol=false
   ├──────────────────┤
   │ Option 3         │
   ├──────────────────┤
   │ Delete           │   ← Menu Item · Type=Destructive · counts toward the 4
   ╰──────────────────╯
```

| Region | Component / Token |
|---|---|
| Trigger | [[Select]] · `State=Default` closed / `State=Focused` while menu is open |
| Popover container | [[Menu]] · fill `Background/Subtle` · `Radius/M` (12) all corners |
| Row | [[Menu Item]] · padding `Space/L` horizontal · label `Form/Label/*` · fill `Text/Primary` |
| Row divider | `Width/XS` bottom stroke · `Border/Primary` — comes from each [[Menu Item]] |
| Trailing check | `Icon/Primary` glyph — shown on the currently-selected row via `Show Symbol=true` |
| Destructive row | [[Menu Item]] · `Type=Destructive` · label `Text/Negative` — last row only |
| Last row divider | `Stroke=None` on the last visible row to avoid a stray edge line |
| Backdrop | **None** — no scrim, no dim. Tap-outside dismisses. |

The menu is **anchored to the trigger**, not the screen. It never occupies the full width of the viewport and never has a scrim behind it — that's the visual signal separating a dropdown from a Sheet or an [[Action Picker Pattern|Action Picker]].

---

## Composition rules

| Rule | Value |
|---|---|
| **Item count** | **1–4 visible rows, including the destructive row** |
| At 5+ items | Switch to [[Action Picker Pattern]] — do not grow the menu |
| Trigger height | `Space/4XL` (48pt) — [[Select]] default |
| Menu width | ≥ trigger width, ≤ 280pt (fits ~24 characters of `Form/Label/*` text) |
| Menu corner radius | `Radius/M` (12) on all four corners |
| Menu gap from trigger | `Space/S` (8pt) |
| Row height | Matches [[Menu Item]] default — single line |
| Unused [[Menu]] slots | Hide via `Show Item N=false` — the component ships 12 slots, the pattern caps usage at 4 |
| Selected row | `Show Symbol=true` with checkmark glyph |
| Non-selected rows | `Show Symbol=false` |
| Destructive row | Bottom of the list, single instance — via `Show Destructive=true` on [[Menu]] |
| Last visible row stroke | `Stroke=None` on the last [[Menu Item]] to remove the trailing hairline |
| Backdrop | **None** — no scrim, no dim. Tap-outside dismisses. |
| Scrolling | Never. A Context Menu that needs to scroll is the wrong pattern. |

---

## Triggers

| Trigger | Component | Use for |
|---|---|---|
| Value pill | [[Select]] | Filter / sort / status / mode / currency — the current value is meaningful and worth surfacing |
| Overflow button | [[Button]] · `Icon Only=true` · `Type=Ghost` (⋯ or ⋮) | Row-level actions on a card / list row — the trigger's job is only to open the menu |
| More icon on a Navigation Bar | [[Navigation Bar]] trailing button | Screen-level overflow (rare — prefer explicit actions in the bar) |

Every menu **must have a visible, tappable trigger**. Never open a Context Menu from a long-press only — that's a [[Sheet Pattern|Sheet]] or an [[Action Picker Pattern|Action Picker]].

---

## Interaction

1. User taps the trigger. Trigger switches to `State=Focused`.
2. Menu fades in anchored below (or above, if there's no room below) the trigger with `Space/S` (8pt) gap.
3. User taps a row → menu dismisses, the selected value updates on the trigger, trigger returns to `State=Default`.
4. User taps outside the menu → menu dismisses, no change, trigger returns to `State=Default`.

There is no Cancel row and no scrolling. If either seems necessary, the list has outgrown this pattern — move to [[Action Picker Pattern]].

---

## When to use vs. adjacent patterns

| If… | Use |
|---|---|
| **1–4 items or actions** | **Context Menu (this pattern)** |
| **5+ items or actions** | **[[Action Picker Pattern]]** |
| Rows need avatars / helper text / search / grouping (any count) | [[Sheet Pattern]] · Half Sheet + list |
| Confirming one decision, especially destructive (do it / don't) | [[Sheet Pattern]] · Stack Button Sheet |
| Two mutually-exclusive modes, both always visible | [[Components/Segment Control|Segment Control]] |
| Free-text entry | [[Input]] |
| Yes / no state | [[Toggle]] |

A destructive **confirmation** ("Delete this receipt?" → Delete / Cancel) is not a picker — it's a [[Sheet Pattern|Stack Button Sheet]] regardless of count.

---

## Real Driver App screens using this pattern

Verified against the Driver App `DS` page — see [[_Pattern Evidence Map]].

- **Order Details** — status pickers on the trip header use Select + Menu.
- **Filters** — Filter/Search sub-flows (see [[Filter Search Results Pattern]]) use Select-triggered menus for currency / date range / status.
- **Settings** — small enum choices (language, distance unit).

Any of these that currently exposes 5 or more rows should be migrated to the [[Action Picker Pattern]].

---

## Do

- ✅ Keep to **1–4 rows total**, destructive row included.
- ✅ Anchor the menu to the control the user tapped — never float it in the middle of the screen.
- ✅ Show the current selection with `Show Symbol=true` and the checkmark glyph. Hide checkmarks on non-selected rows.
- ✅ Hide unused [[Menu]] slots with `Show Item N=false`.
- ✅ Set `Stroke=None` on the last visible [[Menu Item]] to remove the trailing hairline.
- ✅ Toggle `State=Focused` on the [[Select]] trigger while the menu is open.
- ✅ Put the destructive option last, via `Show Destructive=true` — never mid-list.
- ✅ Dismiss on tap-outside.

## Don't

- ❌ **Don't exceed 4 rows** — at 5+ switch to the [[Action Picker Pattern]], don't grow the popover.
- ❌ Don't let a Context Menu scroll. Scrolling means you're past the threshold.
- ❌ Don't put a scrim behind a Context Menu — it visually promotes it to a Sheet.
- ❌ Don't put multi-line content, avatars, or helper text in [[Menu Item|Menu Items]] — they're single-line rows.
- ❌ Don't stack two destructive rows.
- ❌ Don't add a Cancel row — dismissal is tap-outside; Cancel belongs to [[Action Picker Pattern|Action Pickers]].
- ❌ Don't open a menu without a visible trigger the user can point to.
- ❌ Don't fill all 12 [[Menu]] slots just because the component allows it — the pattern ceiling is 4.

---

Back to [[Patterns]] · [[Design System]].
