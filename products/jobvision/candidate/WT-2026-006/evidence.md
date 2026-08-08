---
walkthrough_id: WT-2026-006
status: draft
product_group: JobVision
product: Candidate
candidate_areas:
  - Application Management (candidate area TBD)
recorded_at: 2026-08-07
source:
  type: browser-agent
  reference: Direct read-only Production audit of https://jobvision.ir
reviewed_by: []
reviewed_at:
---

# Walkthrough Evidence Package

## Context

- Goal: Inspect how a logged-in jobseeker finds, reviews, filters, and manages previously submitted applications.
- Actor: Jobseeker.
- Role: Logged-in candidate account; exact account entitlements are unknown.
- Authentication state: Logged in.
- Account, plan, or configuration: Existing Production account with historical applications; plan and special permissions were not verified.
- Permissions: Normal visible candidate access was assumed only from the available UI; no permission-changing action was taken.
- Environment: Production.
- Starting point: JobVision home page.
- Safety constraints: Read-only exploration. Do not withdraw an application, edit a sent resume, submit rejection feedback, change priority, send messages, edit profile/resume data, make purchases, or take any action that may affect an employer or another user.

## Coverage

### Covered

- Entry from the home-page account menu to submitted applications.
- Active-application status filters and account-specific count badges.
- Empty-state behavior for a status with no applications.
- Sorting active applications by request date and status-decision date.
- Application summary information and expandable details.
- Read-only inspection of available edit and withdrawal controls.
- Rejected-application feedback prompts without answering them.
- Closed-application grouping and pagination.
- On-page FAQ guidance for status meanings, withdrawal eligibility, review timestamps, closed postings, and rejection feedback.
- Visible "My Priority" explanation and quota model without changing priority.

### Narrated but not demonstrated

- None. No recorder or domain-owner narration was supplied during this browser-agent walkthrough.

### Not covered

- Executing or confirming application withdrawal.
- Editing the resume attached to a submitted application.
- Selecting or removing "My Priority" or adding/editing its introduction letter.
- Submitting rejection-stage or interview feedback.
- Opening or applying to similar jobs from a rejected application.
- Applications in initial evaluation, final evaluation, or withdrawn states because the audited account had no current examples.
- Empty-account behavior, other candidate roles or plans, mobile/responsive behavior, keyboard navigation, and screen-reader behavior.

### Unclear or blocked

- Whether withdrawal has a confirmation step, is reversible, and how quickly list counts and status update.
- Whether editing a sent resume changes a snapshot or the current canonical candidate resume visible to the employer.
- How rejection feedback is persisted and whether it is optional or required.
- How "My Priority" is presented in the employer experience and whether quota rules vary by plan.
- Whether the "All" filter intentionally excludes closed applications in every account/context.

## Evidence

### E-001 — Submitted applications are reachable from the candidate account menu

- Type: observed
- Timestamp: 2026-08-07 19:37:51–19:38:01 +03:30
- Scope: Logged-in candidate on the Production home page.
- Conditions: Desktop web experience; account menu opened from the header.
- Confidence: high
- Claim: The candidate account menu includes a "Submitted resumes" entry that navigates to `/my-applications`, where the page heading identifies the submitted-applications workspace.
- Remaining uncertainty: Other responsive layouts and unauthenticated behavior were not tested.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-002 — The page separates applications by lifecycle-oriented status filters

- Type: observed
- Timestamp: 2026-08-07 19:38:01–19:38:44 +03:30
- Scope: Logged-in candidate with existing active and historical applications.
- Conditions: Counts are specific to the audited account and are intentionally omitted from this claim.
- Confidence: high
- Claim: The page provides filters for All, Received by employer, Initial evaluation, Final evaluation, Rejected, Withdrawn, and Closed postings. Selecting a filter narrows the visible list and encodes the selected status in the page URL.
- Remaining uncertainty: The complete server-side status model and permission-dependent states were not verified.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-003 — Application summaries expose status and timing signals

