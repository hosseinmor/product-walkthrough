# Reviewing Walkthrough Evidence

The reviewer confirms whether each extracted claim is reliable enough to use as a source for Product Knowledge reconciliation.

The reviewer is usually the owner of the relevant product area. Evidence about a shared service may also require the service owner.

## Review decisions

Use one decision for each evidence item:

- `accepted` — the claim and its scope are correct.
- `edited` — the evidence is useful, but the claim or scope must be corrected. Write the complete final claim.
- `rejected` — the claim is incorrect, misleading, unsupported, or not representative.

A rejected item may still be marked as a suspected bug or a follow-up question, but it must not be used as product truth.

## What to check

For each item, verify:

- Is the claim accurate?
- Is it described at the right level, rather than as isolated UI detail?
- Is its type correct: observed, narrated, or inferred?
- Does the timestamp support it?
- Are the role, state, permission, account, and preconditions clear?
- Has the claim been generalized beyond the evidence?
- Could the behavior be a bug, temporary state, or test-data artifact?
- Does the final wording preserve uncertainty where needed?

You do not need to rewatch the whole recording. Open the cited timestamp when a claim is unclear, high impact, contradictory, inferred, or potentially a bug.

## Editing a claim

When choosing `edited`, write a complete standalone `final_claim`. Do not write only a correction note.

Bad:

> Only for some accounts.

Good:

> The request owner can edit the submitted request until the first approver action, only when the request uses an approval workflow.

## Completion criteria

An evidence package is ready for handoff only when:

- Its overall status is `reviewed`.
- Every evidence item has a decision.
- Every edited item has a complete final claim.
- Rejected items are excluded from the approved evidence set.
- Remaining coverage gaps and uncertainties stay visible.
- The reviewer name and review date are recorded.

Review does not directly update Product Knowledge. It produces an approved source package for a separate reconciliation step.
