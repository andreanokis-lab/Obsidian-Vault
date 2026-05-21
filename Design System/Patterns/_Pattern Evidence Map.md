# Pattern Evidence Map

Reference: Driver App (`yhxCSzJrafZbqXGZOCBCKE`) → `DS` page. Every pattern doc cites real screens from this map.

---

## Form Pattern

| Screen | Section | Notes |
|---|---|---|
| Log In (Done) | Login `1:29600` | Email + password form |
| Log in via Phone Number (Done) | Login `1:29600` | Phone-number entry |
| Carrier Sign-up (Done) | Login `1:29600` | Multi-field registration form |
| Forgot Password Stage 1 / 2 / 3 (Done) | Login `1:29600` | Multi-step password recovery |
| Password (Done) | Change Pass `667:31702` | Current + new + confirm |
| Not Match (Done) | Change Pass `667:31702` | Form with `State=Negative` validation |
| Profile Settings (Done) | Profile `667:31697` | Editable profile fields |
| New Note (Done) | Notes `667:31700` | Text Area form |
| Driver Notes (Done) | Driver Notes `737:21942` | Text Area inside trip flow |
| Add Truck Services (Done) | Truck Service `662:30875` | Form with multiple fields |
| Receipts Add COP/COD (Done) | Receipts `662:30759` | Amount + type form |
| Add Driver Notes (Done) | Order Details `667:31707` | Text Area in sheet |
| ETA (Done) | Order Details `667:31707` | Date/time picker form |
| Customer Template (Done) | Order Details `667:31707` | Pick from list + edit |

---

## List with Actions Pattern

| Screen | Section | Notes |
|---|---|---|
| Sibebar menu (Done) | Sidebar `662:30757` | Navigation list with chevrons |
| Settings (Done) | Settings `667:31696` | Toggles, Pickers, Trailing-Icon |
| Notifications List (Done) | Notifications `662:30691` | Trailing-Icon rows |
| Receipts list (Done) | Receipts `662:30759` | Content Row variant with Receipts data |
| Truck Service (Done) | Truck Service `662:30875` | Content Row variant for services |
| FIles (Done) | Files `667:31228` | File rows with Trailing-Icon |
| File (Done) | My Files `667:31699` | Generic list |
| Notes List (Done) | Notes `667:31700` | Notes rows with chevron |
| Request List (Done) | Requests `667:31704` | Status + chevron rows |
| Safety List (Done) | Safety `667:31706` | Unit list |
| Trip List (Done) | Trips `1:28891` | Trip rows |
| Completed (Done) | Trips `1:28891` | Completed trip rows |
| Archived (Done) | Trips `1:28891` | Archived trip rows |
| Trip Order List Pickup / Delivery / Completed (Done) | Trips `1:28891` | Lists with Content Row Stops variant |
| Routes List (Done) | Routes `1:29825` | Route rows |
| List of stops (Done) | Routes `1:29825` | Stop rows with Vertical Badge |

---

## Empty State Pattern

### Default empty (no data yet)

| Screen | Section | Notes |
|---|---|---|
| Empty State | Top-level `1:28742` | Standalone empty state reference |
| Notifications Placeholder (Done) | Notifications `662:30691` | No notifications |
| Notes Placeholder (Done) | Notes `667:31700` | No notes yet |
| Leaderboard Placeholder (Done) | Leaderboard `667:31703` | No leaderboard data |
| Request Placeholder (Done) | Requests `667:31704` | No requests |
| Company Placeholder (Done) | Company `667:31705` | No companies |
| Add Truck + Placeholder (Done) | Safety `667:31706` | No trucks added |
| Nothing Here (Done) ×2 | Truck Service `662:30875` | No services / empty filtered list |

### No results (after search / filter)

| Screen | Section | Notes |
|---|---|---|
| No Contact Found (Done) | Company `667:31705` | Search returned no results — Filter Search Results sub-case |

---

## Error State Pattern