- Type: observed
- Timestamp: 2026-08-07 19:38:01–19:39:57 +03:30
- Scope: Active, rejected, and closed application cards in the audited account.
- Conditions: Some timing fields were absent on individual cards.
- Confidence: high
- Claim: Each visible application summary identifies the job, employer, current visible status, and relative submission time; when available, it also shows when the employer viewed the application.
- Remaining uncertainty: The exact conditions that suppress the viewed timestamp were not tested.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-004 — Empty status filters explain what would appear there

- Type: observed
- Timestamp: 2026-08-07 19:38:34 +03:30
- Scope: Initial-evaluation filter with no matching applications in the audited account.
- Conditions: Desktop Production page.
- Confidence: high
- Claim: When a status filter has no matching applications, the list is replaced by explanatory copy describing which employer-driven transition would place an application in that section.
- Remaining uncertainty: Empty-state copy for every other status was not inspected.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-005 — Closed applications are separated and paginated

- Type: observed
- Timestamp: 2026-08-07 19:38:44–19:38:54 +03:30
- Scope: Closed-postings filter in an account with multiple pages of historical applications.
- Conditions: Read-only navigation between the first two pages.
- Confidence: high
- Claim: Applications associated with closed job postings appear in a dedicated filter and are paginated; moving to another page updates the page parameter in the URL and loads a different set of historical applications.
- Remaining uncertainty: Page size, final-page behavior, and very large histories were not fully assessed.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-006 — Active applications can be sorted by request date or status-decision date

- Type: observed
- Timestamp: 2026-08-07 19:40:08 +03:30
- Scope: All active applications in the audited account.
- Conditions: Both sort options were available because multiple active applications were present.
- Confidence: high
- Claim: The active-applications list offers sorting by request date and by status-decision date. Changing the selection updates both the result order and the `sortType` URL parameter.
- Remaining uncertainty: Sort direction, tie-breaking, and sort availability in other filters were not verified.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-007 — Expanding an active application reveals management details and actions

- Type: observed
- Timestamp: 2026-08-07 19:39:30–19:39:49 +03:30
- Scope: One active application in the Received-by-employer filter.
- Conditions: The application already contained an introduction letter and had not been withdrawn.
- Confidence: high
- Claim: Expanding an active application can reveal the employer's latest visit to applications for that job, an attached introduction letter when present, and visible controls for editing the sent resume and withdrawing the application.
- Remaining uncertainty: Neither management action was opened or executed; their validations, confirmations, persistence, and downstream effects remain unknown.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-008 — The UI states that withdrawal is limited to unseen applications

- Type: observed
- Timestamp: 2026-08-07 19:40:31 +03:30
- Scope: On-page FAQ guidance in the submitted-applications workspace.
- Conditions: Guidance was read but the rule was not demonstrated through a withdrawal attempt.
- Confidence: medium
- Claim: The FAQ states that a candidate can withdraw a previously submitted application only while the organization has not yet viewed the resume.
- Remaining uncertainty: Enforcement behavior, race conditions, confirmation, and exceptions were not tested.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-009 — Rejected applications ask the candidate for process feedback

- Type: observed
- Timestamp: 2026-08-07 19:39:57 +03:30
- Scope: One rejected application that had been viewed by the employer.
- Conditions: No feedback option was selected or submitted.
- Confidence: high
- Claim: Expanding a rejected application shows when the employer viewed it and asks the candidate to identify the rejection stage (after submission, after a phone interview, or after an in-person interview) and whether an interview occurred.
- Remaining uncertainty: Submission trigger, optionality, persistence, and how this feedback is used were not assessed.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-010 — The page explains core employer-driven status meanings

- Type: observed
- Timestamp: 2026-08-07 19:40:17 +03:30
- Scope: On-page FAQ guidance.
- Conditions: Help content was observed; the transitions were not independently triggered.
- Confidence: medium
- Claim: The FAQ describes Received by employer as the organization having received the resume for initial review, Initial evaluation as further review, Final evaluation as passing the review stage without guaranteeing an interview, Rejected as the employer continuing with another candidate, and Closed as the employer having filled the position and closed the posting.
- Remaining uncertainty: The FAQ does not define the Withdrawn state even though it exists as a page filter.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-011 — Application details distinguish application-view time from employer activity time

