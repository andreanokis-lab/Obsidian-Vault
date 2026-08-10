# Action Picker Pattern

Bottom-anchored **iOS Action Sheet** used to pick one of 3–5 actions on the current target — the platform-native alternative to a [[Context Menu Pattern|Context Menu]]. Comes with a mandatory Cancel button and a full-width backdrop scrim.

The Driver App uses this pattern (not a custom sheet) whenever a Driver taps a control that offers a handful of short verbs — "Take photo / Choose from library / Cancel", "Edit / Delete / Cancel", currency source pickers, etc.

- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit)
- **Figma page:** `----- Action Sheet (Under Constraction)` — visual scaffold only; there is no shipped custom component. **Use the iOS native `UIAlertController(preferredStyle: .actionSheet)`.**
- **Related pattern:** [[Sheet Pattern]] · Variant 4 (Action Sheet)

---

## The core rule

> **Action Picker** = 3–5 short verbs, one target, one Cancel, native iOS.

If the user is picking an **action** and there are 3–5 of them → Action Picker.
If the user is picking a **value** to display back on the trigger → [[Context Menu Pattern]].
If there are exactly 2 paths, one destructive → [[Sheet Pattern]] · Stack Button Sheet.
If there are ≥ 6 actions, or the actions need helper text / avatars / dividers → [[Sheet Pattern]] · Half Sheet.

---

## Anatomy

```
    ╭──────────────────────────────╮
    │        (scrim, ~30%)         │
    │                              │
    │                              │
    │  ┌────────────────────────┐  │
    │  │  Optional title        │  │
    │  │  Optional message      │  │
    │  ├────────────────────────┤  │
    │  │       Action           │  │
    │  ├────────────────────────┤  │
    │  │       Action           │  │
    │  ├────────────────────────┤  │
    │  │       Delete           │  │   ← destructive · red tint
    │  └────────────────────────┘  │
    │  ┌────────────────────────┐  │
    │  │        Cancel          │  │   ← always present · bold
    │  └────────────────────────┘  │
    │        [safe area]           │
    ╰──────────────────────────────╯
```

| Region | Notes |
|---|---|
| Backdrop scrim | iOS default (~30% black) — handled by `UIAlertController` |
| Sheet container | Native, `Radius/L`-equivalent top+bottom corners on the two grouped blocks |
| Action group | 3–5 rows in a rounded rectangle · `Background/Subtle` |
| Row label | Native iOS text style — 20pt Regular, `Text/Action` (system blue) |
| Destructive row | Same row shape, label in `Text/Negative` (system red) — set via `UIAlertAction.Style.destructive` |
| Cancel block | Separate rounded rectangle, bold label, tinted `Background/Primary` — spatial gap of `Space/S` from the action group |
| Safe area | Cancel sits above the home indicator, respected by iOS |

Do not mock or replicate this with custom shapes — the visual quirks (spacing between groups, Cancel bolding, tap targets) are iOS's job.

---

## Composition rules

| Rule | Value |
|---|---|
| Action count | 3–5 rows, plus Cancel |
| Cancel | **Always present**, always last, in its own block below the actions |
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
| 3–5 actions on the current target, need one Cancel | Action Picker (this pattern) |
| Picking a value the trigger will display afterwards | [[Context Menu Pattern]] |
| Exactly 2 paths, one destructive | [[Sheet Pattern]] · Stack Button Sheet |
| ≥ 6 actions, or rows have avatars / helper text | [[Sheet Pattern]] · Half Sheet with a list |
| Actions target multiple objects (bulk) | [[Sheet Pattern]] · Half Sheet with checkboxes |
| A confirm dialog with title + one primary + one cancel | [[Sheet Pattern]] · Stack Button Sheet |
| Filter or sort selection | [[Context Menu Pattern]] or [[Filter Search Results Pattern]] |

The rule of thumb: Context Menu leaves the user **on the same screen with a new value visible**; an Action Picker leaves the user **on the same screen with something having happened**.

---

## Real Driver App screens using this pattern

Verified against the Driver App `DS` page — see [[_Pattern Evidence Map]] and [[Sheet Pattern]] · Variant 4.

- **Photo Actions (Done)** — Truck Service `662:30875` · "Take photo / Choose from library / Cancel"
- **Picture (Done)** — Profile `667:31697` · profile photo source picker
- **Dropdown (Done)** — Profile `667:31697` · picker rendered as an Action Sheet rather than a Context Menu
- **Select (Done)** — Order Details `667:31707` · same pattern used from an Order row

The **Dropdown** and **Select** entries are examples where the Driver App deliberately uses the Action Picker instead of an anchored [[Context Menu Pattern|Context Menu]] — because the target list is short, the actions are verbs (not value-selection with a persistent selected state), and Cancel is a first-class exit.

---

## Do

- ✅ Use the iOS-native `UIAlertController` — never draw a custom Action Picker.
- ✅ Include Cancel every time. Cancel is what separates an Action Picker from a [[Context Menu Pattern|Context Menu]].
- ✅ Keep to 3–5 actions. Convert to a Half Sheet list once you're at 6+.
- ✅ Put the destructive action second-to-last, right above Cancel.
- ✅ Use verb labels ("Delete", "Take photo") — not "OK" / "Confirm".
- ✅ Chain a [[Sheet Pattern|Stack Button confirmation]] after destructive picks only when the action is truly irreversible.

## Don't

- ❌ Don't ship a custom Action Sheet component — the UIKit page is a scaffold only, and the platform version already handles safe area, dark mode, dynamic type, and accessibility.
- ❌ Don't omit Cancel — even if the sheet is dismissable by tap-outside, iOS users expect the button.
- ❌ Don't stack two destructive actions in one Action Picker — split into two flows.
- ❌ Don't add a title / message unless the target isn't obvious from context; extra text turns an Action Picker into a heavier sheet.
- ❌ Don't use Action Picker for value-selection with a persistent selected state (currency, mode, sort) — that's a [[Context Menu Pattern|Context Menu]].
- ❌ Don't anchor an Action Picker to a specific control (like a Context Menu) — iOS always docks it to the bottom of the screen.
- ❌ Don't nest a picker inside another sheet — dismiss the parent first, then present.

---

Back to [[Patterns]] · [[Design System]].
