# Walkthrough Registry

This is the central index for walkthrough planning, package status, and product-area coverage. It helps select the next bounded scope, prevents duplicate IDs, and keeps known gaps visible.

The registry is operational metadata, not product evidence or canonical Product Knowledge. Do not copy claims from earlier packages into this file or use registry entries to complete a new extraction.

## Status model

- `planned` — the ID and bounded scope are reserved; extraction has not produced a package.
- `draft` — evidence has been extracted, but owner review is incomplete.
- `reviewed` — every evidence item has an owner decision and edited items have complete final claims.
- `handed-off` — the reviewed package has entered Product Knowledge reconciliation; record the proposal or pull request in notes.
- `cancelled` — the walkthrough stopped intentionally; keep the row so its ID is not reused.

Only `draft` and `reviewed` are evidence-package statuses. `planned`, `handed-off`, and `cancelled` describe the wider walkthrough lifecycle in this registry.

## Coverage model

- `not-assessed` — no extraction result exists yet.
- `partial` — the walkthrough covered meaningful behavior, but one or more paths, roles, states, or conditions in its bounded scope remain untested or unclear.
- `complete-for-scope` — the intended bounded scope was covered with no known gaps. This never means the whole product area is complete.

Coverage is an audit-planning assessment, not evidence confidence or owner approval. Record meaningful remaining gaps in the registry instead of inflating coverage.

## Product-area coverage

Use one row per product area. Base the summary only on registered walkthrough metadata and reviewed package coverage sections.

| Product group | Product | Product area | Coverage | Reviewed walkthroughs | Known gaps / next scope |
| --- | --- | --- | --- | --- | --- |
| JobVision | Candidate | Job Search (candidate area) | `not-assessed` | — | Complete the first bounded production walkthrough for logged-in search and filters. |
| JobVision | Candidate | Resume Management (candidate area) | `not-assessed` | — | Complete the first bounded production walkthrough for logged-in resume entry points, visible states, preview, and safe validation boundaries. |
| JobVision | Candidate | Job Details & Evaluation | `partial` | — | Draft WT-2026-005 covers the Saved Jobs empty state, one authorized save transition, and resulting one-item list. Next: removal, persistence, unavailable jobs, list navigation, and accessibility follow-up. |

## Walkthroughs

Use the next unused `WT-YYYY-NNN` value. Never renumber or reuse an ID.

