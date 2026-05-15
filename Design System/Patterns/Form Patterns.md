# Form Patterns

Guide for designing forms, inputs, and data-entry screens in the Driver App.

---

## Anatomy of a form field

```
Form/Label text (16pt)
┌─────────────────────────────────┐
│  Input text (17pt)              │
└─────────────────────────────────┘
  Error message (13pt, Negative)   ← only visible in error state
```

| Element | Token |
|---|---|
| Label | `Form/Label` text style + `Text/Secondary` color |
| Input text | `Form/Input` text style + `Text/Primary` color |
| Placeholder text | `Form/Input` text style + `Text/Tertiary` color |
| Field background | `Background/Subtle` |
| Border (default) | `Border/Primary` at `Width/XS` (1pt) |
| Border (focused) | `Border/Blue` at `Width/XS` |
| Border (error) | `Border/Negative` at `Width/XS` |
| Border (disabled) | `Border/Disabled` at `Width/XS` |
| Field radius | `Radius/M` (12pt) |
| Field minimum height | 44pt |
| Error label color | `Text/Negative` + `Text/Footnote` text style |
| Gap: label → field | `Space/XS` (4pt) |
| Gap: field → error | `Space/XS` (4pt) |
| Gap: field → next field | `Space/L` (16pt) |

---

## States (required for every input)

| State | Visual indicator |
|---|---|
| Default | `Border/Primary` border |
| Focused | `Border/Blue` border (system highlight) |
| Filled | Same as default, `Text/Primary` label |
| Error | `Border/Negative` border + error message below |
| Disabled | `Background/Disabled` fill + `Text/Disabled` text + `Border/Disabled` border |
| Read-only | No border, `Background/Subtle`, no cursor |

Design all states. Handing off only the default state is a handoff bug.

---

## Form layout rules

**Vertical single-column layout** is the standard for mobile forms. Side-by-side fields are only acceptable for very short, tightly related fields (e.g., expiry month + year on a card).

| Rule | Value |
|---|---|
| Screen horizontal margin | `Space/L` (16pt) |
| Between fields | `Space/L` (16pt) |
| Between field groups / sections | `Space/2XL` (32pt) |
| Submit button bottom margin (above safe area) | `Space/L` (16pt) |
| Submit button width | Fill container (full width minus 2× `Space/L`) |
| Submit button height | 50pt minimum |

---

## Keyboard behavior

- The form should scroll when the keyboard appears — no fields should be hidden behind it
- The focused field should always be visible above the keyboard
- "Return" on the last field should either submit the form or dismiss the keyboard depending on context
- Use `Done` / `Next` keyboard toolbar buttons for multi-field forms

---

## Short form (1–3 fields) — use a Half Sheet

Place inside a half sheet. The keyboard will push the sheet up naturally and the background remains visible, giving the user context.

Example: Add a load note, update a single field.

## Long form (4+ fields) — use a Full Sheet or pushed screen

A half sheet will be too cramped once the keyboard appears. Use a full sheet or push a dedicated screen. Include a nav bar with a Cancel action (left) and Save/Done action (right).

---

## Validation rules

- **Validate on submit** for most cases — don't flag errors as the user types (frustrating)
- **Validate on blur** (when field loses focus) for fields with strict formats (phone number, date)
- **Never clear a field** to show an error — show the error message, keep the user's input
- Always pair an error border with an error message — color alone is insufficient (accessibility rule A1)

---

## Do / Don't

✅ Every form field has a visible label — no placeholder-only inputs
✅ Every field has a disabled state designed
✅ Error states always include a text description of the error, not just red color
✅ Submit button is disabled until minimum required fields are filled
❌ Don't use all-caps labels — use sentence case (matches system conventions)
❌ Don't place destructive actions (delete, clear) near submit — separate them spatially
❌ Don't use border-radius larger than `Radius/M` on inputs — `Radius/L` is for cards

---

Back to [[Design System]] · [[Patterns]] · [[Getting Started]].
