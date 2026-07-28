# Walkthrough Packages

This directory may contain reviewed evidence packages when repository-based audit history is useful.

Do not commit raw recordings or large media files. Store recordings in an approved internal location and reference them from the package metadata.

Recommended structure:

```text
walkthroughs/
└── WT-YYYY-NNN/
    └── evidence.md
```

A package may be added here only when:

- The relevant owner has reviewed every evidence item.
- The package status is `reviewed`.
- Edited evidence has complete final claims.
- Sensitive data has been removed.
- The recording reference is accessible only to authorized people.

Draft extraction may remain in the AI workspace instead of Git.
