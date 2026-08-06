# Walkthrough Packages

This directory contains the central Walkthrough Registry and may contain reviewed evidence packages when repository-based audit history is useful.

Do not commit raw recordings or large media files. Store recordings in an approved internal location and reference them from the package metadata.

Recommended structure:

```text
walkthroughs/
├── index.md
└── WT-YYYY-NNN/
    └── evidence.md
```

`index.md` tracks walkthrough lifecycle status and coverage metadata. AI must read it before each walkthrough to select a bounded gap and allocate the next unused ID, then update it after extraction, owner review, and handoff as applicable.

Registry metadata must not contain product claims and must not be used to complete evidence. During extraction, linked prior packages remain outside the allowed evidence sources.

A package may be added here only when:

- The relevant owner has reviewed every evidence item.
- The package status is `reviewed`.
- Edited evidence has complete final claims.
- Sensitive data has been removed.
- The recording reference is accessible only to authorized people.

Draft extraction may remain in the AI workspace instead of Git.

When a draft is not committed, its registry package value should be `workspace only`. Keep the registry row so the ID, scope, status, coverage, and next gap remain visible.
