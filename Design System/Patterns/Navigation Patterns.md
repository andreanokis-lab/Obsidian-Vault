# Navigation Patterns

Guide for choosing the right navigation pattern in the Driver App. iOS has two primary navigation systems — using the wrong one is a HIG violation.

---

## The two primary systems

### Navigation Stack (push/pop)
For **hierarchical** content — user drills down into detail, then comes back.

- Implemented with `UINavigationController`
- Left-to-right push, right-to-left pop
- Back button always in top-left, inherits previous screen title
- Use when: List → Detail, Settings → Sub-settings, Load → Load Detail

### Tab Bar (peer navigation)
For **peer-level** top sections — user switches between unrelated areas at the same hierarchy level.

- Implemented with `UITabBarController`
- 3–5 tabs maximum (HIG hard limit)
- Each tab: icon + label (reduces navigation errors by 34%)
- Use when: Home / Loads / Messages / Profile — top-level sections

---

## Navigation Bar rules

| Property | Rule |
|---|---|
| Height | 44pt (+ safe area top) |
| Title style | `Screen/Title` — 17pt Semibold |
| Title length | 1–3 words maximum |
| Back button | Always present when not at root; inherits previous screen name |
| Leading action | Back button only (do not add a second leading action) |
| Trailing action | Max 1–2 icon buttons; use SF Symbols |
| Background | Follows `Background/Primary` in Light, `Background/Primary` in Dark |

### Token spec

| Element | Token |
|---|---|
| Title label | `Text/Primary` + `Screen/Title` text style |
| Back chevron icon | `Icon/Primary` |
| Action icon (default) | `Icon/Primary` |
| Action icon (tinted/active) | `Icon/Blue` |
| Bar background | `Background/Primary` |
| Bottom separator | `Border/Subtle` at `Width/XS` |

---

## Tab Bar rules

| Property | Rule |
|---|---|
| Position | Bottom of screen, above home indicator safe area |
| Tab count | 3–5 (never fewer than 3, never more than 5) |
| Tab content | Icon + label (both required — label reduces errors) |
| Active tab | `Icon/Blue` + `Text/Link` |
| Inactive tab | `Icon/Subtle` + `Text/Tertiary` |
| Badge | Use `NotificationBadge` component for unread counts |

---

## Modal vs Push — decision guide

| Situation | Use |
|---|---|
| Drilling into a record (load, company, trip detail) | **Push** (navigation stack) |
| Switching top-level app section | **Tab Bar** |
| Completing a task without losing context of current screen | **Half Sheet** (see [[Sheet Pattern]]) |
| Entering a focused multi-step flow | **Full Sheet** (see [[Sheet Pattern]]) |
| Showing settings that belong to the current screen | **Push** |
| Confirming a destructive action | **Stack Button Sheet** (see [[Sheet Pattern]]) |

---

## Maximum depth rule

> No more than **2 taps** to reach any core feature from the tab bar.

If you find yourself designing a 3rd or 4th level of drill-down, the information architecture needs to be restructured, not the navigation pattern.

---

## Do / Don't

✅ Back button always shows the name of the previous screen (not generic "Back")
✅ Navigation title is always centered on the screen
✅ Tab icons are SF Symbols — they scale with accessibility settings
❌ Don't add navigation bars inside a half sheet — use the handle drag to dismiss
❌ Don't put more than 5 tabs in the tab bar — collapse extras into "More"
❌ Don't use push navigation for peer-level sections (tabs exist for this)
❌ Don't hide the tab bar when pushing into detail views (it should remain visible)

---

Back to [[Design System]] · [[Patterns]] · [[Getting Started]].
