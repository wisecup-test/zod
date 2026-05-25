# Adopt Schema-Based Validation with Benchmarking for Integration Patterns: Data Crossing Integration

These rules are ALWAYS ACTIVE for all data crossing integration boundaries including message queues, API endpoints, component interfaces, external system integrations, and event-driven architecture messages.

### Rules

- **R-27-001** MUST: All data crossing integration boundaries (message queues, API endpoints, component interfaces) MUST be validated using schema-based validation.
- **R-27-002** MUST: Schema validation implementations MUST include corresponding performance benchmarks measuring validation overhead.
- **R-27-003** SHOULD: Establish baseline performance benchmarks before implementing validation to measure actual overhead.
- **R-27-004** SHOULD: Create reusable schema libraries for common patterns (datetime, IP addresses, standard objects) to reduce duplication.
- **R-27-005** SHOULD: Integrate validation failures into observability infrastructure for monitoring and alerting.
- **R-27-006** MAY: Provide exception process for performance-critical hot paths where validation overhead exceeds 5% of total execution time (EXC-001).
- **R-27-007** MAY: Support gradual migration for legacy integration points undergoing transition (EXC-002).

### Verify

```bash
# Count schema-based validation usage across codebase
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
- New integration boundaries include schema validation or documented exception with performance analysis

<enforcement>
Claude Code MUST NOT skip or defer verification. CI pipeline MUST fail if new integration boundaries lack schema validation without documented exception. Code review MUST block merge if validation requirements not met. Performance regression testing MUST validate benchmark thresholds.
</enforcement>