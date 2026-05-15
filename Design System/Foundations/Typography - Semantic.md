# Typography — Semantic

Semantic typography tokens. 50 variables across 10 roles, **iOS mode only**. Each role maps to [[Typography - Primitives|primitive]] values for family, size, weight, line-height, and letter-spacing.

**Always apply via [[Text Styles]] in Figma — never set font, size, or spacing manually.**

- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit)
- **Collection:** `Typography: Semantic`
- **Mode:** iOS (single mode)
- **Total tokens:** 50 (10 roles × 5 properties)
- **Visualization:** Section `1698:3169` "Semantic Typography — Visualization" on `----- Typography` page — 10-role reference table with live text samples, spec columns, and group separators.

---

## How to apply

Text styles are published in Figma under `Semantic/iOS/<Role>`. Select text, open the text style picker, and choose the role. The style binds all five properties at once — family, size, weight, line-height, letter-spacing.

Never set individual values manually. Manual overrides break Dynamic Type and become stale when the primitive scale is updated.

---

## Token spec

| Role             | iOS primitive | Family      | Size | Weight   | Line-height | Letter spacing |
| ---------------- | ------------- | ----------- | ---- | -------- | ----------- | -------------- |
| `Screen/Title`   | Headline      | SF Pro      | 17pt | Semibold | 22          | −0.43          |
| `Section/Title`  | Title 3       | SF Pro      | 20pt | Regular  | 25          | +0.38          |
| `Text/Body`      | Body          | SF Pro Text | 17pt | Regular  | 22          | −0.408         |
| `Text/Secondary` | Subheadline   | SF Pro Text | 15pt | Regular  | 20          | −0.45          |
| `Text/Footnote`  | Footnote      | SF Pro Text | 13pt | Regular  | 13†         | −0.078         |
| `List/Title`     | Body          | SF Pro Text | 17pt | Regular  | 22          | −0.408         |
| `List/Subtitle`  | Subheadline   | SF Pro Text | 15pt | Regular  | 20          | −0.45          |
| `Form/Label`     | Subheadline   | SF Pro Text | 15pt | Regular  | 20          | −0.45          |
| `Form/Input`     | Body          | SF Pro Text | 17pt | Regular  | 22          | −0.408         |
| `Meta/Caption`   | Caption 1     | SF Pro Text | 12pt | Regular  | 16          | 0              |

† `Text/Footnote` line-height = 13pt = same as size. Intentional tight single-line spacing for hint/legal text. Do not use for multi-line copy.

---

## When to use

| Role | Use for |
|---|---|
| `Screen/Title` | Navigation bar title only — the centred label in the nav bar |
| `Section/Title` | In-page section headers — grouping content within the scrollable area |
| `Text/Body` | All paragraph copy, main content blocks, multi-line descriptions |
| `Text/Secondary` | Supporting text: subtitles under a headline, inline descriptions, callout text |
| `Text/Footnote` | Hint text below form inputs, legal disclaimers, inline validation support copy |
| `List/Title` | Primary label in any list row — driver name, item title, status label |
| `List/Subtitle` | Secondary label in a list row — metadata, date, subtext beneath the primary label |
| `Form/Label` | Label placed above an input field — "First Name", "Password", etc. |
| `Form/Input` | Text typed inside an input field; also placeholder text (pair with `Text/Tertiary` color) |
| `Meta/Caption` | Timestamps, badge labels, fine-print tags, photo counts |

---

## Don't

- ❌ Do not set font, size, weight, or spacing manually — always use the Figma text style. Manual values bypass Dynamic Type and go stale when primitives change.
- ❌ Do not use `Screen/Title` for in-page section headers — it is strictly for the navigation bar title. Use `Section/Title` for anything inside the scrollable content area.
- ❌ Do not use `Text/Body` and `List/Title` interchangeably because they share 17pt. `List/Title` is semantically tied to list rows; `Text/Body` is for flowing paragraph content. They will diverge if the scale changes.
- ❌ Do not use `Text/Footnote` for multi-line body copy — its 1:1 line-height ratio (13/13) is unreadable at length. Use `Text/Body` or `Text/Secondary` for anything more than a single line of support text.
- ❌ Do not use `Meta/Caption` for anything that must be read in a primary context — 12pt is the system minimum and is for supplementary information only.
- ❌ Do not apply `Form/Label` to a navigation bar title. Visual similarity (both 15–17pt Regular) is coincidental. Semantic role matters when the token values change.
- ❌ Do not go below `Meta/Caption` (12pt) — no token exists below this. Anything smaller violates both the system minimum and Apple HIG.

---

## Quick lookup

| UI element | Style |
|---|---|
| Navigation bar title | `Screen/Title` |
| In-page section header | `Section/Title` |
| Body paragraph | `Text/Body` |
| Supporting / secondary sentence | `Text/Secondary` |
| List row main label | `List/Title` |
| List row detail / subtitle | `List/Subtitle` |
| Form field label | `Form/Label` |
| Input field text | `Form/Input` |
| Placeholder text | `Form/Input` + color `Text/Tertiary` |
| Caption / timestamp | `Meta/Caption` |
| Hint / footnote below field | `Text/Footnote` |
| Inline validation error | `Text/Footnote` + color `Text/Negative` |

Back to [[Design System]] · [[Rules]] · [[Text Styles]].
