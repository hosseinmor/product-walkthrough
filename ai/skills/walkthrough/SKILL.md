# Walkthrough Skill

## Trigger

Use this Skill when the user asks to:

- Analyze a product screen recording
- Extract product behavior or evidence from a walkthrough
- Turn recorder narration into reviewable evidence
- Review or complete a walkthrough evidence package
- Prepare a reviewed evidence package for Product Knowledge handoff

Do not use it for general product Q&A, PRD writing, design exploration, or direct Product Knowledge updates without a reviewed evidence package.

## Contracts

```text
ai/workflow.md
→ process contract

rules/evidence.md
→ evidence quality contract

templates/evidence-package.md
→ output contract

guides/recording.md
→ recorder guidance

guides/evidence-review.md
→ owner review guidance
```

## Mode A — Evidence extraction

Input:

- A screen recording or a reliable transcript with visual references
- Optional recorder notes
- Optional product or area label

Process:

1. Use only the supplied recording and recorder context.
2. Do not read Product Knowledge or previous documentation.
3. Determine the actual observed scope.
4. Extract comprehensive, meaningful, timestamped claims.
5. Classify each claim as observed, narrated, or inferred.
6. Preserve conditions and uncertainty.
7. Record coverage gaps and suspected bugs.
8. Produce one evidence package using the template.
9. Leave owner decisions pending.

Output:

- One draft evidence package
- No Product Knowledge edits
- No claims of owner approval

## Mode B — Evidence review support

Input:

- Draft evidence package
- Owner corrections or decisions

Process:

1. Apply the owner decisions exactly.
2. For edited items, require a complete final claim.
3. Do not reinterpret a rejected item as approved.
4. Keep rejected evidence and remaining gaps visible for audit.
5. Mark the package reviewed only when completion criteria are met.

Output:

- One reviewed evidence package

## Mode C — Handoff preparation

Input:

- Reviewed evidence package

Process:

1. Verify that every evidence item has a decision.
2. Select only accepted claims and edited final claims as approved evidence.
3. Summarize candidate product areas and unresolved questions.
4. Prepare a clean handoff package.

Do not update Product Knowledge in this mode unless the user explicitly starts a separate reconciliation task and current access to `hosseinmor/product-knowledge/main` is available.

## Non-negotiable rules

- Narrated behavior is not observed behavior.
- Existing Product Knowledge must not bias extraction.
- One recording proves only the context it covers.
- Suspected bugs are not intended rules.
- AI does not approve evidence.
- Reviewed evidence is a source, not canonical Product Knowledge.
- Raw or unreviewed evidence must never trigger a direct Product Knowledge update.
