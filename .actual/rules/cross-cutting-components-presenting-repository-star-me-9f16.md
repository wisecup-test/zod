---
version: 2
name: cross-cutting-components-presenting-repository-star-me-9f16
description: "Adoption of @/loaders/stars Module for Repository Metrics: Components Presenting Repository Star Metrics Import"
metadata:
  actual:
    adr_id: 9f164433-dba6-4dea-8efa-e328749b3ab6
    status: accepted
    candidate_group_id: 43667bb6-7881-43a1-aeec-aa06921cc0ca
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# Adoption of @/loaders/stars Module for Repository Metrics: Components Presenting Repository Star Metrics Import

Scope: applies to `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for:
- Documentation UI components displaying repository star counts or ecosystem popularity metrics.
- Presentation elements requiring standardized star pill indicators or ecosystem summaries.

### Rules

- **R-LM-001** MUST: Components presenting repository star metrics MUST import star data exclusively from the internal @/loaders/stars module.

### Verify

- Discover and run the project static analysis and module boundary verification scripts to confirm that star metrics imports originate exclusively from @/loaders/stars.
- Discover and execute the project test runner to verify that components consuming @/loaders/stars render metric data according to the module contract.

**Accept when:**

- All UI components rendering repository star metrics import star data exclusively from the @/loaders/stars module.
- Static analysis and module boundary checks pass with zero unauthorized direct network imports for repository metadata in presentation components.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated linting and module boundary checks verifying import sources for repository star data.
- Verified by: Mandatory peer code review for all new UI components presenting ecosystem or repository metrics.
- Violation handling: Pull requests containing direct external metric fetches in UI components are blocked by automated review gates.
- Violation handling: Code violations must be refactored to consume the @/loaders/stars module prior to merge.
- Exception process: Submit an architectural exception request detailing why the internal loader module cannot fulfill the specific metric retrieval requirements.
- Exception process: Require formal approval from the documentation architecture leads before introducing alternative metric sources.
</enforcement>