| Screen | Section | Notes |
|---|---|---|
| Alert | Top-level `1:28890` | Generic alert overlay |
| Alert (Done) | Scan VIN `736:40323` | Scan failure alert |
| VIN Doesn't Match | ORDERS `1:30405` / Scan VIN `736:40323` | Validation error |
| Something Wrong w/ VIN (Done) | Scan VIN `736:40323` | Server error / unknown failure |
| Remove Alert (Done) | Truck Service `662:30875` | Destructive confirm |
| Long Press (Deleting) (Done) | Truck Service `662:30875` | Destructive action sheet |
| Deleting Reciept (Done) | Receipts `662:30759` | Destructive confirm |
| Deleting Image (Long Press) (Done) | Receipts `662:30759` | Destructive action sheet |
| Deleting (Done) | Files `667:31228` | Destructive confirm |
| Deleting Acc (Done) | Settings `667:31696` | Destructive account deletion |

---

## Loading Skeleton Pattern

| Screen | Section | Notes |
|---|---|---|
| Titles `Place=Skeleton` | Leaderboard `667:31703` | Skeleton variant of the Titles molecule (documented in [[Components/Titles]]) |

Most lists rely on the Skeleton variant of Titles or implicit shimmer. No dedicated skeleton screens found beyond Leaderboard.

---

## Section Header Pattern

Used inside most list screens — Settings groups, Notes sections, etc. Not a standalone screen pattern; appears as a sub-pattern within others.

---

## Camera Capture Flow

| Screen | Section | Notes |
|---|---|---|
| Take a Photo (Done) | Receipts `662:30759` | Receipt capture |
| Аdd Photo Receipts (Done) | Receipts `662:30759` / Adjustments `737:21382` | Multi-photo capture |
| Camera (Done) | Truck Service `662:30875` | Service photo capture |
| Multiple Photos (Done) | Truck Service `662:30875` | Multi-frame capture |
| Add Photo (Done) | Adjustments `737:21382` | Adjustments photo flow |
| Сhoose from Library (Done) | Adjustments `737:21382` | Library picker (not camera) |
| Picture (Done) | Profile `667:31697` | Avatar photo capture |
| Scan VIN (Done) | Scan VIN `736:40323` | VIN-barcode capture |
| Scan VIN + Input (Done) | Scan VIN `736:40323` | Manual fallback after scan failure |

---

## Take Photo Screen Pattern

Specific composition of Camera atoms + molecules into a full capture screen. Lives on the UIKit `----- Camera` page (`1182:544`) and instantiated in:

- Take a photo section `737:20442` (in DS — empty section, references the UIKit composition)
- Take a Photo (Done) — Receipts
- Add Photo (Done) — Adjustments
- Multiple Photos (Done) — Truck Service

---

## Leaderboard Pattern

| Screen | Section | Notes |
|---|---|---|
| Leaderboard (Done) | Leaderboard `667:31703` | Podium (3 [[Components/Places Segments]]) + Leaderboard Row list for 4+ |
| One (Done) | Leaderboard `667:31703` | Single-driver state |
| Placeholder (Done) | Leaderboard `667:31703` | Skeleton + empty state |

---

## Sheet Pattern

| Screen | Section | Notes |
|---|---|---|
| Sheet (Done) | Truck Service `662:30875` | Half sheet for adding |
| Photo Actions (Done) | Truck Service `662:30875` | Action sheet style |
| Dropdown (Done) | Profile `667:31697` | Sheet-based dropdown |
| Picture (Done) | Profile `667:31697` | Photo source sheet |
| Select (Done) | Order Details `667:31707` | Picker sheet |
| Add Driver Notes (Done) | Order Details `667:31707` | Half sheet with Text Area |
| Receipts Add COP/COD (Done) | Receipts `662:30759` | Sheet form |
| Аdd Photo Receipts (Done) | Receipts `662:30759` | Camera sheet |
| Customer Template (Done) | Order Details `667:31707` | Template-picker sheet |

---

## Filter / Search Results (Empty)

| Screen | Section | Notes |
|---|---|---|
| No Contact Found (Done) | Company `667:31705` | Search returned empty — the canonical screen for this pattern |
| Company File List (Done) | Company `667:31705` | Populated state for contrast |

---

## Source

Audit date: 2026-05-21. Driver App file: `yhxCSzJrafZbqXGZOCBCKE` → DS page (71 top-level children, ~40 SECTION groups containing screens).

Back to [[Patterns]] · [[Design System]].
