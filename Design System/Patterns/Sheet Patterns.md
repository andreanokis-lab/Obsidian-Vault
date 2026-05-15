# Sheet Patterns

Guide for choosing and building sheets (bottom sheets / modals) in the Driver App. Every sheet decision should map to one of these patterns.

---

## The core rule

> **Half sheet = user returns to the same screen.**
> **Full sheet = user enters a new context.**

If dismissing the sheet puts the user back where they were — use half.
If the sheet feels like navigating into a new "page" — use full.

---

## Pattern 1 — Half Sheet (medium detent)

**What it is:** Covers ~50% of the screen. The content behind it remains visible. Feels lightweight and temporary.

**Use when:**
- Quick confirmation of a single action
- Short selection (2–5 options in a list)
- Single-field or two-field form where keyboard fits naturally
- Filters / sort controls that don't need the full screen

**Do not use when:**
- The content is a multi-step flow
- The form has 4+ fields (keyboard + content will fight for space)
- The user needs full focus and cannot be distracted by what's behind

**HIG backing:** `UISheetPresentationController` with `.medium` detent.

---

## Pattern 2 — Full Sheet (large detent)

**What it is:** Covers ~90% of the screen. Background is fully obscured. Feels like a new page.

**Use when:**
- Multi-step flow requiring full focus (e.g., signature capture, expense entry)
- Document viewer, photo viewer, camera roll
- Long forms (4+ fields)
- Sub-navigation or a second level inside a flow
- Any sheet that contains its own navigation

**Do not use when:**
- The action is a quick confirmation or single selection — half is less disruptive

**HIG backing:** `UISheetPresentationController` with `.large` detent.

---

## Pattern 3 — Stack Button Sheet

**What it is:** A half sheet whose only content is a title/message (optional) and 2–3 stacked buttons. The most common confirmation pattern.

```
┌─────────────────────────────┐
│         ── handle ──        │
│                             │
│   Optional title or message │
│                             │
│   ┌─────────────────────┐   │
│   │   Primary Action    │   │
│   └─────────────────────┘   │
│   ┌─────────────────────┐   │
│   │      Cancel         │   │
│   └─────────────────────┘   │
│                             │
│         [safe area]         │
└─────────────────────────────┘
```

**Use when:**
- Confirm a destructive action (delete, remove, cancel trip)
- Confirm an irreversible state change
- Offer exactly 2 paths (do it / don't do it)

**Do not use when:**
- There are 3+ meaningful options (use an action list instead)
- The action is reversible and low-stakes (just do it directly, no confirmation needed)

---

## HaulEx Driver App — which pattern to use

| Scenario | Pattern |
|---|---|
| "Delete this photo?" | Stack Button Sheet (Primary Red + Cancel) |
| "End trip?" confirmation | Stack Button Sheet |
| Company filter options | Half Sheet (list of tappable rows) |
| Add a short load note | Half Sheet (keyboard form) |
| Full photo review with metadata | Full Sheet |
| Signature capture | Full Sheet |
| Expense / receipt entry (multi-field) | Full Sheet |
| Sort options (3–5 choices) | Half Sheet (list) |

---

## Token spec for sheets

| Element | Token |
|---|---|
| Sheet background | `Background/Primary` |
| Sheet corner radius (top) | `Radius/L` (16pt) |
| Handle bar background | `Background/Subtle` |
| Handle bar size | 4pt × 36pt, centered |
| Horizontal padding | `Space/L` (16pt) |
| Bottom padding (above safe area) | `Space/L` (16pt) |
| Gap between stacked buttons | `Space/S` (8pt) |
| Button minimum height | 50pt (exceeds 44pt HIG minimum) |
| Primary button (confirm) | `Background/Primary Blue` or contextual color |
| Destructive button (delete) | `Background/Primary Red` |
| Cancel / secondary button | `Background/Subtle` (no border) |
| Primary button label | `Text/Primary Inverse Static` (white) |
| Cancel button label | `Text/Primary` |
| Optional title | `Section/Title` text style |
| Optional message | `Text/Body` + `Text/Secondary` color |

---

## Do / Don't

✅ Always provide a visible dismiss affordance (handle bar + swipe down, or explicit Cancel button)
✅ For destructive actions, make Cancel the bottom (secondary) button — the less prominent position
✅ Use the full sheet when the sheet needs its own navigation bar or back button
❌ Don't stack more than 3 buttons — use a list-based sheet instead
❌ Don't use a full sheet for a single-line confirmation — it feels heavy
❌ Don't block swipe-to-dismiss unless the user has unsaved data (and then prompt before dismissing)

---

Back to [[Design System]] · [[Patterns]] · [[Getting Started]].
