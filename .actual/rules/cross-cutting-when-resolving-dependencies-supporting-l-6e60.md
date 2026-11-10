---
version: 2
name: cross-cutting-when-resolving-dependencies-supporting-l-6e60
description: "Adoption of @/loaders/stars Module for Repository Metrics: When Resolving Dependencies Supporting Loader Infrastructure"
metadata:
  actual:
    adr_id: 6e60ad8b-59b4-485e-893d-0791414e909d
    status: accepted
    candidate_group_id: 43667bb6-7881-43a1-aeec-aa06921cc0ca
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# Adoption of @/loaders/stars Module for Repository Metrics: When Resolving Dependencies Supporting Loader Infrastructure

Scope: applies to `packages/docs/components/**`.

These rules are ALWAYS ACTIVE for documentation UI components displaying repository star counts, ecosystem popularity metrics, or presentation elements requiring standardized star pill indicators or ecosystem summaries.

### Rules

- **R-LOADER-001** MUST: When resolving dependencies supporting the loader infrastructure, the consumer MUST inspect the repository lock artifact to determine the exact resolved versions before point of use.
- **R-LOADER-002** MUST: All UI components rendering repository star metrics import star data exclusively from the @/loaders/stars module.
- **R-LOADER-003** MUST: Treat data returned by @/loaders/stars as read-only presentation models, encapsulating all caching, revalidation, or fallback handling within the loader module boundary.

### Verify

```bash
# Discover and run project static analysis and module boundary verification scripts
# to confirm star metrics imports originate exclusively from @/loaders/stars.
npm run test:boundaries || yarn test:boundaries || pnpm test:boundaries

# Discover and execute project test runner to verify component metric rendering contracts
npm test || yarn test || pnpm test
```

**Accept when:**
- All UI components rendering repository star metrics import star data exclusively from the @/loaders/stars module.
- Static analysis and module boundary checks pass with zero unauthorized direct network imports for repository metadata in presentation components.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated linting, module boundary checks, and mandatory peer code reviews enforce these rules.
</enforcement>