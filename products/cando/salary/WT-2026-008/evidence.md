---
walkthrough_id: WT-2026-008
status: draft
product_group: Cando
product: salary
candidate_areas: [Team Management, Salary Benchmarking, Scenario Analysis, Organization Settings, Job Profile Management]
recorded_at: 2026-08-09
source:
  type: direct-product-audit
  reference: Production browser audit; no screen recording
reviewed_by: []
reviewed_at:
---

# Walkthrough Evidence Package

## Context

- Goal: Audit visible Salary Benchmark flows and controlled test-data actions.
- Actor: Authenticated organization user.
- Role: Exact role and permissions not identified.
- Authentication state: Logged in.
- Account, plan, or configuration: One production organization with existing team, job profiles, departments and business lines.
- Permissions: UI exposed create/edit/delete controls; exact permission model untested.
- Environment: Production.
- Starting point: Home, which resolved to Team.

## Coverage

### Covered

- Team list, search, employee creation, employee detail, edit and final-salary entry.
- Salary benchmark breakdown and scenario create/edit/delete.
- Management/team reports and report-download trigger.
- Job-profile creation and generated job-profile detail.
- Organization settings, department/business-line create/edit/delete guards.

### Narrated but not demonstrated

- None.

### Not covered

- Responsive/mobile behavior; unauthenticated and permission variants; network/error states; real organization-profile or calculation-model changes.

### Unclear or blocked

- Report download click produced no observable download or visible state change in this browser session.
- Full delete confirmation for employee was not shown; the delete command immediately reported success.

## Evidence

### E-001 — Team list exposes compensation comparison fields
- Type: observed
- Timestamp: Direct audit session, 2026-08-09
- Scope: Authenticated production organization, Team page.
- Conditions: Existing employee records.
- Confidence: high
- Claim: The Team table shows organizational fields plus 1404 salary, proposed 1405 salary range, and final 1405 salary; search can narrow the visible list by personnel code.
- Remaining uncertainty: Search matching semantics beyond the tested personnel-code query were not assessed.

#### Owner review
- Decision: pending
- Final claim:
- Owner note:

### E-002 — Employee creation validates required information before save
- Type: observed
- Timestamp: Direct audit session, 2026-08-09
- Scope: Add Employee dialog.
- Conditions: Empty form versus completed controlled test record.
- Confidence: high
- Claim: Add Employee groups required identity, organizational, and compensation fields; the save-and-calculate action was disabled initially and became enabled after required values and selections were supplied.
- Remaining uncertainty: Complete required/optional matrix was not exhaustively tested.

#### Owner review
- Decision: pending
- Final claim:
- Owner note:

### E-003 — Saving an employee triggers benchmark calculation
- Type: observed
- Timestamp: Direct audit session, 2026-08-09
- Scope: Controlled test employee in Production.
- Conditions: Test employee assigned an existing job profile and organization structure.
- Confidence: high
- Claim: After employee save, the Team row initially showed a calculating state and later displayed a proposed 1405 salary range.
- Remaining uncertainty: Calculation timing, retry behavior and failure state were not tested.

#### Owner review
- Decision: pending
- Final claim:
- Owner note:

### E-004 — Employee details show model-level benchmark inputs
- Type: observed
- Timestamp: Direct audit session, 2026-08-09
- Scope: Controlled test employee detail drawer.
- Conditions: Existing benchmark result.
- Confidence: high
- Claim: Employee detail displays proposed and final salary, payment strategy, complexity, and per-model benchmark sections with weights, source descriptions and percentile/range values when available; one model displayed insufficient-data messaging.
- Remaining uncertainty: Model-weight semantics and all source-data conditions require owner review.

#### Owner review
- Decision: pending
- Final claim:
- Owner note:

### E-005 — Final salary can be recorded independently of proposed range
- Type: observed
- Timestamp: Direct audit session, 2026-08-09
- Scope: Controlled test employee.
- Conditions: Final-salary dialog; a test amount within the visible proposed range was saved.
- Confidence: high
- Claim: The employee-detail and Team surfaces allow a final 1405 salary to be recorded and display its percentage comparison to 1404 salary.
- Remaining uncertainty: Edit/remove behavior for final salary was not fully tested.

