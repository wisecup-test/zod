# Adopt Schema-Based Validation with Benchmarking for Integration Patterns: Validation Libraries Provide

These rules are ALWAYS ACTIVE for all integration boundary code including message queue payload validation, API request and response validation, inter-component data transfer validation, external system integration boundaries, and event-driven architecture message validation.

### Rules

- **R-27-001** SHOULD: Validation libraries SHOULD provide multiple implementation variants (mini, classic, core) to support different performance and feature requirements.
- **R-27-002** MUST: Mandatory benchmarking MUST be established for all schema validation implementations to ensure performance overhead is monitored and optimized continuously.
- **R-27-003** MUST: Schema validation MUST be present at all identified integration boundaries (message queues, API endpoints, external system integrations).
- **R-27-004** SHOULD: Each schema definition SHOULD have corresponding performance benchmarks measuring validation overhead.
- **R-27-005** SHOULD: Validation coverage metrics SHOULD demonstrate >90% of integration points have schema-based validation implemented.
- **R-27-006** MUST: New integration boundaries MUST include schema validation or documented exception with performance analysis and justification.
- **R-27-007** SHOULD: Reusable schema libraries SHOULD be created for common patterns (datetime, IP addresses, standard objects) to reduce duplication.
- **R-27-008** SHOULD: Validation failures SHOULD be integrated into observability infrastructure for monitoring and alerting.

### Verify

```bash
# Count schema validation patterns across codebase
grep -r "z\.object\|z\.string\|z\.number\|schema" packages/*/src --include="*.ts" | wc -l

# Find benchmark files with schema/validation references
find . -name "*benchmark*.ts" -o -name "*bench*.ts" | xargs grep -l "schema\|validation" | wc -l

# Verify message queue boundary validation patterns
grep -r "boundaries\.message_queues" . --include="*.ts" | wc -l
```

**Accept when:**
- Schema validation is present at all identified integration boundaries (message queues, API endpoints)
- Each schema definition has corresponding performance benchmarks measuring validation overhead
- Validation coverage metrics show >90% of integration points have schema-based validation implemented
- New integration points include schema definitions or documented exceptions with performance justification
- Performance regression testing validates benchmark thresholds in CI pipeline

<enforcement>
Claude Code MUST NOT skip or defer verification. CI pipeline MUST fail if new integration boundaries lack schema validation without documented exception. Code review MUST block merge if validation requirements not met. Performance regression alerts MUST trigger investigation if validation overhead exceeds thresholds. Exceptions MUST be submitted to architecture review board with performance analysis and tracked in technical debt register.
</enforcement>