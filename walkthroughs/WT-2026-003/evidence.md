---
walkthrough_id: WT-2026-003
status: draft
product_group: JobVision
product: Candidate
candidate_areas:
  - Resume Management (candidate area)
recorded_at: 2026-08-07
source:
  type: browser-agent
  reference: Direct read-only audit of Production in the Codex in-app browser
reviewed_by: []
reviewed_at:
---

# Walkthrough Evidence Package

## Context

- Goal: Inspect logged-in Resume Management entry points, visible resume states, employer preview, and validation boundaries without saving changes.
- Actor: Jobseeker
- Role: Candidate
- Authentication state: Logged in
- Account, plan, or configuration: Existing Production account with a completed resume; subscription plan and feature entitlements were not verified.
- Permissions: Candidate account permissions as observed; no cross-account or employer permission was tested.
- Environment: Production (`https://jobvision.ir`)
- Starting point: Home page
- Browser context: Codex in-app browser, approximately 1003 × 1023 CSS pixels.
- Safety boundary: Read-only exploration. No save, delete, upload, application submission, purchase, privacy change, new AI evaluation, or download was completed.
- Privacy: Personal resume values were visible during the audit but are intentionally omitted from this package.

## Coverage

### Covered

- Logged-in Home-page state and the Resume Management route exposed by the header (`/my-cv`).
- Existing completed-resume state and its section navigation.
- Overall and per-section completion indicators.
- Candidate/self view versus employer preview.
- Visibility of add, edit, and delete controls without invoking a mutation.
- Opening the About Me form and inspecting visible fields and the pre-save boundary.
- Opening an existing AI resume-evaluation result without starting a new evaluation.
- Visibility of the resume-download control without initiating a download.

### Narrated but not demonstrated

- None. No recorder narration was supplied during this browser-agent walkthrough.

### Not covered

- Saving, deleting, or changing resume data.
- Uploading a personal resume, portfolio, audio introduction, or other file.
- Downloading the generated resume or AI-evaluation report.
- Starting a new AI resume evaluation.
- Validation messages that require clearing or modifying existing data.
- Empty, partially completed, or newly created resume states.
- Persistence after a mutation or across another device/session.
- Employer-side access from an actual employer account.
- Application submission or the resume representation attached to an Application.
- Purchases, plan upgrades, privacy changes, and visibility configuration.

### Unclear or blocked

- The exact interactive path through the responsive profile menu was not reliably exposed to browser automation. The `/my-cv` destination was discovered from the Home-page header structure and opened directly.
- Whether the employer preview exactly matches every employer-side surface is unknown; it was observed only as the Candidate-side preview.
- Required-field validation could not be tested safely without modifying existing values or attempting a save.
- Download formats, generated language variants, and download permissions were not tested.

## Evidence

### E-001 — Logged-in Candidate can reach Resume Management from the Home context

- Type: observed
- Timestamp: 2026-08-07T17:12:53Z–2026-08-07T17:15:00Z
- Scope: JobVision Candidate, logged-in Production account, responsive Home header.
- Conditions: Existing authenticated Candidate session.
- Confidence: high
- Claim: The logged-in Home context exposes a Candidate resume destination labeled “رزومه من” with route `/my-cv`; opening that route displays the Candidate’s Resume Management page.
- Remaining uncertainty: The exact click sequence through the responsive profile popover was not reliably exercised by automation.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-002 — Resume Management organizes one resume into structured sections with completion state

- Type: observed
- Timestamp: 2026-08-07T17:15:00Z
- Scope: Existing completed resume in the Candidate self view.
- Conditions: This account displayed an overall completed state; the result must not be generalized to incomplete resumes.
- Confidence: high
- Claim: Resume Management presents a single structured professional profile with an overall completion indicator, per-section completion indicators, and navigation across identity, experience, skills, references, achievements, contact, attachments, portfolio, and assessment-related sections.
- Remaining uncertainty: Completion calculation rules and required sections were not tested.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-003 — Candidate self view exposes resume-management controls

- Type: observed
- Timestamp: 2026-08-07T17:15:00Z–2026-08-07T17:15:53Z
- Scope: Candidate self view of an existing completed resume.
- Conditions: Read-only observation; no control that mutates data was confirmed.
- Confidence: high
- Claim: In the default “خودم” view, the page exposes section-level add, edit, and delete controls alongside the current resume content.
- Remaining uncertainty: Permission, confirmation, validation, and persistence behavior behind those controls remains untested.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-004 — Employer preview removes management controls and limits displayed sections

