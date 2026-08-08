---
walkthrough_id: WT-2026-004
status: draft
product_group: JobVision
product: Candidate
candidate_areas:
  - Job Search
  - Recommended Jobs & Preferences (candidate area TBD)
recorded_at: 2026-08-07
source:
  type: direct-browser-audit
  reference: Production browser-agent session in the Codex in-app browser
reviewed_by: []
reviewed_at:
---

# Walkthrough Evidence Package

## Context

- Goal: Capture the current logged-in Candidate experience for recommended jobs and the visible preference-management boundary.
- Actor: Jobseeker
- Role: Candidate
- Authentication state: Logged in
- Account, plan, or configuration: Existing Production Candidate account; plan and broader account configuration were not assessed.
- Permissions: Read-only browser exploration. No account, preference, notification, saved-job, resume, or application changes were authorized.
- Environment: Production, desktop Codex in-app browser
- Starting point: JobVision home page
- Safety boundary: Stop before saving or changing preferences, toggling notifications, saving a job, applying, uploading or downloading, purchasing, messaging, or any action that persists data or affects another user.

## Coverage

### Covered

- Logged-in home-page entry points and personalization cues for recommended jobs
- Dedicated Recommended Jobs page and its two visible recommendation modes
- Visible job-list card information and available actions
- Sorting in the interest-related recommendation mode
- Pagination in the higher-employment-probability mode
- Read-only preference summary and the edit entry boundary
- Visible notification-related controls and messaging, without changing their state

### Narrated but not demonstrated

- None. The audit used direct observation only.

### Not covered

- Saving preference changes
- Dismissing or completing the preference onboarding guide
- Notification activation, deactivation, delivery, or persistence
- Saving or removing a saved job
- Opening a Job Post in detail
- Applying or submitting a resume
- Recommendation behavior for other accounts, roles, authentication states, plans, or empty-data states
- Mobile, responsive, keyboard-only, and assistive-technology behavior
- Backend ranking logic, model inputs, refresh cadence, and recommendation persistence

### Unclear or blocked

- The exact relationship among explicit preferences, observed behavior/performance, and the two recommendation modes
- Whether the preference onboarding guide is account-persistent or session-only
- Whether edit controls can be reached without acknowledging the guide
- The relationship between the settings-level notification control and the inline activation prompt
- Validation, cancellation, and unsaved-change behavior inside the preference editor

## Evidence

### E-001 — Home page exposes personalized recommendation entry points

- Type: observed
- Timestamp: 2026-08-07T17:52:52.981Z
- Scope: Logged-in Candidate on the Production home page
- Conditions: Existing Candidate account with personalized content available
- Confidence: high
- Claim: The logged-in home page exposes a primary navigation entry for recommended jobs and a personalized job module. The module labels its content as being for the Candidate and presents several personalization cues, including interests, employment likelihood, work arrangement, proximity, and AI-based behavior/performance.
- Remaining uncertainty: The ranking logic and exact meaning or eligibility of each cue were not visible.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-002 — Recommended Jobs provides two distinct recommendation modes

- Type: observed
- Timestamp: 2026-08-07T17:52:56.145Z; 2026-08-07T17:53:37.639Z
- Scope: Logged-in Candidate on the Production Recommended Jobs experience
- Conditions: Entered from the home-page navigation
- Confidence: high
- Claim: The Recommended Jobs experience separates recommendations into an interest-related mode and a higher-employment-probability mode. Each mode displays its own opportunity count and a different explanatory basis for the list.
- Remaining uncertainty: The rules for including, excluding, or ordering opportunities in either mode were not visible.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-003 — Recommended job cards support evaluation and account-affecting actions

- Type: observed
- Timestamp: 2026-08-07T17:52:56.145Z; 2026-08-07T17:53:37.639Z
- Scope: Visible cards in both recommendation modes
- Conditions: Logged-in Candidate, Production
- Confidence: high
- Claim: Recommendation cards expose job and employer context such as title, organization, location, recency, and conditional metadata including salary, work arrangement, urgency, employer responsiveness, or active resume review. Each card also exposes controls to save the job and begin resume submission.
- Remaining uncertainty: Save persistence, duplicate actions, application eligibility, and the destination flow were not exercised because they can change account or employer-facing state.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-004 — Interest-related recommendations support three sorting modes

