---
status: open
type: design-sprint-checklist
figma_node: "1:40837"
figma_file: yhxCSzJrafZbqXGZOCBCKE
reviewed_against: Apple HIG (iOS) + DS2
---

# Company Filter Not Found — Sprint Checklist

Design sprint checklist for the HaulEx Driver App empty-state screen "company filter not found" (Figma node `1:40837`). Issues identified by HIG audit; tasks grouped by priority.

**Figma:** https://www.figma.com/design/yhxCSzJrafZbqXGZOCBCKE/HaulEx-Driver-App?node-id=1-40837

## P0 — Must Fix (HIG violations)

- [ ] **Fix tab strip overflow** — Accounting / Dispatcher / Claims / Mechanic row is full-bleed (`x=0, w=393`); "Mechanic" is clipped. Apply 16pt (`Space/L`) horizontal margin; make horizontally scrollable, shorten labels, or collapse into dropdown. Verify on 375pt screens.
- [ ] **Make "Clear Filters" a real button** — currently plain `Text/Primary` body. Restyle as `Text/Link` (systemBlue) or Secondary button. Pad hit area to **44×44pt minimum**. Add VoiceOver label "Clear filters".
- [ ] **Replace empty-state glyph with proper SF Symbol** — text node `􀉬` should be an SF Symbol image node (`person.2.fill`) with `Icon/Subtle` color, scaling with Dynamic Type.
- [ ] **Fix search field clear icon** — instance is named `eye-solid 1`; replace with `xmark.circle.fill`. Confirm tap clears input.

## P1 — Layout & Alignment

- [ ] Align "Filters" label to 16pt margin (currently `x=15`)
- [ ] Center "Company" title against the **screen** (393pt), not the 224pt header container
- [ ] Add back-button label ("‹ Back" or inherited previous screen title) instead of bare chevron
- [ ] Audit all interactive elements for **44×44pt** hit areas (filter button ✓, segmented ✓; verify tabs and clear-filters action)

## P2 — Information Architecture

- [ ] Resolve redundant navigation layers — keep segmented control (Contacts/Files) **OR** category tabs (Accounting/Dispatcher/Claims/Mechanic). If both, justify hierarchy.
- [ ] Re-rank empty-state typography:
  - "No Contact Found" → Headline (17pt Semibold, `Text/Primary`)
  - Supporting hint → Body or Subheadline (`Text/Secondary`)
  - "Clear Filters" → Link/Button styling
- [ ] Add a search-with-results state so empty state isn't the only feedback after typing

## P3 — Token & System Compliance

- [ ] All spacing values use DS2 tokens (`Space/XS`–`Space/2XL`) — no arbitrary px (see [[Spacing]])
- [ ] All colors use semantic tokens (`Text/*`, `Background/*`, `Border/*`) — no raw hex (see [[Colors - Semantic]])
- [ ] All radii use `Radius/*` tokens (see [[Border]])
- [ ] Typography uses DS2 IOS semantic styles — no custom sizes (see [[Typography - Semantic]])

## P4 — Cross-Mode & Accessibility QA

- [ ] Reviewed in **Light mode** — re-check contrast and surfaces
- [ ] Reviewed in **Dark mode** — current mode, validate token mapping
- [ ] Dynamic Type tested at **XS, L (default), XXL, AX1** — confirm reflow, no truncation, no clipping
- [ ] Contrast: all text ≥ **4.5:1**, large text ≥ 3:1
- [ ] VoiceOver labels for: back button, filter button, segmented options, tabs, clear-filters action, empty-state icon
- [ ] Reduce Motion tested
- [ ] RTL layout sanity check

## P5 — Variants to Produce

- [ ] Default empty (no search query yet)
- [ ] No results for active search + filters (current screen)
- [ ] Loading state
- [ ] Error / offline state
- [ ] Populated list state (for context)

## Definition of Done

Every P0 + P1 item closed, screen tested in Light/Dark + 4 Dynamic Type sizes, all tokens semantic, and a populated-list counterpart exists.

---

Back to [[Driver App]].
