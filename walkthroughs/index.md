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
| — | — | — | `not-assessed` | — | Add the first bounded walkthrough. |

## Walkthroughs

Use the next unused `WT-YYYY-NNN` value. Never renumber or reuse an ID.

| ID | Product / area | Bounded scope and context | Status | Coverage | Package | Updated | Notes / next gap |
| --- | --- | --- | --- | --- | --- | --- | --- |
| — | — | — | — | — | — | — | Add a `planned` row before the first walkthrough. |

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
