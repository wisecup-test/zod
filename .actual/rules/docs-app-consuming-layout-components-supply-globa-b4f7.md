# fumadocs-ui Layout Adoption for Documentation and Content Presentation: Consuming Layout Components Supply Global Navigation

These rules are ALWAYS ACTIVE for route layout components serving documentation, blog, or content landing pages within the documentation application.

### Rules

- **R-FUMA-001** MUST: Consuming layout components MUST supply global navigation attributes through centralized shared layout configuration modules to maintain cross-route visual consistency.
- **R-FUMA-002** MUST (DISCOVERY POLICY): The consumer MUST derive all tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-FUMA-003** MUST (LOCK-VERSION GROUNDING): Before writing code that uses a versioned library, execute in order: find dependency manifest, identify build tool, inspect repository lock or resolution artifact to determine exact resolved version, look up official documentation/changelog for that exact version, confirm every API/class/function exists in that version, and re-run steps 3-5 per dependency at point of use for version-sensitive behavior.

### Verify

```bash
# Discover and execute the repository type-checking script to verify interface compatibility
# Discover and execute the repository static analysis suite to verify absence of disallowed custom layout wrappers
# Discover and execute the repository build script to confirm successful compilation of all route layout boundaries
```

**Accept when:**
- Documentation route layouts successfully render navigation, sidebars, and body content using fumadocs-ui layout components without layout structural errors.
- All layout components resolve their configuration and source definitions through the standardized shared application configuration contract.
- The repository static verification suite passes without module resolution or layout contract violations.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated static analysis, continuous integration type-checking, automated build verification, and peer review verification enforce these rules. Violation handling: Pull request checks fail when route layout boundaries implement redundant custom navigation chrome instead of fumadocs-ui layout components, and must be remediated by refactoring layout boundaries to consume standardized primitives and shared configuration.
</enforcement>