---
version: 2
name: cross-cutting-consumer-components-handle-loading-fallb-2765
description: "Adoption of @/loaders/stars Module for Repository Metrics: Consumer Components Handle Loading Fallback States"
metadata:
  actual:
    adr_id: 276534a8-834d-4bc8-8d6a-b9fa007751dd
    status: accepted
    candidate_group_id: 43667bb6-7881-43a1-aeec-aa06921cc0ca
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# Adoption of @/loaders/stars Module for Repository Metrics: Consumer Components Handle Loading Fallback States

Scope: applies to `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for documentation UI components displaying repository star counts or ecosystem popularity metrics.

### Rules

- **R-STARS-001** SHOULD: Consumer components SHOULD handle loading and fallback states as defined by the @/loaders/stars module contract.
- **R-STARS-002** MANDATORY: Consumer components should treat the data returned by @/loaders/stars as read-only presentation models.
- **R-STARS-003** MANDATORY: Any caching, revalidation, or fallback handling must remain encapsulated within the loader module boundary.
- **R-STARS-004** MANDATORY (DISCOVERY POLICY): The consumer MUST discover tool names, file names, commands, package managers, and versions from the project repository.
- **R-STARS-005** MANDATORY (LOCK-VERSION GROUNDING): Before writing code using a versioned library, find manifest, identify build tool, inspect lock/resolution artifact for exact version, look up official docs for that version, confirm API existence, and re-verify per dependency at point of use.

### Verify

```bash
# Discover and run the project static analysis and module boundary verification scripts
# to confirm that star metrics imports originate exclusively from @/loaders/stars.
# Discover and execute the project test runner to verify that components consuming 
# @/loaders/stars render metric data according to the module contract.
```

**Accept when:**
- All UI components rendering repository star metrics import star data exclusively from the @/loaders/stars module.
- Static analysis and module boundary checks pass with zero unauthorized direct network imports for repository metadata in presentation components.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated review blocks pull requests containing direct external metric fetches in UI components, and code violations must be refactored to consume the @/loaders/stars module prior to merge.
</enforcement>