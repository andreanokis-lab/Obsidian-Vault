# Sheet Pattern

How to choose and compose iOS bottom sheets in the Driver App. Three primary variants (Half, Full, Stack Button) plus the iOS Action Sheet as a 4th case. Every sheet decision maps to one of these.

The Sheet itself is an organism (out of scope for individual component docs); the composition rules + every header / button slot are documented here. The header components — [[Components/Title and Controls|Title and Controls]], [[Components/Leading (Sheets)|Leading (Sheets)]], [[Components/Trailing (Sheets)|Trailing (Sheets)]] — are documented individually.

- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit)
- **Figma documentation:** Section `1806:10755` "Sheet Pattern — Documentation" on the `----- Patterns` page

---

## The core rule

> **Half sheet** = user returns to the same screen
> **Full sheet** = user enters a new context
> **Stack Button sheet** = confirm a single decision (especially destructive)
> **Action Sheet** = pick one of 3–5 actions from a list

If dismissing the sheet puts the user back where they were → Half.
If the sheet feels like a new "page" → Full.
If the user must say yes/no to one thing → Stack Button.
If the user picks from a short menu of actions → Action Sheet.

---

## Anatomy (shared across all variants)

| Region | Component / Token |
|---|---|
| Backdrop scrim | Overlays (organism) — dims the screen behind |
| Sheet container | [[Components/Card Base]]-style surface · `Background/Primary` fill · `Radius/L` (16pt) **top corners only** |
| Handle bar (grabber) | 4pt × 36pt, centred · fill `Background/Subtle` (or system grabber on iOS 15+) |
| Header (optional) | [[Components/Title and Controls|Title and Controls]] — title + Leading + Trailing slots |
| ↳ Leading (optional) | [[Components/Leading (Sheets)|Leading (Sheets)]] — Back / Close circle or text button |
| ↳ Trailing (optional) | [[Components/Trailing (Sheets)|Trailing (Sheets)]] — Cancel / Done text button or close circle |
| Content area | Pattern-specific (see variants below) |
| Bottom safe area | Respected — content never overlaps the home indicator |

---

## Variant 1 — Half Sheet (medium detent)

Covers ~50% of the screen. Background visible behind.

**Use when:**
- Short selection (2–5 options in a list)
- Single- or two-field form where keyboard fits naturally
- Filters / sort controls
- Inline pickers (date, value selection)

**Don't use when:**
- Multi-step flow
- Form has 4+ fields — keyboard fights for space → Full Sheet
- User needs full focus

**iOS:** `UISheetPresentationController` with `.medium` detent.

---

## Variant 2 — Full Sheet (large detent)

Covers ~90% of the screen. Background mostly obscured.

**Use when:**
- Multi-step flow requiring full focus (signature capture, multi-field forms)
- Document / photo viewer
- Long forms (4+ fields)
- Sub-navigation inside a flow
- Any sheet that contains its own navigation bar

**Don't use when:**
- Action is a quick confirmation or single selection → Half is less disruptive

**iOS:** `UISheetPresentationController` with `.large` detent.

---

## Variant 3 — Stack Button Sheet

A half sheet whose only content is a title / message + 2–3 stacked Buttons. The most common confirmation pattern, especially for destructive actions.

```
┌─────────────────────────────┐
│         ── grabber ──       │
│                             │
│   Title (Section/Title)     │
│   Optional message          │
│                             │
│   [ Primary action  ]       │   ← [[Components/Button]] Size=L
│   [ Cancel          ]       │   ← Button Size=L · Secondary · Outline
│                             │
│        [safe area]          │
└─────────────────────────────┘
```

