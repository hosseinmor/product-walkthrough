# Evidence Rules

These are the canonical rules for extracting product evidence from a walkthrough recording.

## 1. Evidence is a product claim

Each item must describe meaningful product behavior, such as a user outcome, business rule, permission, state transition, validation, persistence rule, alternate path, recovery behavior, or visible shared-service dependency.

Do not create separate evidence items for every click, label, or visual element.

Bad:

> An Edit button is visible.

Better:

> The request owner can open and edit a draft request from the request list.

## 2. Extract independently

During extraction, do not read Product Knowledge or use previous documentation to complete, normalize, or reinterpret the recording.

Existing knowledge is used later, after owner review, during reconciliation.

## 3. Evidence types

Every evidence item must use one type:

- `observed` — directly visible in the recording.
- `narrated` — stated by the recorder but not demonstrated.
- `inferred` — cautiously derived from visible signals or multiple observations.

Never label narrated or inferred behavior as observed.

Use inferred evidence sparingly and state the remaining uncertainty.

## 4. Traceability

Every evidence item must include at least one timestamp or time range. When multiple moments support one claim, include all relevant references.

The timestamp must point to the action, visible result, or narration that supports the claim.

## 5. Scope

Each claim must state the conditions that materially limit it, when known:

- Actor or role
- Authentication state
- Product state or lifecycle status
- Account, plan, or configuration
- Permission
- Preconditions
- Environment

Do not generalize one observed context to all users or accounts.

## 6. Atomic but meaningful

One evidence item should contain one reviewable product claim. It may summarize several consecutive UI steps when they support the same behavior.

Split an item when its parts could receive different owner decisions.

## 7. Comprehensive extraction

Extract all meaningful behavior actually present in the recording, including narrated rules and explicit uncertainty.

Comprehensive means complete relative to the recording, not complete relative to the whole product area.

The output must explicitly list:

- Covered behavior
- Narrated but not demonstrated behavior
- Not covered behavior mentioned by the recorder
- Unclear or blocked behavior

## 8. No silent completion

Do not fill gaps using common product patterns, assumptions, interface labels, or prior knowledge.

When evidence is insufficient:

- Keep the claim narrow.
- Lower confidence.
- Mark the uncertainty.
- Or record the case as a coverage gap instead of creating a claim.

## 9. Suspected bugs

A surprising or inconsistent behavior may be listed as a suspected bug, but it must not be rewritten as an intended product rule.

A suspected bug still needs a timestamp and scope.

## 10. Confidence

Use:

- `high` — direct, clear, and unambiguous evidence.
- `medium` — direct evidence with meaningful contextual uncertainty.
- `low` — narrated, inferred, incomplete, or ambiguous evidence.

Confidence is an extraction assessment, not an owner decision.

## 11. Review boundary

AI does not approve evidence. The owner decides whether each item is accepted, edited, or rejected.

Only accepted claims and complete owner-edited final claims are eligible for Product Knowledge reconciliation.

## 12. Privacy and safety

Do not reproduce credentials, personal data, private messages, tokens, sensitive customer data, or unnecessary identifying information in the evidence package.

Describe sensitive values generically when they are not material to product behavior.
