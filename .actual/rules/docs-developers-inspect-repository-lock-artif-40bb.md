# Fumadocs Library Adoption for Documentation Architecture: Developers Inspect Repository Lock Artifact Verify

These rules are ALWAYS ACTIVE for all documentation application layout wrappers, page routes, content loading, source indexing, and search overlay modules.

### Rules

- **R-FUM-001** MUST: Developers MUST inspect the repository lock artifact and verify the exact resolved version of all Fumadocs dependencies before writing or modifying code that consumes Fumadocs APIs.

### Verify

```bash
# Discover and execute the repository dependency audit script to confirm resolved Fumadocs package versions adhere to the lock artifact.
# Discover and run the project typecheck and lint verification tasks to confirm Fumadocs layout imports and source loader interfaces conform to design constraints.
# Discover and execute the workspace test suite to validate that documentation layouts, search components, and MDX loaders render successfully.
```

**Accept when:**
- All documentation and blog page routes resolve navigation and content via Fumadocs UI layouts and Core source loaders without runtime errors.
- Static analysis, type checking, and linting suites pass without unapproved custom documentation layout implementations.
- The project test suite passes with all documentation rendering and search dialog integration tests verified.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration checks executing typechecking, linting, and build verification, as well as architectural peer review.
</enforcement>