- Type: observed
- Timestamp: 2026-08-07T17:15:27Z and subsequent controlled comparison
- Scope: Candidate-side “کارفرما” preview on the same Production resume.
- Conditions: Preview selected from the Resume Management page; no actual employer account was used.
- Confidence: high
- Claim: Switching the viewer from “خودم” to “کارفرما” removes visible add, edit, and delete controls while keeping the professional resume sections readable. In this account, the employer preview omitted the Candidate-only sections for audio introduction, uploaded personal resume, and assessment results, while still showing the contact-information section.
- Remaining uncertainty: Whether all real employer surfaces use this exact representation and whether plan, application, or privacy state changes visibility.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-005 — About Me opens a bilingual edit form at a save boundary

- Type: observed
- Timestamp: 2026-08-07T17:15:53Z
- Scope: About Me section in Candidate self view.
- Conditions: Existing values were left unchanged; the form was closed without saving.
- Confidence: medium
- Claim: The About Me section opens an edit dialog containing Persian and English job-title and self-description fields, a LinkedIn-profile field, and a “ذخیره تغییرات” action.
- Remaining uncertainty: No native required marker was observed and the save action was enabled in the prefilled account state, but empty-field validation and server-side rules were not tested.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-006 — Existing AI resume-evaluation results are available separately from starting a new evaluation

- Type: observed
- Timestamp: 2026-08-07T17:16:40Z
- Scope: AI assistant banner on the Candidate Resume Management page.
- Conditions: This account had a previous evaluation result; a new evaluation was not started.
- Confidence: high
- Claim: Resume Management provides separate actions to open the latest existing AI resume-evaluation result and to start a new evaluation. Opening the existing result displays a dated evaluation summary and exposes a report-download action.
- Remaining uncertainty: Evaluation criteria, entitlement rules, generation time, failure states, and report contents were not tested.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-007 — Resume download is exposed as a dedicated page-level control

- Type: observed
- Timestamp: 2026-08-07T17:15:00Z
- Scope: Candidate Resume Management top section.
- Conditions: Download was intentionally not initiated.
- Confidence: high
- Claim: The page exposes a dedicated “دانلود رزومه” control alongside viewer selection and resume-management features.
- Remaining uncertainty: Available formats, language selection, generation behavior, permissions, and failure handling were not observed.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

## Suspected bugs

- None recorded. Automation difficulty with the responsive profile popover is insufficient evidence of a user-facing bug.

## Coverage gaps

- Incomplete and empty resume states, including how overall completion is calculated.
- Safe validation testing with disposable data for each editable section.
- Save, cancel, delete-confirmation, error, and recovery behavior.
- Resume visibility and privacy controls across Candidate, Employer, Application, and resume-bank contexts.
- Real employer-account rendering and permissions.
- Generated resume preview/download variants and their language behavior.
- Upload constraints, file validation, replacement, deletion, and download behavior.
- New AI evaluation flow, entitlement rules, progress states, failures, and report generation.
- Multiple resumes or language variants, if supported.
- Current resume versus the resume representation associated with an Application.
- Mobile, keyboard, screen-reader, and accessibility coverage.

## Recommended follow-up recording

- Use a disposable Candidate account with an incomplete resume to test required fields, completion calculation, save/cancel behavior, and safe deletion confirmations.
- Run a separately approved download/upload walkthrough to cover generated formats, language variants, file limits, and error states.
- Compare Candidate employer-preview output with the same resume opened from a real employer context using approved test data.
- Record a separate Application walkthrough to determine whether employers see a live resume or an Application-specific snapshot.

## Related Product Areas

- Primary: JobVision Candidate / Resume Management (candidate area)
- Secondary candidate areas requiring team confirmation: Application Submission and Application Tracking
- Shared concept for later reconciliation only: `shared.resume`

## Suggested Product Knowledge updates

- Do not update canonical Product Knowledge from this draft package.
- After Owner review, compare accepted claims primarily with the Candidate Resume Management Product Area and secondarily with the shared Resume concept.
- Preserve the unresolved distinction between the current editable resume and any Application-associated resume representation.

## Handoff summary

Complete this section only after owner review.

- Package status: draft
- Accepted evidence IDs:
- Edited evidence IDs:
- Rejected evidence IDs:
- Remaining unknowns: See Coverage gaps.
- Suggested Product Knowledge scope: Candidate Resume Management; shared Resume concept only for genuinely cross-product meaning and relationships.

A reviewed package is an approved source for reconciliation. It is not canonical Product Knowledge and must not be copied directly into product documentation without comparison against the current `product-knowledge/main` branch.
