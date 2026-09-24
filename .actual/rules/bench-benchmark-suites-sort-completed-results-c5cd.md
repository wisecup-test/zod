# benchmark Event-Driven Lifecycle Integration: Benchmark Suites Sort Completed Results Throughput

These rules are ALWAYS ACTIVE for performance benchmarking suites and execution harnesses within the project.

### Rules

- **R-BENCH-001** SHOULD: Benchmark suites SHOULD sort completed benchmark results by throughput to compute relative performance ratios against the baseline slowest implementation.
- **R-BENCH-002** MANDATORY: The consumer MUST derive all tool names, file names, commands, package managers, and version numbers from the project repository (DISCOVERY POLICY).
- **R-BENCH-003** MANDATORY: Before writing code that uses a versioned library, the consumer MUST execute in order: find dependency manifest, identify build tool, inspect repository lock/resolution artifact, look up official documentation for that exact version, confirm every API/class/function exists in that version's docs, and re-run steps per dependency at point of use (LOCK-VERSION GROUNDING).
- **R-BENCH-004** MANDATORY: Attach cycle listeners solely for minimal progress logging, deferring summary transformations until the complete event fires, ensuring heavy calculation and table formatting occur exclusively within the complete event rather than per-iteration cycle callbacks.

### Verify

```bash
# Discover and run the project benchmark suite script defined in the repository configuration.
# Inspect benchmark execution output to confirm cycle progress and completion tables render without errors.
```

**Accept when:**
- Benchmark suite runs to completion and emits cycle notifications followed by a tabular summary.
- Reported metrics contain throughput, mean duration, and error margin calculations.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration runs execute project benchmark validation tasks, and peer code review verifies benchmark harness additions and event subscriptions.
</enforcement>