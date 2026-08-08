---
walkthrough_id: WT-2026-005
status: draft
product_group: JobVision
product: Candidate
candidate_areas:
  - Job Details & Evaluation
recorded_at: 2026-08-08T05:26:45Z
source:
  type: browser-audit
  reference: "Read-only Production audit on jobvision.ir; no screenshots retained"
reviewed_by: []
reviewed_at:
---

# Walkthrough Evidence Package

## Context

- Goal: Inspect the logged-in Saved Jobs flow from the home page, including entry points, visible states, navigation outcomes, and safe save/remove boundaries.
- Actor: Jobseeker
- Role: Authenticated Candidate
- Authentication state: Logged in
- Account, plan, or configuration: Existing Production account; the Saved Jobs collection was initially empty. One current Job Post was then saved after explicit user authorization. Plan was not verified.
- Permissions: Normal visible Candidate access; no elevated permissions were tested.
- Environment: Production, desktop in-app browser
- Starting point: JobVision home page

## Coverage

### Covered

- The home-page account menu entry for Saved Jobs and its distinction from Saved Searches
- Navigation from the home page to the authenticated Saved Jobs route
- The Saved Jobs placement within the Candidate activity navigation
- The current account's empty state and its visible guidance
- Read-only inspection of bookmark-style save entry points on a job card and a current job detail
- An explicitly authorized save action on one current Job Post, including the control-state transition
- The resulting transition from the empty Saved Jobs state to a one-item list containing the saved Job Post
- Accessibility signals exposed by the save controls

### Narrated but not demonstrated

- None.

### Not covered

- Saved Jobs ordering, pagination, filtering, or sorting beyond the observed one-item list
- Opening a Job Post by activating its link from the Saved Jobs list
- Removing a saved Job Post
- Persistence across reload, sign-out/sign-in, browser sessions, or devices
- Repeated save/remove behavior
- Closed, expired, deleted, or otherwise unavailable saved Job Posts
- Network failure, loading failure, retry, or recovery behavior
- Unauthenticated access and return-after-login behavior
- Mobile, responsive, keyboard-only, and assistive-technology execution
- Account or plan variations

### Unclear or blocked

- The account began with no saved Job Posts; only the resulting one-item state was observed after the user explicitly authorized one save action.
- Removal remained prohibited because the user authorized saving one job, not removing it.
- No visible toast or status message was detected after saving; whether feedback exists in other contexts remains unknown.
- Exact removal confirmation, recovery, and longer-term persistence behavior remain unknown.

## Evidence

### E-001 — Saved Jobs has a dedicated account-menu entry

- Type: observed
- Timestamp: 2026-08-08T05:26:45Z
- Scope: Logged-in Candidate on the Production home page
- Conditions: Account menu opened; no account state changed
- Confidence: high
- Claim: The account menu exposes “مشاغل نشان‌ شده” as a dedicated link to `/saved-jobs`.
- Remaining uncertainty: Other entry points and role/account variations were not tested.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-002 — Saved Jobs is separate from Saved Searches

- Type: observed
- Timestamp: 2026-08-08T05:26:45Z
- Scope: Logged-in Candidate account menu in Production
- Conditions: Account menu opened from the home page
- Confidence: high
- Claim: The account menu presents “مشاغل نشان‌ شده” (`/saved-jobs`) and “جستجوهای ذخیره شده” (`/saved-searches`) as separate destinations.
- Remaining uncertainty: The relationship between these destinations beyond their separate links was not tested.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-003 — Saved Jobs belongs to the Candidate activity navigation

- Type: observed
- Timestamp: 2026-08-08T05:26:57Z–2026-08-08T05:27:16Z
- Scope: Logged-in Candidate on `/saved-jobs` in Production
- Conditions: Navigation started from the home-page account menu
- Confidence: high
- Claim: The Saved Jobs page appears in a Candidate activity navigation alongside submitted resumes, recommended jobs, and followed companies; “مشاغل نشان شده” is visually selected on the Saved Jobs route.
- Remaining uncertainty: Navigation behavior from the other destinations was not exercised.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-004 — Empty Saved Jobs state explains the collection and save entry point

- Type: observed
- Timestamp: 2026-08-08T05:26:57Z–2026-08-08T05:27:16Z
- Scope: Existing logged-in Candidate account with no saved Job Posts
- Conditions: `/saved-jobs` finished loading in Production
- Confidence: high
- Claim: When the collection is empty, the page states that saved jobs will appear in this section and instructs the Candidate to use the icon at the top of a Job Post to save it.
- Remaining uncertainty: Whether the empty state includes a separate call to action in other viewports or account configurations was not tested.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-005 — Current job surfaces expose bookmark-style save entry points