- Type: observed
- Timestamp: 2026-08-07T17:54:14.580Z–2026-08-07T17:54:28.215Z
- Scope: Interest-related Recommended Jobs list
- Conditions: Logged-in Candidate, Production
- Confidence: high
- Claim: The interest-related recommendation list supports sorting by newest, most relevant, and highest salary. Changing the selection updates the page query state, and the audit restored the default most-relevant selection before leaving.
- Remaining uncertainty: Tie-breaking, jobs without salary data, and whether the choice persists across sessions were not tested.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-005 — Recommendation results are paginated

- Type: observed
- Timestamp: 2026-08-07T17:53:57.924Z
- Scope: Higher-employment-probability recommendation list
- Conditions: Logged-in Candidate with more than one result page
- Confidence: high
- Claim: The recommendation list exposes numbered pagination and a final-page control. Selecting page 2 updates the URL with page and sort query parameters and loads a different set of job cards.
- Remaining uncertainty: Last-page behavior, back/forward restoration, and pagination behavior after data changes were not tested.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-006 — Preference summary groups the inputs that shape recommendations

- Type: observed
- Timestamp: 2026-08-07T17:52:56.145Z
- Scope: Preference summary on the Recommended Jobs page
- Conditions: Existing Candidate preferences were present; personal selections are intentionally omitted from this package.
- Confidence: high
- Claim: The page presents a read-only recommendation-preference summary grouped by preferred provinces, preferred job fields, desired employment types, and remote-versus-onsite willingness, with an edit entry point.
- Remaining uncertainty: Required fields, selection limits, dependencies among fields, and how each preference affects recommendations were not visible.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-007 — Preference editing is preceded by contextual onboarding in this account state

- Type: observed
- Timestamp: 2026-08-07T17:53:07.639Z–2026-08-07T17:53:08.404Z
- Scope: Preference edit entry point on the Recommended Jobs page
- Conditions: Existing logged-in Candidate account; onboarding state not previously established
- Confidence: medium
- Claim: Activating the visible preference edit entry point first displayed contextual guidance explaining that preferences are used for personalized job suggestions, with an acknowledgement action, rather than immediately exposing the editor.
- Remaining uncertainty: The audit did not acknowledge the guide because doing so might persist account or session state; the editor, cancellation path, and save validation therefore remain untested.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-008 — Notification-related controls are colocated with recommendations and preferences

- Type: observed
- Timestamp: 2026-08-07T17:52:56.145Z
- Scope: Recommended Jobs list and preference-summary region
- Conditions: Logged-in Candidate, Production
- Confidence: high
- Claim: The page exposes notification-related messaging in two places: an inline prompt offering preferred-job updates by email or SMS, and a settings-level control for receiving recommended-job email and SMS updates.
- Remaining uncertainty: The relationship between the two controls, channel granularity, current delivery state, consent behavior, and persistence were not tested or recorded.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

## Suspected bugs

- None recorded. The onboarding and notification-control relationships remain unknown rather than being classified as defects without Owner confirmation.

## Coverage gaps

- Preference editor fields, validations, cancel behavior, and save outcome require a disposable account or explicit authorization for a controlled state change.
- Notification activation/deactivation and delivery require a safe test account and approved channels.
- Saved-job and application actions require separate bounded walkthroughs because they persist account state or can affect employers.
- Recommendation empty states, refresh behavior, ranking explanations, and account/plan variations remain untested.
- Mobile, responsive, keyboard, and accessibility coverage remain untested.

## Recommended follow-up recording

- Use a disposable Production-safe or equivalent test account to acknowledge the preference guide, inspect the complete editor, exercise validation and cancellation, and verify recommendation updates without exposing personal values.
- Separately test notification opt-in/out and channel behavior with pre-approved test contact points.
- Capture mobile and keyboard-only variants after the desktop preference-edit flow is understood.

## Handoff summary

Complete this section only after owner review.

- Package status: draft
- Accepted evidence IDs: none
- Edited evidence IDs: none
- Rejected evidence IDs: none
- Remaining unknowns: Preference-edit behavior, notification semantics, ranking logic, persistence, empty states, account/plan variations, and accessibility
- Suggested Product Knowledge scope: Candidate Job Search and a possible Recommended Jobs & Preferences area, subject to Product Owner confirmation

A reviewed package is an approved source for reconciliation. It is not canonical Product Knowledge and must not be copied directly into product documentation without comparison against the current `product-knowledge/main` branch.
