---
status: in-progress
type: screen-spec
figma_node: "792:20481"
figma_file: yhxCSzJrafZbqXGZOCBCKE
---

# Order Files

Dev-ready iPhone screen (393×852) showing the **Files** tab of an order detail view. Lists generated documents and user-uploaded files for a single order. Placed inside the new **Files** section on Page 5 (next to [[Orders List]] in Section 1).

**Figma:** https://www.figma.com/design/yhxCSzJrafZbqXGZOCBCKE/HaulEx-Driver-App?node-id=792-20481

## Structure

| Region | Component | Notes |
|---|---|---|
| Status bar | Status Bar - iPhone (DS instance) | 9:41 |
| Nav bar | Navigation Bar (DS instance) | Back chevron + title "Order 10421" + `ENCL` pill badge |
| Order tab bar | Segment Control (DS instance) | Details / Payment / BOL / **Files** (selected, yellow) |
| Sort control | TEXT + icon | "Sort by ↑↓" — currently static, no menu wired |
| **Generated** section header | Section Header pattern | Plain text label, no trailing action |
| Generated rows | [[File field]] component instances | Contract.pdf · BOL.pdf — file icon + filename |
| **Other Files** section header | Section Header pattern | Plain text label |
| Other Files rows | [[File field]] component instances | 3 image attachments — thumbnail + filename + trailing `...` menu |
| FAB | Button (DS instance, yellow circular) | `+` — entry point for adding a new file |

## Rows

| Section | Filename | Type | Thumbnail | Trailing |
|---|---|---|---|---|
| Generated | Contract.pdf | PDF | file icon | — |
| Generated | BOL.pdf | PDF | file icon | — |
| Other Files | 44786436-AF…….png | image | car rear photo | `...` menu |
| Other Files | 44786436-AF…….png | image | truck front photo | `...` menu |
| Other Files | 44786436-AF…….jpeg | image | truck angle photo | `...` menu |

## Origin

Built by cloning `FIles (Done)` (node `139:13350`) from the DS page's `Files` section (`667:31228`) and adapting:
- Nav title `Order 85384.1` → `Order 10421` (matches first row of [[Orders List]])
- ENCL badge preserved (matches Order 10421 encl flag in [[Orders List]])
- All `SF Pro Text Regular` references rewritten to `SF Pro Regular`

## Token & system compliance

| Property | Token |
|---|---|
| File rows | [[File field]] component — gap `Space/S`, thumbnail `Radius/S` + `Background/Subtle` |
| Section list | Inherits `Space/L` row gap from list pattern |
| Nav Bar / Segment Control / Tab Bar | DS instances — semantic colors only |
| FAB | DS Button instance, yellow accent |

No hardcoded hex values.

## Font workaround

15 text nodes used `SF Pro Text Regular`. Same workaround as [[Orders List]] — clone → walk text nodes → `setRangeFontName` to `SF Pro Regular` → reparent. Resulting screen is a detached frame; nested DS instances still live.

## Follow-ups

- **Empty state**: design "no files yet" state — see [[Empty State Pattern]].
- **Loading state**: `SF Symbols` placeholder rows during fetch — see [[Loading Skeleton Pattern]].
- **Sort menu**: tap "Sort by ↑↓" → action sheet with sort options (date, name, type).
- **Action menu (`...`)**: rename / share / delete sheet — already designed in `Generated (Done)` (`1:30464`), `File Name (Done)` (`122:30409`), `Deleting (Done)` (`122:30736`). Bring those variants into the same Files section when the modal flow is built out.
- **Other tabs**: Details / Payment / BOL tabs not yet built for this order context.
- **FAB action**: confirm whether `+` opens a camera shortcut, file picker, or both — see [[Camera Capture Flow]] for capture branch.

Back to [[Driver App]] · [[Design System]] · [[File field]] · [[Orders List]].
