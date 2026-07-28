# Product Walkthrough

A tool-agnostic side project for turning guided product screen recordings into reviewed evidence packages.

This repository is intentionally separate from `hosseinmor/product-knowledge`.

```text
screen recording
→ AI evidence extraction
→ owner review
→ reviewed evidence package
→ Product Knowledge update proposal
→ branch and pull request in product-knowledge
```

## Core rule

Evidence extraction must not depend on existing Product Knowledge. The extraction AI should use only the recording and recorder-provided context so that existing documentation does not bias what it observes.

Product Knowledge is read only after owner review, during the separate reconciliation and update step.

## Repository structure

```text
AGENTS.md
→ tool-agnostic entry point

guides/recording.md
→ guidance for the person recording the walkthrough

guides/evidence-review.md
→ guidance for the product owner reviewing extracted evidence

rules/evidence.md
→ canonical evidence quality and classification rules

templates/evidence-package.md
→ single output artifact for extraction and review

ai/workflow.md
→ end-to-end walkthrough process

ai/skills/walkthrough/SKILL.md
→ execution contract for AI tools

walkthroughs/
→ optional reviewed evidence packages; never store large video files here
```

## Default operating model

1. A product expert selects a bounded area and records the product while explaining context and behavior.
2. AI extracts comprehensive evidence into one evidence package.
3. The relevant owner accepts, edits, or rejects each evidence claim.
4. Only accepted claims and owner-edited final claims become eligible for Product Knowledge reconciliation.
5. A separate AI session reads `product-knowledge/main`, proposes focused document changes, and opens a normal branch and pull request.

## Storage

Do not commit raw screen recordings, personal data, credentials, or large media files. Store recordings in an approved internal location and reference them from the evidence package.

## Canonical boundaries

- This repository owns walkthrough capture, extraction, evidence rules, and evidence review.
- `hosseinmor/product-knowledge` owns canonical Product Knowledge.
- A reviewed evidence package is a source for an update proposal, not canonical product truth.
