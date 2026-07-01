# Patterns

Compositional design patterns for the HaulEx Driver App. Each pattern documents how multiple components combine into a recurring UI shape, with composition rules, real Driver App screen evidence, and Do / Don't guidance.

Evidence for every pattern is verified against the Driver App `DS` page — see [[_Pattern Evidence Map]] for the cross-reference.

---

## Generic patterns

| Pattern | What it solves |
|---|---|
| [[Form Pattern]] | Multi-field data entry — Input / Text Area / Toggle / Button into a submit screen or sheet |
| [[List with Actions Pattern]] | Scrollable list where each row has a tap target or control (chevron, toggle, picker, count) |
| [[Empty State Pattern]] | Icon + headline + body + optional CTA when a screen / list has nothing to show |
| [[Error State Pattern]] | Inline field, inline section, modal confirmation, full-screen — picked by recovery path |
| [[Loading Skeleton Pattern]] | Native iOS activity indicator vs the one documented skeleton (Leaderboard Titles `Place=Skeleton`) |
| [[Section Header Pattern]] | Plain title · title + trailing action · or full Action Section component |

## HaulEx-specific patterns

| Pattern | What it solves |
|---|---|
| [[Camera Capture Flow]] | End-to-end photo capture: entry → camera → review → attach. Single-photo vs multi-photo. |
| [[Take Photo Screen Pattern]] | Static composition of the camera screen — Top Bar + Viewfinder + Zoom + Camera Actions + Bottom Bar |
| [[Leaderboard Pattern]] | Olympic-podium (2 · 1 · 3) of Places Segments + Leaderboard Row list for ranks 4+ |
| [[Sheet Pattern]] | Half · Full · Stack Button · Action Sheet — pick by recovery context |
| [[Filter Search Results Pattern]] | Search Bar + chips composition with the no-results sub-case of the Empty State Pattern |
| [[Photo Viewer Pattern]] | Native iOS 18 viewer for attached/captured photos — single-photo (portrait) and gallery (landscape) variants sharing one shell |

---

## How patterns relate

- A **List with Actions** that has zero rows → falls into the [[Empty State Pattern]]. If the user filtered, it's the [[Filter Search Results Pattern]] sub-case.
- A **Form** with 1–2 fields → presented in a Half Sheet ([[Sheet Pattern]]).
- A **Form** with 4+ fields → presented in a Full Sheet or a pushed screen.
- An **Error** inside a Form → [[Error State Pattern]] · Inline field sub-pattern (Input `State=Negative`).
- An **Error** at the screen level → [[Error State Pattern]] · Full-screen sub-pattern (mirrors Empty State layout).
- **Loading** that takes longer than ~250ms → [[Loading Skeleton Pattern]]. The Leaderboard uses the Titles `Place=Skeleton`.
- **Camera Capture Flow** wraps around the [[Take Photo Screen Pattern]] composition.

---

## How to use these patterns

1. Identify which patterns apply to the screen you're designing — most screens combine 2–3.
2. Read the **Composition rules** table in each pattern — these list the exact `Space/*`, `Radius/*`, and `Color/*` tokens to apply.
3. Read the **Do / Don't** section — these capture the most common composition mistakes.
4. Cite the matching real screen from [[_Pattern Evidence Map]] in your design rationale.

If a screen requires a new pattern not documented here, design it and add a new note in this folder following the slim template.

---

Back to [[Design System]] · [[Getting Started]].
