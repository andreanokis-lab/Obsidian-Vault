# Action Picker Pattern

Bottom-anchored **sheet of actions** (iOS Action Sheet) used whenever a picker or action list reaches **5 or more items**. Comes with a mandatory Cancel button and a full-width backdrop scrim.

Below 5 items the list stays an anchored popover — see [[Context Menu Pattern]].

- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit)
- **Figma documentation:** Section `2126:4034` "Action Picker Pattern — Documentation" on the `----- Patterns` page
- **Figma page:** `----- Action Sheet (Under Constraction)` — visual scaffold only; there is no shipped custom component. **Use the iOS native `UIAlertController(preferredStyle: .actionSheet)`.**
- **Related pattern:** [[Sheet Pattern]] · Variant 4 (Action Sheet)

---

## The core rule

> **1–4 items or actions → [[Context Menu Pattern|Context Menu]]** (anchored popover)
> **5+ items or actions → Action Picker** (bottom sheet with actions)

Count is the deciding factor. At 5+ rows an anchored popover stops being comfortable to reach and scan on a phone held one-handed, so the list moves to the bottom of the screen where the thumb lands — and gains an explicit Cancel.

Cancel does **not** count toward the 5. Five actions + Cancel is the minimum shape of this pattern.

**Upper bound:** if the list grows long enough to scroll (roughly 8+ rows), or the rows need avatars, helper text, search, or grouping — go to [[Sheet Pattern]] · Half Sheet with a list instead.

---

## Anatomy

```
    ╭──────────────────────────────╮
    │        (scrim, ~30%)         │
    │                              │
    │  ┌────────────────────────┐  │
    │  │  Optional title        │  │
    │  │  Optional message      │  │
    │  ├────────────────────────┤  │
    │  │       Action           │  │
    │  ├────────────────────────┤  │
    │  │       Action           │  │
    │  ├────────────────────────┤  │
    │  │       Action           │  │
    │  ├────────────────────────┤  │
    │  │       Action           │  │
    │  ├────────────────────────┤  │
    │  │       Delete           │  │   ← destructive · red tint
    │  └────────────────────────┘  │
    │  ┌────────────────────────┐  │
    │  │        Cancel          │  │   ← always present · bold · own block
    │  └────────────────────────┘  │
    │        [safe area]           │
    ╰──────────────────────────────╯
```

| Region | Notes |
|---|---|
| Backdrop scrim | iOS default (~30% black) — handled by `UIAlertController` |
| Sheet container | Native, `Radius/L`-equivalent corners on the two grouped blocks |
| Action group | 5+ rows in a rounded rectangle · `Background/Subtle` |
| Row label | Native iOS text style — 20pt Regular, `Text/Action` (system blue) |
| Destructive row | Same row shape, label in `Text/Negative` (system red) — `UIAlertAction.Style.destructive` |
| Cancel block | Separate rounded rectangle, bold label, `Background/Primary` — `Space/S` gap from the action group |
| Safe area | Cancel sits above the home indicator, respected by iOS |

Do not mock or replicate this with custom shapes — the visual quirks (spacing between groups, Cancel bolding, tap targets) are iOS's job.

---

## Composition rules

| Rule | Value |
|---|---|
| **Action count** | **5+ rows, plus Cancel** (Cancel is not counted) |
| Below 5 actions | Use [[Context Menu Pattern]] — do not present a sheet for a short list |
| Above ~8 actions | Switch to [[Sheet Pattern]] · Half Sheet + list — an Action Picker that scrolls is a Half Sheet |
| Cancel | **Always present**, always last, in its own block |
| Destructive row | At most one, placed immediately above Cancel |
| Row order | Most likely action first; destructive second-to-last; Cancel last |
| Row height | Native (~57pt) — do not override |
| Title / message | Optional; use only when the target is ambiguous without label context |
| Backdrop | System scrim; tap-outside dismisses (equivalent to Cancel) |
| Trigger | Any tappable control — icon button, list row, long-press, [[Components/Button|Button]] with `Type=Ghost` |
| Presentation | `UIAlertController` with `preferredStyle: .actionSheet` |

