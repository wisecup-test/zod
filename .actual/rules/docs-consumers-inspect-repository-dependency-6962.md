# Lucide React Adoption for UI Iconography: Consumers Inspect Repository Dependency Resolution Lock

These rules are ALWAYS ACTIVE for all documentation interface components, interactive controls, content metadata schemas, and source loader definitions within the workspace.

### Rules

- **R-LUCIDE-001** MUST: Consumers MUST inspect the repository dependency resolution lock artifact to identify the authoritative version of lucide-react and ensure all icon symbol imports align with the resolved version exported interface.
- **R-LUCIDE-002** MUST: Lock-version grounding MUST be executed in order (find manifest, identify build tool, inspect lock artifact for exact resolved version, look up public API docs for that exact version, confirm API existence, and re-verify per dependency at point of use) before writing code that uses a versioned library.
- **R-LUCIDE-003** MUST: All interface icon elements MUST be imported directly from the adopted lucide-react library, and component instances MUST apply consistent size utility classes to maintain typography alignment.
- **R-LUCIDE-004** MUST: All standalone interactive icon buttons MUST include accessible label props or screen-reader text descriptions.

### Verify

```bash
# Discover and run the project static analysis and type-checking scripts
# Discover and run the project linting and validation suites to confirm no forbidden raw inline vector elements or unapproved alternative icon packages are introduced
# Discover and run the project automated test suites to ensure component rendering with icon primitives functions as expected
```

**Accept when:**
- All interface icon elements are imported directly from the adopted lucide-react library without unresolved module errors.
- Static analysis and lint checks pass cleanly with no prohibited inline vector elements or unapproved icon dependencies.
- Component test suites pass without accessibility warnings or rendering defects.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated continuous integration pipeline executing static analysis, type checking, and linting rules, alongside peer code review.
</enforcement>