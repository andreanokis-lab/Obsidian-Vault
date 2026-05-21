# Loading Skeleton Pattern

How to show loading state while data is fetching. The Driver App uses two mechanisms:

1. **Native iOS activity indicator** (system spinner) — for short or generic loads. iOS HIG-standard, no DS component.
2. **Content skeleton** — placeholder shapes that mirror the eventual content layout. Only one is documented in the DS: the [[Components/Titles|Titles]] `Place=Skeleton` variant used in the Leaderboard's loading state.

This pattern is narrowly scoped because the Driver App doesn't have many designed skeleton placeholders — most loading is handled by the OS-level activity indicator. Don't invent new skeletons unless a real screen needs one.

- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit)
- **Figma documentation:** Section `1786:9986` "Loading Skeleton Pattern — Documentation" on the `----- Patterns` page

---

## When to use which loading affordance

| Situation | Affordance |
|---|---|
| Initial load of a screen, < 1s expected | Native iOS activity indicator (small spinner, centred) |
| Initial load of a screen, 1–3s expected | Native activity indicator + brief "Loading…" caption (`Meta/Caption` · `Text/Tertiary`) |
| List of content arriving (variable timing) | Skeleton placeholder rows — preserve layout while data loads |
| Hero / above-the-fold content (leaderboard podium) | Use the [[Components/Titles|Titles]] `Place=Skeleton` variant |
| Mid-flow action (saving, submitting) | Disable the action button + show inline activity indicator inside it |
| Background refresh of already-loaded content | No loading state — leave the previous content visible until refresh completes |

iOS HIG: don't show a loading state if the load completes in under ~250ms — the flicker is worse than the wait.

---

## Anatomy

### Native iOS activity indicator

Not a designed component. Use the system spinner — `UIActivityIndicatorView` at runtime. In Figma, represent with a small circle / SF Symbol `arrow.triangle.2.circlepath` placeholder if a mock is needed for the spec.

| Element | Token / Style |
|---|---|
| Spinner color | `Icon/Subtle` |
| Optional caption | `Meta/Caption/*` (12pt) · `Text/Tertiary` |
| Caption position | Below the spinner, gap `Space/S` (8pt) |
| Vertical centring | Centred in available content area |

### Content skeleton — Titles (Leaderboard)

The only documented skeleton variant in the DS.

| Element | Component / token |
|---|---|
| Container | [[Components/Titles|Titles]] · `Place=Skeleton` — preserves the podium layout |
| Placeholder shapes | Internal to the Titles Skeleton variant — neutral-tinted shapes matching the eventual name + stats positions |
| Animation (runtime) | Subtle shimmer / pulse — not a Figma asset; implementation detail |

Skeletons should match the **layout** of the eventual content (same row count, same proportions), not the **exact dimensions of every text run**.

---

## Composition rules

| Rule | Value |
|---|---|
| Don't show loading for <250ms operations | iOS HIG — flicker hurts more than the wait |
| Spinner colour | `Icon/Subtle` — quiet, not attention-grabbing |
| Skeleton background fill | `Background/Subtle` for placeholder shapes — same as content surfaces |
| Skeleton corner radius | Match the real content (`Radius/S` for cards, `Radius/Pill` for pills, etc.) |
| Don't combine skeleton + spinner | Pick one per region |
| Vertical centring (spinner-only loads) | Centre in available content area, same as Empty State |
| Skeleton row count | Match the eventual data (e.g., 3 rows for a 3-driver podium) |

---

## Real Driver App screens using this pattern

Verified against the Driver App DS page on 2026-05-21. See [[_Pattern Evidence Map]].

- **Leaderboard / Placeholder (Done)** — Leaderboard section `667:31703` · uses [[Components/Titles|Titles]] `Place=Skeleton` in the podium position before driver data loads
- **All other "Placeholder" frames** found in the DS scan are **Empty States**, not loading states — see [[Empty State Pattern]] for those

The Driver App overwhelmingly relies on the native iOS activity indicator for loading; the Leaderboard Skeleton is the single designed exception.

---

## Do

- ✅ Use the native iOS activity indicator for most loading — it's the system standard.
- ✅ Use the [[Components/Titles|Titles]] `Place=Skeleton` variant for the Leaderboard's loading state.
- ✅ If a new skeleton is needed elsewhere, match it to the eventual content's **layout** (row count, proportions), not pixel-perfect dimensions.
- ✅ Skip the loading state entirely if the operation completes in under ~250ms (iOS HIG).
- ✅ For mid-flow actions (Save, Submit), disable the action button and show an inline spinner inside it.

## Don't

- ❌ Don't invent custom skeletons without a real screen need — the DS doesn't have them by design.
- ❌ Don't show a skeleton **and** a spinner in the same region — pick one.
- ❌ Don't show a loading state during background refresh of already-loaded content — keep the previous content visible.
- ❌ Don't use `Icon/Primary` for the spinner — it draws too much attention; use `Icon/Subtle`.
- ❌ Don't pair the spinner with alarming copy ("Don't close this app") — drivers under time pressure don't need extra anxiety.

---

Back to [[Patterns]] · [[Design System]].
