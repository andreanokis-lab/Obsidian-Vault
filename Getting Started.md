# Getting Started — HaulEx Design System

> Read this before opening Figma. It takes 10 minutes and will save you hours.

**Design System Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit)
**Driver App Figma file:** [HaulEx Driver App](https://www.figma.com/design/yhxCSzJrafZbqXGZOCBCKE/HaulEx-Driver-App)

---

## The one thing you must understand first

The design system uses a **two-layer token system**:

```
Primitives  →  Semantics  →  Your design
(raw values)   (role aliases)   (always here)
```

- **Primitives** are raw scales: `neutral/950`, `blue/500`, `red/300`. They have no meaning — just a value.
- **Semantics** are role-based aliases: `Text/Primary`, `Background/Subtle`, `Icon/Negative`. They tell you *what the token is for*.

**Rule:** You always use semantics. You never touch primitives directly. This is how Light/Dark mode works — swap the semantic mode, all your colors update automatically.

---

## What's in the Figma library

| Category | Status | Notes |
|---|---|---|
| Colors: Primitives | ✅ Complete | 58 color tokens — do not use directly |
| Colors: Semantic | ✅ Complete | Light + Dark modes — use these |
| Spacing | ✅ Complete | 18 tokens, 0–112pt |
| Border (Radius + Width) | ✅ Complete | 11 tokens |
| Typography: Primitives | ✅ Complete | Font size/weight ramp — do not use directly |
| Typography: Semantic | ✅ Complete | iOS roles — use these |
| Components | 🔄 In progress | See [[Component Status]] |

---

## Before designing any screen

1. **Read [[Rules]]** — 5 categories, ~15 rules. Non-negotiable.
2. **Check [[Component Status]]** — does the component you need exist? Use it if so.
3. **Choose your tokens** — semantic colors + semantic typography only.
4. **Design in both modes** — Light and Dark. Every screen, every state.
5. **Verify touch targets** — every tap target ≥ 44×44pt.

---

## Your workflow for a new screen

```
1. Identify the screen type → check [[Patterns]] for the right pattern
2. Pick layout → 16pt margins, respect safe areas (see [[Rules]] L1–L4)
3. Drop in components from the library (check [[Component Status]])
4. Apply semantic tokens for any custom elements
5. Build Dark mode variant using the same Figma frame, toggle variable mode
6. Run through the P0–P1 audit checklist (use [[Company Filter Not Found - Sprint Checklist]] as template)
```

---

## Quick token reference

| I need... | Token to use |
|---|---|
| Main text | `Text/Primary` |
| Supporting/label text | `Text/Secondary` |
| Hint / placeholder | `Text/Tertiary` |
| Disabled text | `Text/Disabled` |
| Link / action text | `Text/Link` |
| Error text | `Text/Negative` |
| Success text | `Text/Positive` |
| Page background | `Background/Primary` |
| Card / row background | `Background/Subtle` |
| Primary button fill (blue) | `Background/Primary Blue` |
| Destructive button fill | `Background/Primary Red` |
| Success button fill | `Background/Primary Green` |
| Divider line | `Border/Subtle` |
| Input border (default) | `Border/Primary` |
| Input border (focused) | `Border/Blue` |
| Input border (error) | `Border/Negative` |
| Primary icon | `Icon/Primary` |
| Secondary / decorative icon | `Icon/Subtle` |
| Screen margin | `Space/L` (16pt) |
| Row vertical padding | `Space/M` (12pt) |
| Element gap | `Space/S` (8pt) |
| Section separation | `Space/XL` (24pt) |
| Card radius | `Radius/L` (16pt) |
| Input radius | `Radius/M` (12pt) |
| Pill button radius | `Radius/Pill` (999) |

---

## Typography quick reference

| Context | Style to use |
|---|---|
| Screen nav title | `Screen/Title` — 17pt Semibold |
| Section header | `Section/Title` — 20pt Regular |
| Body copy | `Text/Body` — 17pt Regular |
| Supporting text | `Text/Secondary` — 16pt Regular |
| List row main label | `List/Title` — 17pt Regular |
| List row sub-label | `List/Subtitle` — 16pt Regular |
| Form field label | `Form/Label` — 16pt Regular |
| Form field input text | `Form/Input` — 17pt Regular |
| Caption / metadata | `Meta/Caption` — 12pt Regular |
| Footnotes / hints | `Text/Footnote` — 13pt Regular |

Apply these via Figma's text style panel — never set font size manually.

---

## Key links

- [[Design System]] — full token + component hub
- [[Rules]] — non-negotiable design rules
- [[Component Status]] — what's built, what's in progress
- [[Patterns]] — sheet, navigation, form, empty state guides
- [[Architecture]] — token philosophy and naming conventions
- [[Driver App]] — app-level screen specs and flow docs