**Use when:**
- Confirm a destructive action (delete, remove, cancel trip, sign out)
- Confirm an irreversible state change
- Exactly 2 paths (do it / don't do it)

**Don't use when:**
- 3+ meaningful options → Action Sheet
- Action is reversible and low-stakes → just do it, skip confirmation

---

## Variant 4 — Action Sheet

iOS native action list — 3–5 actions stacked vertically, anchored to the bottom of the screen. Used to pick one action from a short menu.

**Use when:**
- 3–5 actions on the same target (e.g., "Edit photo / Replace / Delete / Cancel")
- One destructive option among neutral options

**Don't use when:**
- Only 2 actions → Stack Button Sheet
- 6+ actions → use a Half Sheet with a `[[Components/Menu|Menu]]` list inside

iOS native: `UIAlertController` with `.actionSheet` style. The DS doesn't ship a custom Action Sheet — use the system one.

---

## Composition rules

| Rule | Value |
|---|---|
| Sheet top corner radius | `Radius/L` (16pt) on the top corners only |
| Sheet background | `Background/Primary` |
| Handle bar | 4pt × 36pt · `Background/Subtle` · centred, `Space/S` (8pt) from the top |
| Horizontal content padding | `Space/L` (16pt) |
| Header padding | `Space/L` × `Space/M` |
| Bottom padding (above safe area) | `Space/L` (16pt) |
| Stack Button gap | `Space/S` (8pt) between buttons |
| Stack Button width | Fill container (full sheet width minus 2 × `Space/L`) |
| Stack Button height | `Space/4XL` (48pt) — Button `Size=L` |
| Destructive button | [[Components/Button]] · `Size=L, Type=Primary, Role=Red` |
| Cancel button | [[Components/Button]] · `Size=L, Type=Secondary, State=Outline` |
| Primary (non-destructive) confirm | [[Components/Button]] · `Size=L, Type=Primary, Role=Inverse` (or `Role=Blue` for confirm) |
| Backdrop scrim opacity | System default (~30% black) — handled by `UISheetPresentationController` |

---

## Header — when to include

| Sheet has… | Header |
|---|---|
| Title only | Title and Controls — title centred, no Leading / Trailing |
| Cancel + Save | Title centre, Leading = "Cancel" text button, Trailing = "Save" text button |
| Back navigation (sub-step) | Leading = circle Back button, title centred |
| Dismiss only | Trailing = circle Close button (✕) |
| No header | Stack Button sheets / Action Sheets — grabber is enough |

---

## Real Driver App screens using this pattern

Verified against the Driver App DS page on 2026-05-21. See [[_Pattern Evidence Map]].

### Half Sheet
- **Sheet (Done)** — Truck Service `662:30875` · half sheet for adding a service
- **Add Driver Notes (Done)** — Order Details `667:31707` · half sheet with Text Area
- **Receipts Add COP/COD (Done)** — Receipts `662:30759` · sheet form

### Full Sheet
- **Аdd Photo Receipts (Done)** — Receipts `662:30759` / Adjustments `737:21382` · multi-photo camera sheet
- **Customer Template (Done)** — Order Details `667:31707` · template picker

### Stack Button Sheet (destructive)
- **Deleting Reciept (Done)** — Receipts `662:30759`
- **Deleting Image (Long Press) (Done)** — Receipts
- **Deleting (Done)** — Files `667:31228`
- **Deleting Acc (Done)** — Settings `667:31696`
- **Remove Alert (Done)** — Truck Service `662:30875`
- **Alert** — top-level `1:28890`

### Action Sheet
- **Photo Actions (Done)** — Truck Service `662:30875` · "Take photo / Choose from library / Cancel" trio
- **Picture (Done)** — Profile `667:31697` · profile photo source picker
- **Dropdown (Done)** — Profile `667:31697`
- **Select (Done)** — Order Details `667:31707`

---

## Do

- ✅ Match variant to recovery context — Half for "return to screen", Full for "new context".
- ✅ Always show a dismiss affordance — grabber + swipe-down, or explicit Cancel button.
- ✅ For destructive Stack Button sheets, put Cancel **below** the destructive button — the secondary position.
- ✅ Use the destructive verb as the button label ("Delete", "Sign out") — not "Confirm".
- ✅ Use a Full Sheet when the sheet contains its own navigation.
- ✅ Use `Radius/L` only on the top corners — the bottom hugs the safe area.

## Don't

- ❌ Don't stack 4+ buttons in a Stack Button Sheet — switch to Action Sheet or list-based Half Sheet.
- ❌ Don't use a Full Sheet for a single-line confirmation — it feels heavy.
- ❌ Don't block swipe-to-dismiss unless the user has unsaved data — and then prompt before dismissing.
- ❌ Don't put a Navigation Bar inside a Half Sheet — use Title and Controls header instead.
- ❌ Don't use `Radius/L` on all four sheet corners — the bottom corners are hidden against the safe area; rounding looks broken.
- ❌ Don't override the grabber color — use `Background/Subtle` (or the system grabber on iOS 15+).

---

Back to [[Patterns]] · [[Design System]].
