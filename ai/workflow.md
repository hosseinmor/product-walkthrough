# Product Walkthrough Workflow

This workflow turns a guided product screen recording into a reviewed evidence package and then hands that package to a separate Product Knowledge reconciliation process.

## Phase 0 — Check and register

Before recording or extracting evidence, the AI must read `walkthroughs/index.md` from the current `main` branch.

Use the registry to:

1. Check related product-area coverage and known gaps.
2. Confirm that the proposed scope is bounded and not an accidental duplicate.
3. Allocate the next unused `WT-YYYY-NNN` ID.
4. Resolve the lowercase product-group and product slugs for the package path.
5. Add or update a `planned` row with `not-assessed` coverage.

Store packages at `products/<product-group>/<product>/WT-YYYY-NNN/evidence.md`. The registry remains centralized at `walkthroughs/index.md`.

The registry is planning metadata only. Do not read linked prior packages or use registry wording as product evidence during extraction.

## Phase 1 — Record

A product expert selects a bounded product area or flow and records the product while explaining context, behavior, rules, uncertainty, and omitted paths.

Use `guides/recording.md`.

No formal walkthrough plan is required for guided screen recordings.

## Phase 2 — Extract evidence

Input:

- Screen recording
- Optional recorder notes
- Optional product or area name

The extraction AI must:

1. Read `rules/evidence.md`.
2. Use `templates/evidence-package.md`.
3. Infer the actual scope from the recording without pretending that an unprovided plan existed.
4. Extract all meaningful product behavior present in the recording.
5. Separate observed, narrated, and inferred claims.
6. Add timestamps and contextual limits.
7. Record coverage gaps, uncertainty, and suspected bugs.
8. Leave all owner decisions as `pending`.
9. Store one evidence package at `products/<product-group>/<product>/WT-YYYY-NNN/evidence.md`.
10. Update the registry row to `draft`, set its coverage assessment, link the product-organized package, and record the most useful next gap.

During this phase, do not read Product Knowledge, PRDs, prior walkthrough conclusions, or design documents unless the user explicitly requests comparison.

Output:

```text
products/<product-group>/<product>/WT-YYYY-NNN/evidence.md
```

## Phase 3 — Owner review

The relevant product owner reviews each evidence item using `guides/evidence-review.md`.

Allowed decisions:

- accepted
- edited
- rejected

For edited evidence, the owner writes a complete final claim.

The package becomes `reviewed` only when every item has a decision and all edited items have a final claim.

After completion, update the registry row to `reviewed` and recalculate the related product-area coverage summary. Do not mark an entire product area complete from one bounded walkthrough.

## Phase 4 — Prepare handoff

The reviewed package must clearly identify:

- Accepted evidence
- Owner-edited final claims
- Rejected evidence
- Remaining unknowns
- Candidate product areas
- Reviewer and review date

The reviewed package is the boundary between this repository and Product Knowledge.

When reconciliation starts, update the registry row to `handed-off` and add the proposal or pull request link in notes.

## Phase 5 — Reconcile with Product Knowledge

This is a separate task and may run in a separate AI environment.

Input:

- Reviewed evidence package
- Current `main` branch of `hosseinmor/product-knowledge`

The reconciliation AI must:

1. Read the current repository entry point and manifest.
2. Select the smallest relevant Product Knowledge documents.
3. Compare each approved claim with current knowledge.
4. Classify it as supporting, extending, contradicting, or outside current documentation.
5. Preserve remaining uncertainty.
6. Propose focused changes only where useful.
7. Show the proposed document changes for human review.
8. Use a dedicated branch and pull request after approval.
9. Regenerate the Product Knowledge manifest when indexed documents change.

Do not copy the evidence package into Product Knowledge as a new permanent artifact.

## Browser-agent variant

When an AI agent explores the product directly, define scope, safety constraints, permitted actions, forbidden actions, account context, and stop conditions before execution.

The output remains the same evidence package and follows the same owner review and handoff process.

The browser-agent variant must also check and update `walkthroughs/index.md` before and after the walkthrough.