- Type: observed
- Timestamp: 2026-08-07 19:40:42 +03:30
- Scope: On-page FAQ guidance and one expanded active application.
- Conditions: Relative times were shown for the audited account.
- Confidence: medium
- Claim: The page distinguishes when the employer viewed a specific candidate application from the employer's latest visit to the job's received-applications panel; both signals are discoverable through expanded application details when available.
- Remaining uncertainty: Refresh cadence and data-source accuracy were not tested.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-012 — Employer rejection feedback is optional and may be absent

- Type: observed
- Timestamp: 2026-08-07 19:41:09 +03:30
- Scope: On-page FAQ guidance.
- Conditions: No employer-provided rejection explanation was visible in the inspected rejected application.
- Confidence: medium
- Claim: The FAQ states that employers can provide a rejection reason or feedback that appears in application details, but an employer may reject an application without providing a reason, leaving that section empty.
- Remaining uncertainty: Feedback formats, moderation, editability, and notification behavior were not assessed.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-013 — "My Priority" is presented as a limited recurring application-enhancement allowance

- Type: observed
- Timestamp: 2026-08-07 19:38:01–19:40:08 +03:30
- Scope: Audited candidate account and page explanation.
- Conditions: At least one existing application was already marked as priority; no priority state was changed.
- Confidence: medium
- Claim: The page explains that candidates can mark selected submitted applications as "My Priority" so the resume is differentiated for the employer and can include an introduction letter. The UI describes a recurring allowance of five priority selections per 30 days and shows account-specific remaining allowance and renewal timing.
- Remaining uncertainty: Plan eligibility, employer-side presentation, removal behavior, and quota enforcement were not tested.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

## Suspected bugs

### B-001 — Status terminology differs between the filter and application card

- Timestamp: 2026-08-07 19:38:01–19:38:26 +03:30
- Scope: The only application returned by the Received-by-employer filter.
- Observation: The filter is labeled "Received by employer," while the matching application card displays a status equivalent to "Status not set."
- Why it may be a bug: The two labels appear to represent the same current application state but communicate different meanings to the candidate.
- Owner note:

### B-002 — The status FAQ omits the Withdrawn status

- Timestamp: 2026-08-07 19:40:17 +03:30
- Scope: Status filters and the first FAQ answer on the same page.
- Observation: Withdrawn is available as a filter, but the FAQ titled "What do the different resume statuses mean?" defines the other principal states and does not define Withdrawn.
- Why it may be a bug: The help content appears incomplete relative to the status taxonomy presented immediately above it.
- Owner note:

### B-003 — Several interactive controls lack standard semantic roles

- Timestamp: 2026-08-07 19:38:01–19:39:49 +03:30
- Scope: Desktop accessibility tree and visible DOM for status filters, card expansion, edit, and withdrawal controls.
- Observation: Status filters were exposed as links without destinations, card expansion as a raw icon, and edit/withdraw actions as clickable containers rather than buttons.
- Why it may be a bug: These implementations may reduce keyboard operability and screen-reader clarity; a dedicated accessibility test is required before confirmation.
- Owner note:

## Coverage gaps

- Safely test withdrawal on a disposable application and pre-approved test posting, including confirmation, cancellation, state update, and reversibility.
- Safely test editing the resume associated with a submitted application and determine snapshot versus live-resume behavior.
- Demonstrate initial-evaluation, final-evaluation, and withdrawn application cards.
- Test "My Priority" selection, introduction-letter validation, removal, quota enforcement, and employer-side visibility with approved test accounts.
- Test rejection-feedback submission and persistence with a disposable application.
- Test empty-account, mobile, keyboard-only, and screen-reader experiences.
- Verify status terminology and FAQ completeness with the Product Owner.

## Recommended follow-up recording

