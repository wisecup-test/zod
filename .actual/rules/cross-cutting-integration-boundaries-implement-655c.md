# Adopt Event-Driven Integration Pattern for API Boundaries: Integration Boundaries Implement

These rules are ALWAYS ACTIVE for all API integration implementations and boundary definitions within the system, including all new integration points, cross-service communication patterns, and asynchronous operations that span multiple execution contexts.

### Rules

- **R-EVI-001** SHOULD: Integration boundaries SHOULD implement retry logic with exponential backoff for transient failures.

### Verify

```bash
# Detect event-driven patterns in integration modules
grep -r "addEventListener\|EventEmitter\|on(\|emit(" packages/tsc --include="*.ts" | wc -l

# Verify async/await patterns in critical integration files
grep -r "async.*await\|Promise<" packages/tsc/bisect.ts packages/tsc/bench/index.ts

# Find event-driven infrastructure definitions
find . -name "*.ts" -exec grep -l "event.*driven\|EventBus\|MessageBroker" {} \;
```

**Accept when:**
- Event-driven patterns are detected in API boundary code with grep commands returning matches in integration modules
- Code review confirms no direct synchronous dependencies between independently deployable components
- Event schema definitions exist with version identifiers and backward compatibility documentation
- Integration tests demonstrate idempotent event handling and proper retry behavior
- Retry logic with exponential backoff is implemented for all cross-boundary asynchronous operations

<enforcement>
Claude Code MUST NOT skip or defer verification. All integration boundaries crossing service or module boundaries MUST be reviewed against these rules. Violations discovered in code review or CI/CD analysis MUST be escalated to architecture review unless an approved exception (EXC-001 or EXC-002) applies.
</enforcement>