- Type: observed
- Timestamp: 2026-08-08T05:27:28Z–2026-08-08T05:29:02Z
- Scope: Logged-in Candidate viewing current Job Post surfaces in Production
- Conditions: A home-page job card and one current Job Post detail were inspected; no control was activated
- Confidence: high
- Claim: Job cards expose an outline bookmark icon control, and the inspected current Job Post detail also exposes an outline bookmark-style control for the primary Job Post.
- Remaining uncertainty: Removal behavior, duplicate action behavior, longer-term persistence, and feedback in other contexts remain untested.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-006 — Global job-search controls remain available on Saved Jobs

- Type: observed
- Timestamp: 2026-08-08T05:26:57Z–2026-08-08T05:27:16Z
- Scope: Logged-in Candidate on the Production Saved Jobs page
- Conditions: Empty Saved Jobs collection
- Confidence: high
- Claim: The Saved Jobs page retains global job-search inputs for job title or company, job category, and city, plus a search action above the Candidate activity navigation.
- Remaining uncertainty: Search submission and return behavior relative to Saved Jobs were not tested.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-007 — Saving a current Job Post changes the bookmark state

- Type: observed
- Timestamp: 2026-08-08T05:34:36Z
- Scope: Logged-in Candidate on one current Job Post detail in Production
- Conditions: The user explicitly authorized saving one job; no application or other account action was performed
- Confidence: high
- Claim: Activating the Job Post save control changed its icon from an outline secondary bookmark to a filled primary bookmark.
- Remaining uncertainty: No visible toast or status message was detected; reload and cross-session persistence were not tested.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-008 — A newly saved Job Post appears in Saved Jobs

- Type: observed
- Timestamp: 2026-08-08T05:34:57Z
- Scope: Same logged-in Candidate account on `/saved-jobs` in Production
- Conditions: One current Job Post had just been saved with explicit user authorization
- Confidence: high
- Claim: After the save action, the empty-state message was no longer visible and the Saved Jobs page contained a single Job Post link matching the saved Job Post; its card showed a filled primary bookmark icon.
- Remaining uncertainty: Ordering, pagination, filters, opening the item by click, removal, and longer-term persistence were not verified.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

## Suspected bugs

### B-001 — Empty-state copy names a heart while visible save controls use a bookmark icon

- Timestamp: 2026-08-08T05:26:57Z–2026-08-08T05:29:02Z
- Scope: Logged-in Candidate, empty Saved Jobs page plus inspected current Job Post surfaces in Production
- Observation: The empty state instructs the user to click a heart icon, while inspected save controls use outline bookmark icons.
- Why it may be a bug: The instruction and visible iconography do not match, which may make the save action harder to recognize.
- Owner note: Intended terminology and icon choice require confirmation.

### B-002 — Save controls lack an accessible name

- Timestamp: 2026-08-08T05:27:28Z–2026-08-08T05:29:02Z
- Scope: Logged-in Candidate, inspected home-page job card and current Job Post detail in Production
- Observation: The job-card bookmark control is a button with no visible text, `aria-label`, or `title`. The primary Job Post bookmark control is an icon inside a clickable `div` without a semantic role, accessible name, or keyboard tabindex.
- Why it may be a bug: Screen-reader and keyboard users may be unable to identify or operate the save action reliably.
- Owner note: Confirm expected accessibility behavior and supported assistive-technology baseline.

## Coverage gaps

- Saved-list navigation by activating the item link
- Remove state transition and longer-term persistence
- Closed, expired, deleted, and unavailable saved Job Posts
- Feedback and recovery on failed save/remove requests
- Unauthenticated access and login return
- Responsive, mobile, keyboard, and assistive-technology behavior
- Account and plan variations

## Recommended follow-up recording

- Use a disposable Production-safe or staging account with an active saved Job Post and a closed or unavailable saved Job Post.
- Explicitly authorize removal actions in that disposable account so removal feedback, recovery, and persistence can be verified.
- Repeat the flow with keyboard-only navigation and a mobile viewport.

## Handoff summary

Complete this section only after owner review.

- Package status: draft
- Accepted evidence IDs:
- Edited evidence IDs:
- Rejected evidence IDs:
- Remaining unknowns:
- Suggested Product Knowledge scope:

A reviewed package is an approved source for reconciliation. It is not canonical Product Knowledge and must not be copied directly into product documentation without comparison against the current `product-knowledge/main` branch.
