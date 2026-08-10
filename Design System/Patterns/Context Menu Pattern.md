# Context Menu Pattern

How the Driver App composes a **dropdown / context menu** — a short, anchored list of options that appears next to the control that opened it and disappears when the user taps outside or picks a row.

Built from two DS components:
- [[Select]] — the trigger pill that shows the current value.
- [[Menu]] + [[Menu Item]] — the popover list of options.

- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit)
- **Figma section:** `----- Select + Dropdown` (page)
- **Figma documentation:** Section `1745:7513` "Select — Documentation" and `1745:7656` "Menu — Documentation"

---

## The core rule

> **Context Menu (Dropdown)** = quick single-choice from ≤ 7 options, anchored to the control the user just tapped.
> **[[Action Picker Pattern|Action Picker]]** = 3–5 actions on a target, anchored to the bottom of the screen.
> **[[Sheet Pattern|Half Sheet]] + list** = > 7 options, or the options need helper text / dividers / sections.

If the user is choosing a **value** (sort, filter, status, currency…) → Context Menu.
If the user is choosing an **action** on the current object (Take photo, Delete, Share…) → [[Action Picker Pattern|Action Picker]].
If the list is longer than a menu can comfortably show → Half Sheet with a list.

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
   │ Delete           │   ← Menu Item · Type=Destructive · optional
   ╰──────────────────╯
```

| Region | Component / Token |
|---|---|
| Trigger | [[Select]] · `State=Default` closed / `State=Focused` while menu is open |
| Popover container | [[Menu]] · fill `Background/Subtle` · `Radius/M` (12) all corners |
| Row divider | `Width/XS` bottom stroke · `Border/Primary` — comes from each [[Menu Item]] |
| Row | [[Menu Item]] · padding `Space/L` horizontal · label `Form/Label/*` · fill `Text/Primary` |
| Trailing check | `Icon/Primary` glyph — shown on the currently-selected row via `Show Symbol=true` |
| Destructive row | [[Menu Item]] · `Type=Destructive` · label `Text/Negative` — last row only |
| Last row divider | `Stroke=None` on the last visible row to avoid a stray edge line |

The menu is **anchored to the trigger**, not the screen. It never occupies the full width of the viewport and never has a scrim behind it — that's the visual signal that separates a dropdown from a Sheet or an Action Picker.

---

## Composition rules

| Rule | Value |
|---|---|
| Trigger height | `Space/4XL` (48pt) — [[Select]] default |
| Menu width | ≥ trigger width, ≤ 280pt (fits ~24 characters of `Form/Label/*` text) |
| Menu corner radius | `Radius/M` (12) on all four corners |
| Menu gap from trigger | `Space/S` (8pt) |
| Row height | Matches [[Menu Item]] default — single line |
| Max visible rows | 7 (HIG comfort). Ceiling of 12 exists on [[Menu]] but is for edge cases only. |
| Selected row | `Show Symbol=true` with checkmark glyph |
| Non-selected rows | `Show Symbol=false` |
| Destructive row | Bottom of the list, single instance — via `Show Destructive=true` on [[Menu]] |
| Last visible row stroke | `Stroke=None` on the last [[Menu Item]] to remove the trailing hairline |
| Backdrop | **None** — no scrim, no dim. Tap-outside dismisses. |

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
5. Scroll: if the menu content would extend past the safe area, the menu scrolls internally rather than growing — but this is the sign the list is too long; convert to a Half Sheet.

There is no explicit Cancel row on a Context Menu — dismissal is by tap-outside. Cancel is an [[Action Picker Pattern|Action Picker]] concept.

---

## When to use vs. adjacent patterns

| If… | Use |
|---|---|
| Picking a **value** the trigger will display afterwards | Context Menu (this pattern) |
| Picking an **action** to perform on a target | [[Action Picker Pattern]] |
| List needs > 7 rows, or rows have avatars / helper text | [[Sheet Pattern]] · Half Sheet + list |
| Only two paths, one destructive | [[Sheet Pattern]] · Stack Button Sheet |
| Two mutually-exclusive modes | [[Components/Segment Control|Segment Control]] |
| Free-text entry | [[Input]] |
| Yes / no state | [[Toggle]] |

---

## Real Driver App screens using this pattern

Verified against the Driver App `DS` page — see [[_Pattern Evidence Map]].

- **Order Details** — status pickers on the trip header use Select + Menu.
- **Filters** — Filter Search sub-flows (see [[Filter Search Results Pattern]]) use Select-triggered menus for currency / date range / status.
- **Settings** — small enum choices (language, distance unit).

If the same picker in the Driver App uses a bottom-anchored sheet with a Cancel button instead of an anchored popover, it's the [[Action Picker Pattern]] and not this one.

---

## Do

- ✅ Anchor the menu to the control the user tapped — never float it in the middle of the screen.
- ✅ Show the current selection with `Show Symbol=true` and the checkmark glyph. Hide checkmarks on non-selected rows.
- ✅ Keep menus ≤ 7 rows. Convert to a [[Sheet Pattern|Half Sheet]] list when the list grows.
- ✅ Set `Stroke=None` on the last visible [[Menu Item]] before the destructive row (or the last row overall) to remove the trailing hairline.
- ✅ Toggle `State=Focused` on the [[Select]] trigger while the menu is open.
- ✅ Put the destructive option last, via `Show Destructive=true` — never mid-list.
- ✅ Dismiss on tap-outside.

## Don't

- ❌ Don't put a scrim behind a Context Menu — it visually promotes it to a Sheet.
- ❌ Don't use a Context Menu for a list that scrolls — convert to a Half Sheet.
- ❌ Don't put multi-line content, avatars, or helper text in [[Menu Item|Menu Items]] — they're single-line rows.
- ❌ Don't stack two destructive rows.
- ❌ Don't reuse Context Menu for **actions on the current screen** — that's the [[Action Picker Pattern]].
- ❌ Don't add a Cancel row — dismissal is tap-outside; Cancel belongs to [[Action Picker Pattern|Action Pickers]].
- ❌ Don't open a menu without a visible trigger the user can point to.

---

Back to [[Patterns]] · [[Design System]].