---

## Interaction

1. User taps the trigger (a button, a row, a long-press target).
2. Scrim fades in; the action group and Cancel slide up from the bottom together.
3. User taps a row → the sheet dismisses, the corresponding action executes.
4. User taps Cancel, taps outside the sheet, or swipes down → dismisses with no side effect.
5. If a destructive action is chosen, follow up with a [[Sheet Pattern|Stack Button confirmation sheet]] only if the action is not otherwise recoverable (see [[Error State Pattern]] · Modal confirmation sub-pattern).

---

## When to use vs. adjacent patterns

| If… | Use |
|---|---|
| **5+ items or actions** | **Action Picker (this pattern)** |
| **1–4 items or actions** | **[[Context Menu Pattern]]** |
| List scrolls (~8+), or rows need avatars / helper text / search | [[Sheet Pattern]] · Half Sheet with a list |
| Confirming one decision, especially destructive (do it / don't) | [[Sheet Pattern]] · Stack Button Sheet |
| Actions target multiple objects (bulk) | [[Sheet Pattern]] · Half Sheet with checkboxes |
| Two mutually-exclusive modes, both always visible | [[Components/Segment Control|Segment Control]] |

A destructive **confirmation** ("Delete this receipt?" → Delete / Cancel) is not a picker — it's a [[Sheet Pattern|Stack Button Sheet]] regardless of count.

---

## Real Driver App screens using this pattern

Verified against the Driver App `DS` page — see [[_Pattern Evidence Map]] and [[Sheet Pattern]] · Variant 4.

- **Photo Actions (Done)** — Truck Service `662:30875` · "Take photo / Choose from library / Cancel"
- **Picture (Done)** — Profile `667:31697` · profile photo source picker
- **Dropdown (Done)** — Profile `667:31697` · picker rendered as an action sheet
- **Select (Done)** — Order Details `667:31707` · same pattern used from an Order row

⚠️ Several of these currently show only 2–3 actions. Under the 1–4 / 5+ rule they belong in the [[Context Menu Pattern]] and should be migrated — they are historical evidence of the sheet composition, not endorsements of their current item counts.

---

## Do

- ✅ Use this pattern the moment the list reaches **5 items** — not before.
- ✅ Use the iOS-native `UIAlertController` — never draw a custom Action Picker.
- ✅ Include Cancel every time. Cancel is what separates an Action Picker from a [[Context Menu Pattern|Context Menu]].
- ✅ Put the destructive action second-to-last, right above Cancel.
- ✅ Use verb labels ("Delete", "Take photo") — not "OK" / "Confirm".
- ✅ Move to a [[Sheet Pattern|Half Sheet]] list once the picker would scroll (~8+ rows).
- ✅ Chain a [[Sheet Pattern|Stack Button confirmation]] after destructive picks only when the action is truly irreversible.

## Don't

- ❌ **Don't use an Action Picker for 1–4 items** — that's a [[Context Menu Pattern|Context Menu]]; a sheet for three options is disproportionate.
- ❌ Don't ship a custom Action Sheet component — the UIKit page is a scaffold only, and the platform version already handles safe area, dark mode, dynamic type, and accessibility.
- ❌ Don't omit Cancel — even if the sheet is dismissable by tap-outside, iOS users expect the button.
- ❌ Don't stack two destructive actions in one Action Picker — split into two flows.
- ❌ Don't add a title / message unless the target isn't obvious from context; extra text turns an Action Picker into a heavier sheet.
- ❌ Don't let the picker scroll — at that length it's a [[Sheet Pattern|Half Sheet]] with a list.
- ❌ Don't anchor an Action Picker to a specific control (like a Context Menu) — iOS always docks it to the bottom of the screen.
- ❌ Don't nest a picker inside another sheet — dismiss the parent first, then present.

---

Back to [[Patterns]] · [[Design System]].
