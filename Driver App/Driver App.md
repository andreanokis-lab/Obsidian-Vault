# Driver App

Hub note for the HaulEx Driver App (iOS). Screen specs, flows, components, and design-review checklists live here. Cross-references the [[Design System]] for tokens.

**Figma file:** `yhxCSzJrafZbqXGZOCBCKE`

## Screens & Reviews

- [[Take Photo Screen]] — camera screen DS rebuild (Figma node `1:31606`, DS rebuild `626:20818`) — token violations fixed, 3 component swaps pending
- [[Company Filter Not Found - Sprint Checklist]] — empty-state screen audit against Apple HIG + DS2 (Figma node `1:40837`)
- [[Orders List]] — dev-ready Orders screen (393×852) in Section 1 on Page 5 (Figma node `782:20481`, parent section `762:20797`); built by cloning + font-rewriting Trip Order List Delivery (Done) (`1:29438`)
- [[Order Files]] — dev-ready Files tab for Order 10421 (393×852) in the new Files section on Page 5 (Figma node `792:20481`, parent section `790:761`); built by cloning + font-rewriting FIles (Done) (`139:13350`)
- [[Salary Request Flow]] — 3-screen new-flow (List → Form → Confirmation) for driver salary/reimbursement/loan requests, in the Salary Requests section on Page 5 (`796:926`); screens `798:20481`, `804:20481`, `807:20481`
- [[Breakdown Alert Flow]] — 3-screen emergency flow (Issue Picker → Details Sheet → Alert Sent + Timeline) for drivers to alert dispatch about on-road problems, in the Breakdown Alerts section on Page 5 (`817:1465`); screens `818:1465`, `821:1584`, `823:1776`
- [[Vehicle Details Screen]] — full inspection + vehicle data screen built 2026-06-25, updated 2026-06-26; wrapper `1035:20512` on page `1:2` ("DS"); stacked sections (Action Section header, Upload Summary, Vehicle Data card, Pickup + Delivery Inspection with BOL outline + Damage-Markers, Download CTA + Toast); split-order C/E labels (#XXXXX.N), plain Additional Info rows, photo tiles clean (long-press for upload state)

## Related

- [[Design System]] — DS2 tokens, typography, colors
- [[Spacing]] · [[Colors - Semantic]] · [[Typography - Semantic]] · [[Border]]
