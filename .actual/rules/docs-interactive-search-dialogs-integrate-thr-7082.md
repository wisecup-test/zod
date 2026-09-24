# Fumadocs Library Adoption for Documentation Architecture: Interactive Search Dialogs Integrate Through Fumadocs

These rules are ALWAYS ACTIVE for documentation application layout wrappers, page routes, content loading, source indexing, MDX rendering modules, search overlay dialogs, and navigation components within the documentation workspace.

### Rules

- **R-FUM-001** SHOULD: Interactive search dialogs SHOULD integrate through `fumadocs-ui/components/dialog/search` abstractions to align with standard documentation keyboard navigation and modal behavior.

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
Claude Code MUST NOT skip or defer verification. Automated continuous integration checks and architectural peer reviews enforce adherence; violations will fail automated checks and review gates.
</enforcement>