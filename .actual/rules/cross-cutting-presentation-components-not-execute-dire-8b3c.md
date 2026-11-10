---
version: 2
name: cross-cutting-presentation-components-not-execute-dire-8b3c
description: "Adoption of @/loaders/stars Module for Repository Metrics: Presentation Components Not Execute Direct Remote"
metadata:
  actual:
    adr_id: 8b3cf220-5fac-44e4-9346-c329b6dd690e
    status: accepted
    candidate_group_id: 43667bb6-7881-43a1-aeec-aa06921cc0ca
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# Adoption of @/loaders/stars Module for Repository Metrics: Presentation Components Not Execute Direct Remote

Scope: applies to `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for documentation UI components displaying repository star counts or ecosystem popularity metrics.

### Rules

- **R-STARS-001** MUST_NOT: Presentation components MUST NOT execute direct remote network requests or API queries to retrieve repository star counts.

### Verify

```bash
# Discover and run the project static analysis and module boundary verification scripts
# Discover and execute the project test runner
```

**Accept when:**
- All UI components rendering repository star metrics import star data exclusively from the @/loaders/stars module.
- Static analysis and module boundary checks pass with zero unauthorized direct network imports for repository metadata in presentation components.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>