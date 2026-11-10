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

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-STARS-001** MUST: Components presenting repository star metrics MUST import star data exclusively from the internal @/loaders/stars module.

### Verify

```bash
# Discover and run the project static analysis and module boundary verification scripts
# to confirm that star metrics imports originate exclusively from @/loaders/stars.

# Example discovery-based execution (adjust commands to match repository conventions):
npm run lint || yarn lint || pnpm lint
npm test || yarn test || pnpm test
```

**Accept when:**
- All UI components rendering repository star metrics import star data exclusively from the @/loaders/stars module.
- Static analysis and module boundary checks pass with zero unauthorized direct network imports for repository metadata in presentation components.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>