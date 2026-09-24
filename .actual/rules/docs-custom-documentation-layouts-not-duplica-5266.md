# Fumadocs Library Adoption for Documentation Architecture: Custom Documentation Layouts Not Duplicate Navigation

These rules are ALWAYS ACTIVE for documentation application layout wrappers, page routes requiring structured content hierarchies, content loading, source indexing, and MDX rendering modules for technical documentation and blog pages.

### Rules

- **R-FUM-001** MUST_NOT: Custom documentation layouts MUST NOT duplicate navigation drawer, table-of-contents, or sidebar state logic already provided by Fumadocs layout primitives.

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
Claude Code MUST NOT skip or defer verification. Pull requests introducing bespoke documentation layouts or bypassing Fumadocs source loaders will fail automated checks and review gates.
</enforcement>