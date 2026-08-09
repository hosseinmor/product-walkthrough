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

walkthroughs/index.md
→ central walkthrough status and product-area coverage registry

walkthroughs/products/<product-group>/<product>/WT-YYYY-NNN/evidence.md
→ product-organized evidence package; use lowercase canonical slugs and never store large video files here
```

## Canonical walkthrough storage rule

Every evidence package MUST use this exact structure:

```text
walkthroughs/products/<product-group>/<product-module>/WT-YYYY-NNN/evidence.md
```

Before creating a package, inspect the existing folders under `walkthroughs/products/` and reuse the canonical product-group and product-module names already used there. Never derive a folder name from a URL, UI label, or an assumed slug. If the canonical product-module folder does not exist, create that folder path by creating the evidence file there, then add the exact path to `walkthroughs/index.md`.

## Default operating model

1. AI reads `walkthroughs/index.md`, selects a bounded gap, allocates the next walkthrough ID, and registers the scope as `planned`.
2. A product expert records the product while explaining context and behavior.
3. AI extracts comprehensive evidence into one evidence package, then updates registry status and coverage.
4. The relevant owner accepts, edits, or rejects each evidence claim; AI updates the registry when review completes.
5. Only accepted claims and owner-edited final claims become eligible for Product Knowledge reconciliation.
6. A separate AI session reads `product-knowledge/main`, proposes focused document changes, and opens a normal branch and pull request.

The registry contains planning and coverage metadata only. It must not be used as evidence or as a source for completing claims during extraction.

## Storage

Group evidence packages first by product group and then by product, for example `walkthroughs/products/jobvision/candidate/WT-YYYY-NNN/evidence.md`. Keep the central lifecycle and coverage registry at `walkthroughs/index.md`.

Do not commit raw screen recordings, personal data, credentials, or large media files. Store recordings in an approved internal location and reference them from the evidence package.

## Canonical boundaries

- This repository owns walkthrough capture, extraction, evidence rules, and evidence review.
- `hosseinmor/product-knowledge` owns canonical Product Knowledge.
- A reviewed evidence package is a source for an update proposal, not canonical product truth.
