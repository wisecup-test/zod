# Adopt Event-Driven Integration Pattern for API Boundaries: Synchronous Request Response

These rules are ALWAYS ACTIVE for all API integration implementations and boundary definitions within the system. All new integration points and API boundaries must comply with the event-driven pattern specified herein.

### Rules

- **R-EDB-001** MAY: Synchronous request-response patterns MAY be used within bounded contexts but not across integration boundaries.

### Verify

```bash
# Detect event-driven patterns in critical infrastructure
grep -r "addEventListener\|EventEmitter\|on(\|emit(" packages/tsc --include="*.ts" | wc -l

# Check for async/await and Promise usage in integration modules
grep -r "async.*await\|Promise<" packages/tsc/bisect.ts packages/tsc/bench/index.ts

# Find event-driven infrastructure definitions
find . -name "*.ts" -exec grep -l "event.*driven\|EventBus\|MessageBroker" {} \;
```

**Accept when:**
- Event-driven patterns are detected in API boundary code with grep commands returning matches in integration modules
- Code review confirms no direct synchronous dependencies between independently deployable components
- Event schema definitions exist with version identifiers and backward compatibility documentation
- Integration tests demonstrate idempotent event handling and proper retry behavior

<enforcement>
Claude Code MUST NOT skip or defer verification. Violations are caught by automated static analysis in CI/CD pipeline scanning for synchronous cross-boundary calls, architecture review for new integration points, code review checklists for event schema versioning, and periodic architecture audits. Pull requests are blocked until architecture review approves integration approach. Exceptions require documented justification and are reviewed quarterly.
</enforcement>