#### Owner review
- Decision: pending
- Final claim:
- Owner note:

### E-006 — Scenario analysis persists and recalculates comparison columns
- Type: observed
- Timestamp: Direct audit session, 2026-08-09
- Scope: Scenario Analysis page.
- Conditions: A test scenario using a complexity coefficient was created, later edited and deleted.
- Confidence: high
- Claim: A scenario can enable a complexity coefficient or payment strategy, save and calculate a named scenario column, then be reopened for edit; saving the edit recalculated the scenario column.
- Remaining uncertainty: Multi-filter and combined-setting semantics were not tested.

#### Owner review
- Decision: pending
- Final claim:
- Owner note:

### E-007 — Scenario deletion requires confirmation
- Type: observed
- Timestamp: Direct audit session, 2026-08-09
- Scope: Test scenario.
- Conditions: Scenario overflow delete control.
- Confidence: high
- Claim: Deleting a scenario shows a confirmation warning that all scenario information will be removed; the test scenario was then deleted.
- Remaining uncertainty: Recovery after deletion was not tested.

#### Owner review
- Decision: pending
- Final claim:
- Owner note:

### E-008 — Job-profile creation resolves a standard job title
- Type: observed
- Timestamp: Direct audit session, 2026-08-09
- Scope: Job Profiles.
- Conditions: Real user-provided title and selected seniority.
- Confidence: high
- Claim: A job profile requires title, seniority and standard job title; after selecting a standard title, the product confirmed creation and supplied a proposed job-profile dossier with editable requirements and content.
- Remaining uncertainty: Rules for standard-title suggestions and profile generation are not established.

#### Owner review
- Decision: pending
- Final claim:
- Owner note:

### E-009 — Structure deletion is blocked when employees are assigned
- Type: observed
- Timestamp: Direct audit session, 2026-08-09
- Scope: Department and Business Line settings.
- Conditions: Selected records with assigned employees.
- Confidence: high
- Claim: Attempting to delete a department or business line with assigned employees is blocked and instructs the user to move employees to another unit first.
- Remaining uncertainty: Deletion behavior for empty units was not tested.

#### Owner review
- Decision: pending
- Final claim:
- Owner note:

### E-010 — Team report download trigger had no observed output
- Type: observed
- Timestamp: Direct audit session, 2026-08-09
- Scope: Team Report page in browser audit.
- Conditions: Authenticated production session; download control clicked twice.
- Confidence: medium
- Claim: Clicking the Team Report download control produced no observable browser download, new tab, or visible page-state change in this audit session.
- Remaining uncertainty: This may be browser/session-specific; it is not an intended-product rule.

#### Owner review
- Decision: pending
- Final claim:
- Owner note:

## Suspected bugs

### B-001 — Report-download control produced no observable output
- Timestamp: Direct audit session, 2026-08-09
- Scope: Team Report download control.
- Observation: Two attempts yielded no captured download, new tab or visible feedback.
- Why it may be a bug: A control labelled for report download gave no observable outcome.
- Owner note:

### B-002 — Employee deletion lacked a second confirmation in the observed flow
- Timestamp: Direct audit session, 2026-08-09
- Scope: Controlled test employee deletion.
- Observation: Selecting Delete Employee reported success without an observed confirmation dialog.
- Why it may be a bug: The destructive action may be insufficiently guarded; browser state should be reproduced before deciding.
- Owner note:

## Coverage gaps

- Permission/role, unauthenticated, error, empty and responsive/mobile states.
- Saving real organization profile or model-weight changes was intentionally not performed.
- Test employee was deleted; the real job profile created at the user’s direction remains.

## Recommended follow-up recording

- Use a disposable organization to test error handling, permissions, empty structures and controlled calculation-model changes.
- Validate the report-download behavior in a standard user browser.

## Handoff summary

Complete this section only after owner review.

- Package status: draft
- Accepted evidence IDs:
- Edited evidence IDs:
- Rejected evidence IDs:
- Remaining unknowns: See Coverage gaps.
- Suggested Product Knowledge scope: Cando Salary Benchmark — Team Management, Benchmark Calculation, Scenario Analysis, Job Profiles, Organization Settings.
