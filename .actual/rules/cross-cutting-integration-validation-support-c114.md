# Adopt Schema-Based Validation with Benchmarking for Integration Patterns: Integration Validation Support

These rules are ALWAYS ACTIVE for all integration boundary code including message queue handlers, API endpoints, inter-component data transfer, and external system integration points.

### Rules

- **R-27-001** SHOULD: Integration validation SHOULD support real-world scenarios including datetime validation, IP address validation, and complex object creation patterns.
- **R-27-002** MUST: Mandatory benchmarking ensures performance is monitored for all schema validation implementations at integration boundaries.
- **R-27-003** SHOULD: Schema validation SHOULD be applied at high-risk integration boundaries (external APIs, message queues) before internal boundaries.
- **R-27-004** SHOULD: Reusable schema libraries SHOULD be created for common patterns (datetime, IP addresses, standard objects) to reduce duplication.
- **R-27-005** MUST: Validation failures MUST be integrated into observability infrastructure for monitoring and alerting.
- **R-27-006** SHOULD: Error messages from validation failures SHOULD be clear and actionable to aid debugging and reduce mean time to resolution.

### Verify

```bash
# Count schema validation usage across codebase
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
- Validation failures are logged and monitored through observability infrastructure
- Clear error messages are provided for all validation failures

<enforcement>
Claude Code MUST NOT skip or defer verification. All integration boundary code MUST include schema-based validation with corresponding benchmarks before merge. Performance regression testing MUST pass. Violations trigger CI pipeline failure and code review block unless documented exception is approved by architecture review board.
</enforcement>