| ID | Product / area | Bounded scope and context | Status | Coverage | Package | Updated | Notes / next gap |
| --- | --- | --- | --- | --- | --- | --- | --- |
| WT-2026-001 | JobVision Candidate / Job Search (candidate area) | Logged-in jobseeker in Production, starting at the home page; discover jobs and exercise visible search/filter controls. Excludes applying, profile/resume edits, purchases, and irreversible actions. | `draft` | `partial` | [evidence](WT-2026-001/evidence.md) | 2026-08-06 | Next gap: advanced filters and saved-search alerts in a disposable account, then mobile/keyboard coverage. Two suspected bugs require Owner review. |
| WT-2026-002 | JobVision Candidate / Application Submission flow (candidate area TBD) | Logged-in jobseeker in Production, starting at the home page; navigate to an eligible job and inspect the application entry point, pre-submit steps, visible validations, and the final submission boundary. Excludes final submission to a real employer unless a pre-approved test posting is identified, resume/profile edits, messages, purchases, and irreversible actions. | `planned` | `not-assessed` | — | 2026-08-06 | Browser-agent safety boundary: stop before any action that sends an application or otherwise affects a real employer; record that path as blocked unless a safe test posting is explicitly approved. |
| WT-2026-003 | JobVision Candidate / Resume Management (candidate area) | Logged-in jobseeker in Production, starting at the home page; navigate to Resume Management and inspect entry points, visible resume states, preview, and validations that can be reached without saving changes. Excludes saving or deleting resume data, uploads, applications, purchases, privacy changes, and any action affecting real data or users. | `draft` | `partial` | [evidence](WT-2026-003/evidence.md) | 2026-08-07 | Next gap: use a disposable incomplete-resume account to test required fields, completion rules, save/cancel/delete behavior, then compare Candidate preview with an approved real employer context. |
| WT-2026-003 | JobVision Candidate / Application Management flow (candidate area TBD) | Logged-in jobseeker in Production, starting at the home page; inspect the entry point, application list, visible statuses and filters, application details, and available management controls. Excludes withdrawing or deleting an application, sending messages, resume/profile edits, purchases, and any action that may affect a real employer or another user. | `draft` | `partial` | [evidence](WT-2026-003/evidence.md) | 2026-08-07 | Next gap: use disposable candidate and employer test accounts to demonstrate withdrawal, resume editing, every status transition, rejection feedback, and My Priority end to end; then test keyboard and screen-reader behavior. Three suspected bugs require Owner review. |
| WT-2026-003 | JobVision Candidate / Resume Management (candidate area) | Logged-in jobseeker in Production, starting at the home page; navigate to Resume Management and inspect entry points, visible resume states, preview, and validations that can be reached without saving changes. Excludes saving or deleting resume data, uploads, applications, purchases, privacy changes, and any action affecting real data or users. | `planned` | `not-assessed` | — | 2026-08-07 | Browser-agent safety boundary: read-only exploration; stop before save, delete, upload, submit, purchase, privacy changes, or any irreversible action. |
| WT-2026-004 | JobVision Candidate / Recommended Jobs & Preferences (candidate area TBD) | Logged-in jobseeker in Production, starting at the home page; inspect recommended-job surfaces, visible preference settings and entry points, personalization cues, navigation outcomes, and safe validation boundaries. Excludes saving or changing preferences, profile/resume edits, applying, uploads/downloads, purchases, messages, notifications, and any action affecting real data or other users. | `planned` | `not-assessed` | — | 2026-08-07 | Browser-agent safety boundary: read-only exploration; stop before save, submit, apply, upload/download, purchase, notification changes, or any action that persists account data. Product Area ownership remains TBD pending evidence and owner review. |
| WT-2026-005 | JobVision Candidate / Job Details & Evaluation — Saved Jobs flow | Logged-in jobseeker in Production, starting at the home page; inspect Saved Jobs entry points, saved-list structure and visible states, job-detail navigation outcomes, and safe boundaries around save/remove actions. Excludes saving or removing jobs, applying, profile/resume edits, uploads/downloads, purchases, messages, notifications, and any action that persists account data or affects other users. | `draft` | `partial` | [evidence](WT-2026-005/evidence.md) | 2026-08-08 | Empty state, one authorized save transition, and resulting one-item list covered. Next gap: removal, longer-term persistence, unavailable jobs, list-link navigation, and keyboard/mobile coverage. Two suspected bugs require Owner review. |
| WT-2026-004 | JobVision Candidate / Recommended Jobs & Preferences (candidate area TBD) | Logged-in jobseeker in Production, starting at the home page; inspect recommended-job surfaces, visible preference settings and entry points, personalization cues, navigation outcomes, and safe validation boundaries. Excludes saving or changing preferences, profile/resume edits, applying, uploads/downloads, purchases, messages, notifications, and any action affecting real data or other users. | `draft` | `partial` | [evidence](WT-2026-004/evidence.md) | 2026-08-07 | Next gap: use a disposable or approved test account to inspect the preference editor after onboarding, verify notification semantics and persistence, then cover empty states, mobile, and keyboard behavior. Product Area ownership remains TBD pending Owner review. |

## Update rules

Before a walkthrough:

1. Read this registry from the current `main` branch.
2. Check related coverage and known gaps without reading prior evidence claims.
3. Select a bounded scope, allocate the next unused ID, and add a `planned` row with `not-assessed` coverage.

After extraction:

1. Set the row to `draft`.
2. Set coverage to `partial` or `complete-for-scope` from the new package's Coverage and Coverage gaps sections.
3. Link the package when it is stored in this repository; otherwise write `workspace only`.
4. Add the most useful remaining gap or follow-up scope.

After owner review or handoff:

1. Set the row to `reviewed` only when the package meets all review completion criteria.
2. Set it to `handed-off` only after reconciliation starts, and link the proposal or pull request in notes.
3. Recalculate the product-area summary without treating one walkthrough as proof of the whole area.
4. Commit registry updates with the related walkthrough or handoff change whenever practical.
