---
version: 2
name: cross-cutting-external-client-integrations-fetching-th-4bfa
description: "External API Integration via HTTP Fetch with Revalidation Caching: External Client Integrations Fetching Third Party"
metadata:
  actual:
    adr_id: 4bfabef6-0cc3-454d-a49d-107b94a29364
    status: accepted
    candidate_group_id: ca08aea7-a6f9-4743-961c-6e451b15f254
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - loaders/**
---

# External API Integration via HTTP Fetch with Revalidation Caching: External Client Integrations Fetching Third Party

Scope: applies to `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for modules that perform outbound HTTP requests to external third-party services to retrieve metadata or public metrics.

### Rules

- **R-EXT-001** MUST: External client integrations fetching third-party service data MUST configure request-level revalidation caching to limit repetitive remote network calls.
- **R-EXT-002** MUST: Configure appropriate time-to-live revalidation parameters matching the data freshness requirements of the consuming presentation components.
- **R-EXT-003** MUST: Ensure error handlers log sufficient context including attempt count and diagnostic error details without exposing authentication headers.
- **R-EXT-004** MUST: Before writing code that uses a versioned library, execute in order: dependency manifest discovery, build tool identification, lock file inspection, public documentation lookup for that exact version, and API existence confirmation.

### Verify

```bash
# Discover and run the project repository typecheck script to verify external API client typings
typecheck_script=$(npm pkg get scripts.typecheck --json 2>/dev/null || echo "tsc --noEmit")
if [ "$typecheck_script" != "null" ] && [ -n "$typecheck_script" ]; then
  npm run typecheck || npx tsc --noEmit
else
  npx tsc --noEmit
fi

# Discover and execute the project integration test suite to validate external client caching and retry behavior
test_script=$(npm pkg get scripts.test:integration --json 2>/dev/null || npm pkg get scripts.test --json 2>/dev/null)
if [ "$test_script" != "null" ] && [ -n "$test_script" ]; then
  npm run test:integration || npm test
else
  npx jest integration
fi
```

**Accept when:**
- Static analysis and test suites execute without errors across all external client modules.
- Mocked external requests confirm caching revalidation headers and retry logic function as specified.
- Outbound requests correctly use runtime environment variables for bearer token authentication.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration test suites and peer code reviews verify these rules.
</enforcement>