- Use a disposable candidate account and a pre-approved employer test posting to cover withdrawal and resume-edit flows without affecting a real employer.
- Use paired candidate and employer test accounts to demonstrate every status transition, rejection feedback, viewed timestamps, and "My Priority" presentation end to end.
- Run a focused keyboard and screen-reader walkthrough of status filters, card expansion, and management actions.

## Related Product Areas

- Primary: JobVision Candidate / Application Management. This area already exists as an owner-review candidate in `products/jobvision/candidate/overview.md`, although no dedicated Product Area document exists yet.
- Secondary: Job Details & Evaluation, because application history is an entry point back toward Job Post context and that area explicitly delegates detailed post-submission journeys to Application Management.
- Secondary candidate: Resume Management, because the expanded application exposes an action to edit the sent resume; ownership and snapshot-versus-live-resume behavior remain unknown.
- Secondary candidate: Premium Insights, because "My Priority" is presented beside an upgrade path and quota; exact ownership and plan rules remain unknown.
- Shared concept: `shared.application`, which owns cross-product Application meaning and relationships while Candidate-visible tracking and management belong in a Candidate Product Area.

## Suggested Product Knowledge updates

This comparison was performed only after evidence extraction. It is preliminary, based on a draft package, and is not eligible for canonical Product Knowledge changes until Owner review.

### Candidate Application Management Product Area

- Recommendation: After Owner approval, create the dedicated Application Management Product Area already anticipated by the Candidate overview and Job Details & Evaluation document.
- Suggested outcome: Help a Candidate understand the current state and employer activity for each submitted application and safely manage eligible post-submission actions.
- Candidate flows supported by this walkthrough: enter from the account menu, filter by Candidate-visible status, sort, paginate closed history, expand application details, inspect employer-view signals, edit the sent resume, withdraw when eligible, manage "My Priority," and provide post-rejection process feedback.
- Why existing areas are insufficient: Job Details & Evaluation explicitly delegates detailed submission and post-submission journeys; Resume Management would not logically own application lifecycle, employer activity, rejection, or withdrawal; Premium Insights would not own the base tracking experience.
- Supporting evidence: E-001 through E-013.
- Missing information: Owner-approved state model, withdrawal enforcement, resume snapshot behavior, employer synchronization, status-transition triggers, notifications, retention, empty-account behavior, plan variations, and end-to-end test evidence.
- Confidence: high that Application Management is the logical Primary Product Area; medium on the exact boundaries with Resume Management and Premium Insights.
- Team recommendation: Confirm the existing candidate area name and boundary before creating the document; do not create a new UI-page-based Product Area.

### Candidate overview and Job Details & Evaluation

- After the Product Area is approved and created, add its document ID to the Candidate overview relationships and replace the "future Application Management Product Area" wording in Job Details & Evaluation with a direct related-area reference.
- Keep application submission and post-submission management boundaries explicit so the Job Post page does not become the owner of tracking, status, withdrawal, or rejection-feedback behavior.

### Shared Application concept

- After Owner review, use accepted evidence to refine Candidate-visible lifecycle terminology and the relationships between submitted, viewed, evaluated, rejected, withdrawn, and closed-posting representations.
- Preserve the existing unknowns for withdrawal, resume snapshot versus live resume, cross-product status synchronization, retention, and related-Job-Post closure until paired Candidate/Employer evidence or an Owner decision resolves them.
- Treat "Received by employer" versus "Status not set" as a possible terminology mismatch rather than a confirmed shared lifecycle rule.

## Handoff summary

Complete this section only after owner review.

- Package status: draft
- Accepted evidence IDs:
- Edited evidence IDs:
- Rejected evidence IDs:
- Remaining unknowns: See Coverage gaps and the remaining uncertainty on each evidence item.
- Suggested Product Knowledge scope: Pending owner review and post-extraction comparison with current Product Knowledge.

A reviewed package is an approved source for reconciliation. It is not canonical Product Knowledge and must not be copied directly into product documentation without comparison against the current `product-knowledge/main` branch.
