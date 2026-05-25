# Error State Pattern

How to communicate errors at four levels of severity — inline (field), inline (section), modal (action confirmation), and full-screen (network / server failure). Each level uses a different composition; choose by the user's recovery path.

- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit)
- **Figma documentation:** Section `1786:9860` "Error State Pattern — Documentation" on the `----- Patterns` page

---

## Four sub-patterns — pick by recovery path

| Sub-pattern | Composition | Use when |
|---|---|---|
| **Inline field error** | [[Components/Input|Input]] (`State=Negative`) + populated `Helper` | A specific form field is invalid (bad format, missing value) |
| **Inline section error** | [[Components/Alert Section Base|Alert Section Base]] (`Alert=Negative`) | A whole section or step has failed; user stays on the screen |
| **Modal confirmation (destructive)** | [[Sheet Pattern|Sheet]] (Action Sheet detent) with [[Components/Button|Button]] (`Role=Red`) | Action is destructive (delete, sign out) — confirm before executing |
| **Full-screen error** | Icon + headline + body + [[Components/Button|Button]] retry CTA, centred (mirrors [[Empty State Pattern]] layout) | Network failure, server unreachable, content can't load at all |

---

## Anatomy by sub-pattern

### Inline field error

| Element | Component / token |
|---|---|
| Field | [[Components/Input|Input]] · `State=Negative` |
| Helper line | populated with error text · auto-shows via Input's `Helper` slot · text color `Text/Negative` (set by Negative state) |
| Field border | `Border/Negative` (set by Negative state) |

### Inline section error

| Element | Component / token |
|---|---|
| Container | [[Components/Alert Section Base|Alert Section Base]] · `Alert=Negative, Stroke=True` |
| Leading icon (optional inside Slot) | `Icon/Negative` |
| Body text | `Text/Body` (17pt Regular) · `Text/Primary` |
| Optional retry / dismiss action | [[Components/Button|Button]] · `Size=S, Type=Ghost` inside the Slot |

### Modal confirmation (destructive)

| Element | Component / token |
|---|---|
| Container | [[Sheet Pattern|Sheet]] (Action Sheet detent — short half-sheet) |
| Title | `Section/Title` (20pt Title 3) · `Text/Primary` — what's about to happen ("Delete this receipt?") |
| Body | `Text/Body` · `Text/Secondary` — consequences ("This can't be undone") |
| Primary action | [[Components/Button|Button]] · `Size=L, Type=Primary, Role=Red` — the destructive verb ("Delete") |
| Secondary action | [[Components/Button|Button]] · `Size=L, Type=Secondary, State=Outline` — "Cancel" |

### Full-screen error

| Element | Component / token |
|---|---|
| Icon | SF Symbol (`wifi.slash` for offline, `exclamationmark.triangle.fill` for server error) · 56–80pt · `Icon/Negative` |
| Headline | `Section/Title` (20pt Title 3) · `Text/Primary` — honest, not alarming ("Couldn't load trips") |
| Message | `Text/Body` · `Text/Secondary` · max 280pt wide — what to do next ("Check your connection and try again") |
| Retry CTA | [[Components/Button|Button]] · `Size=L, Type=Primary, Role=Inverse` — "Try again" |

---

## Composition rules

| Rule | Value |
|---|---|
| Field error → next sibling gap | inherits the form's `Space/L` (16pt) between fields |
| Inline section error spacing inside container | padding `Space/S` × `Space/XS` (component default) |
| Modal confirmation button gap (Cancel ↔ Destructive) | `Space/S` (8pt) — vertically stacked iOS style |
| Modal Cancel always present | iOS HIG: never offer a destructive action without a Cancel |
| Full-screen error positioning | centred in available content area (same as [[Empty State Pattern]]) |
| Color alone is not the signal | pair red color with explicit text — required for accessibility |

---

## Choosing severity

Match the sub-pattern to the recovery context, not just "is it bad?":

| Situation | Sub-pattern |
|---|---|
| User typed an invalid email | Inline field error |
| Server rejected the saved form (multiple things wrong) | Inline section error at the top of the form |
| User tapped "Delete receipt" | Modal confirmation |
| List can't load — no network | Full-screen error |
| Photo upload failed mid-flow | Inline section error in the photo row OR Toast (non-blocking) |
| User tapped "Sign out" | Modal confirmation |

---

## Real Driver App screens using this pattern

Verified against the Driver App DS page on 2026-05-21. See [[_Pattern Evidence Map]].

### Modal confirmation (destructive)
- **Alert** — top-level reference `1:28890`
- **Remove Alert (Done)** — Truck Service `662:30875` · "Remove service?" confirm
- **Long Press (Deleting) (Done)** — Truck Service · destructive action sheet
- **Deleting Reciept (Done)** — Receipts `662:30759`
- **Deleting Image (Long Press) (Done)** — Receipts · long-press destructive sheet
- **Deleting (Done)** — Files `667:31228`
- **Deleting Acc (Done)** — Settings `667:31696` · account deletion (highest-stakes)

### Inline field / section error
- **Not Match (Done)** — Change Pass `667:31702` · password fields in `Negative` state with error message
- **VIN Doesn't Match** — ORDERS `1:30405` / Scan VIN `736:40323` · validation failure on captured VIN

### Full-screen error
- **Alert (Done)** — Scan VIN `736:40323` · scan failed alert
- **Something Wrong w/ VIN (Done)** — Scan VIN `736:40323` · unknown server failure with retry

---

## Do

- ✅ Pair every error with **descriptive text** explaining what went wrong and what to do — color or icon alone fails accessibility.
- ✅ For destructive actions, **always show Cancel** alongside the destructive verb. iOS HIG: don't surprise the user.
- ✅ Use the destructive verb as the button label (`Delete`, `Sign out`, `Remove`) — not generic "Confirm".
- ✅ Match the sub-pattern to the **recovery path**, not the severity emotion.
- ✅ Use full-screen error only when nothing else can render — otherwise prefer inline.
- ✅ Centre full-screen errors in the available content area (same as Empty State).

## Don't

- ❌ Don't use humorous or playful copy for errors — drivers are working under time pressure.
- ❌ Don't show modal alerts for routine warnings — use inline section error instead.
- ❌ Don't omit the recovery path. Every error needs a way out: Retry, Cancel, Edit, or a clear next action.
- ❌ Don't use `Background/Primary Red` for non-destructive actions — users pattern-match red to destruction.
- ❌ Don't rely on `Negative` field border without a populated `Helper` — see [[Components/Input|Input]] doc.
- ❌ Don't stack two destructive actions in one modal — pick the single one.

---

Back to [[Patterns]] · [[Design System]].
