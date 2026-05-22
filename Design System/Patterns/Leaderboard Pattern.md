# Leaderboard Pattern

How to compose the driver leaderboard — a 3-driver podium at the top followed by a list of remaining ranks. Used in the Driver App's gamification surface to show driver standings (vehicles delivered, trips completed).

Composes [[Components/Places Segments|Places Segments]] (the podium spots), [[Components/Titles|Titles]] (name + stats), and [[Components/Leaderboard Row|Leaderboard Row]] (compact rows for rank 4+).

- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit)
- **Figma documentation:** Section `1803:10591` "Leaderboard Pattern — Documentation" on the `----- Patterns` page

---

## Anatomy

Vertical stack: podium → divider → list of ranks 4+.

```
┌─────────────────────────────┐
│  ◯ 2nd     ◯ 1st     ◯ 3rd  │  ← Podium: 3 Places Segments
│   ▢▢▢       ▢▢▢       ▢▢▢   │     (Yellow ring on 1st)
│                              │
│  ─────────────────────────  │  ← Divider (optional)
│                              │
│  4   ▢  Driver Name   24 4   │  ← Leaderboard Row (rank 4)
│  5   ▢  Driver Name   18 3   │  ← Leaderboard Row (rank 5)
│  6   ▢  Driver Name   12 2   │  ← …continues
└─────────────────────────────┘
```

| Region | Components |
|---|---|
| **Podium** | 3 × [[Components/Places Segments|Places Segments]] (1st `First place`, 2nd and 3rd `2-3 Places`) |
| ↳ Avatar / Image | Inside Places Segments — yellow ring (`Border/Yellow`) on 1st only, neutral on 2nd/3rd |
| ↳ Rank Badge | Inside Places Segments — `Background/Primary Yellow` pill with rank number |
| ↳ Titles block | [[Components/Titles|Titles]] (`Place=1st Place` or `2nd - 3nd Places`) — name + Vehicles + Trips stats |
| **Divider (optional)** | [[Components/Divider|Divider]] · Horizontal · `Width/XS` · `Border/Subtle` |
| **Rank list (4+)** | Repeating [[Components/Leaderboard Row|Leaderboard Row]] instances |
| ↳ Each row | rank number + avatar / initials + name + Vehicles + Trips |

---

## Composition rules

| Rule | Value |
|---|---|
| Screen horizontal margin | `Space/L` (16pt) |
| Podium internal spacing | Inherited from Places Segments — don't override |
| Podium → divider gap | `Space/XL` (24pt) |
| Divider → first row gap | `Space/M` (12pt) |
| Between Leaderboard Rows | Built-in divider on each row (`Show divider=true`); hide on the **last** row |
| 1st place visual priority | Centred and larger — Places Segments `First place` variant handles this |
| Rank order in the podium | **2 · 1 · 3** (1st in the middle) — Olympic podium convention |
| Initials fallback | When a driver has no photo, show 2-letter initials (Places Segments / Leaderboard Row both support this) |

---

## States

| State | Composition |
|---|---|
| **Populated** | Full podium + rank-list as above |
| **Single driver** | One Places Segments `First place` only — no podium structure (see screen "One (Done)") |
| **Loading** | Use [[Components/Titles|Titles]] `Place=Skeleton` inside each podium spot. See [[Loading Skeleton Pattern]] |
| **Empty** | Empty State Pattern with leaderboard-specific copy ("No standings yet") |

---

## Real Driver App screens using this pattern

Verified against the Driver App DS page on 2026-05-21. See [[_Pattern Evidence Map]].

| Screen | Section | State |
|---|---|---|
| **Leaderboard (Done)** | Leaderboard `667:31703` | Populated — full podium + ranks 4+ |
| **One (Done)** | Leaderboard `667:31703` | Single-driver state |
| **Placeholder (Done)** | Leaderboard `667:31703` | Loading / skeleton (uses Titles Place=Skeleton) |

---

## Why this pattern is special

- **Podium uses Olympic convention** — 1st centred, 2nd left, 3rd right. Don't sort left-to-right by rank.
- **Yellow ring on 1st only** — encoded in Places Segments via `Border/Yellow` on Width/M (3pt, HIG-aligned). Other ranks use a neutral ring.
- **Stats are always Vehicles + Trips** — the leaderboard scores these two metrics specifically. Don't extend without product confirmation.
- **Loading uses the Titles Skeleton variant** — the only documented skeleton in the entire DS (see [[Loading Skeleton Pattern]]).

---

## Do

- ✅ Order the podium **2 · 1 · 3** — Olympic convention, with 1st place centred.
- ✅ Use `First place` variant only for rank 1; `2-3 Places` for ranks 2 and 3.
- ✅ Show initials when no driver photo is available.
- ✅ Use `Show divider=false` on the last [[Components/Leaderboard Row|Leaderboard Row]] in the list.
- ✅ Fall back to [[Empty State Pattern]] when there's no leaderboard data.
- ✅ Use the [[Components/Titles|Titles]] `Place=Skeleton` variant during initial load, per [[Loading Skeleton Pattern]].

## Don't

- ❌ Don't sort the podium left-to-right by rank — 1st centred is the convention drivers expect.
- ❌ Don't use [[Components/Leaderboard Row|Leaderboard Row]] for the top 3 — they get the podium (Places Segments).
- ❌ Don't extend the stats beyond Vehicles + Trips without product confirmation — the leaderboard's value comes from focus.
- ❌ Don't change the yellow ring colour for 1st place — `Border/Yellow` is the established signal.
- ❌ Don't render an empty leaderboard container — always show the Empty State Pattern.

---

Back to [[Patterns]] · [[Design System]].
