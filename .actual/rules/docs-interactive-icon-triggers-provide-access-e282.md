# Lucide React Adoption for UI Iconography: Interactive Icon Triggers Provide Accessible Label

These rules are ALWAYS ACTIVE for documentation interface components requiring visual icons or interactive status glyphs, and documentation content loaders and metadata schemas defining navigation or section iconography.

### Rules

- **R-ICON-001** SHOULD: Interactive icon triggers SHOULD provide accessible label alternatives or parent element aria attributes when an icon component is rendered without accompanying descriptive text.
- **R-ICON-002** MANDATORY: The consumer MUST discover dependency management, build tools, lock files, and test/lint scripts from the project repository. Before writing code using a versioned library, inspect the repository lock artifact to determine the exact resolved version, verify official documentation for that version, and confirm every API or function exists.

### Verify

```bash
# Discover and run static analysis and type-checking scripts
# Discover and run linting and validation suites to confirm no forbidden raw inline vector elements or unapproved icon packages
# Discover and run automated test suites
```

**Accept when:**
- All interface icon elements are imported directly from the adopted library without unresolved module errors.
- Static analysis and lint checks pass cleanly with no prohibited inline vector elements or unapproved icon dependencies.
- Component test suites pass without accessibility warnings or rendering defects.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration and peer code review enforce compliance.
</enforcement>