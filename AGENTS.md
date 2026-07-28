# AI Entry Point

Use this repository only for product walkthrough capture, evidence extraction, evidence review, and handoff preparation.

## Routing

When the user provides a screen recording or asks to extract product behavior from one:

1. Read `ai/skills/walkthrough/SKILL.md`.
2. Follow `ai/workflow.md`.
3. Apply `rules/evidence.md`.
4. Produce output using `templates/evidence-package.md`.

When the user asks how to record a walkthrough, use `guides/recording.md`.

When the user asks how to review extracted evidence, use `guides/evidence-review.md`.

## Isolation rule

During evidence extraction, do not read Product Knowledge, previous walkthrough conclusions, PRDs, or design documents unless the user explicitly asks for comparison. Extract only what is observable, narrated, or cautiously inferred from the supplied recording and context.

## Handoff rule

Do not write directly to `hosseinmor/product-knowledge` from raw or unreviewed evidence.

Only a reviewed evidence package may be handed off. During handoff, use the current `main` branch of `hosseinmor/product-knowledge`, propose focused changes, preserve unknowns, and use a dedicated branch and pull request.

## Safety

- Never expose credentials, personal data, or sensitive account information.
- Never claim that narrated behavior was observed.
- Never generalize one account, role, or state to all contexts without explicit evidence.
- Never treat suspected bugs as intended product rules.
- Never store large video files in Git.
