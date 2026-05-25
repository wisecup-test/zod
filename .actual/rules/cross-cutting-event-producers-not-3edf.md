# Adopt Event-Driven Integration Pattern for API Boundaries: Event Producers Not

These rules are ALWAYS ACTIVE for all API integration implementations and boundary definitions within the system, particularly in TypeScript modules, compiler tooling infrastructure, and any asynchronous operations that span multiple execution contexts or independently deployable components.

### Rules

- **R-EVT-001** MUST: Event producers MUST NOT have direct dependencies on event consumer implementations.

### Verify

```bash
# Detect event-driven patterns in API boundary code
grep -r "addEventListener\|EventEmitter\|on(\|emit(" packages/tsc --include="*.ts" | wc -l

# Verify async/await patterns in critical integration modules
grep -r "async.*await\|Promise<" packages/tsc/bisect.ts packages/tsc/bench/index.ts

# Find event-driven infrastructure definitions
find . -name "*.ts" -exec grep -l "event.*driven\|EventBus\|MessageBroker" {} \;

# Scan for synchronous cross-boundary calls that violate the pattern
grep -r "new.*Consumer\|import.*Consumer" packages/tsc --include="*.ts" | grep -v "EventConsumer\|MessageConsumer"
```

**Accept when:**
- Event-driven patterns are detected in API boundary code with grep commands returning matches in integration modules
- Code review confirms no direct synchronous dependencies between independently deployable components
- Event schema definitions exist with version identifiers and backward compatibility documentation
- Integration tests demonstrate idempotent event handling and proper retry behavior
- Static analysis confirms producers do not import or instantiate consumer implementations

<enforcement>
Claude Code MUST NOT skip or defer verification. All new API integration implementations and boundary definitions must pass the verify commands and accept criteria before approval. Violations detected in CI/CD must block merge until remediated or approved exception is granted.
</enforcement>