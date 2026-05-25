# Adopt Async/Await Pattern for Asynchronous Operations: New Code Not

Status: proposed
Date: 2024-01-20
Deciders: Detection Pipeline (automated)

## Activation

This ADR is ACTIVE for all asynchronous code development and governs the concurrency model used throughout the codebase.

## Context

- The codebase requires handling asynchronous operations for I/O-bound tasks, API calls, and concurrent processing
- Modern JavaScript/TypeScript provides multiple concurrency models including callbacks, promises, and async/await syntax
- Pattern detected across benchmark files (object-async.ts, object-safeasync.ts) and test files (generics.test.ts) with 90.83% confidence
- The async/await pattern has emerged as the dominant approach in 3 analyzed files, indicating a consistent architectural choice
- Team needs a standardized approach to asynchronous programming to ensure code consistency, readability, and maintainability

## Problem Statement

Without a standardized concurrency model, asynchronous code becomes inconsistent across the codebase, leading to mixed patterns (callbacks, promises, async/await), increased cognitive load for developers, difficulty in error handling, and challenges in code review and maintenance. The codebase needs a clear decision on which concurrency paradigm to adopt for all asynchronous operations.

## Decision

1. SHOULD_NOT: New code SHOULD NOT use callback-based patterns or raw Promise constructors unless interfacing with legacy APIs

## Policy Block

- SHOULD_NOT New code SHOULD NOT use callback-based patterns or raw Promise constructors unless interfacing with legacy APIs

In scope:
- All new asynchronous code in TypeScript/JavaScript files
- Benchmark implementations requiring async operations
- Test files that exercise asynchronous functionality
- API client implementations and service layer code
- Database access and I/O operations

Out of scope:
- Synchronous utility functions and pure computations
- Third-party library code that uses different patterns
- Legacy code scheduled for deprecation
- Performance-critical hot paths where Promise overhead is measured and documented as problematic

Exceptions:
- EX-001: Interfacing with legacy callback-based APIs that cannot be easily promisified
- EX-002: Performance benchmarks demonstrate measurable overhead from async/await in critical paths

## Rationale

- Pattern detected with 90.83% confidence across 3 files including benchmark and test code, indicating this is an established architectural choice
- Async/await syntax provides superior readability compared to promise chains and callbacks, making code easier to understand and maintain
- Error handling with try-catch blocks is more intuitive and consistent with synchronous code patterns, reducing bugs
- Modern TypeScript tooling and type inference work exceptionally well with async/await, providing better IDE support and type safety
- The pattern is already in use across critical areas (benchmarks and tests), indicating team familiarity and acceptance

## Consequences

Positive:
- Improved code readability and maintainability through consistent, linear-looking asynchronous code
- Better error handling with familiar try-catch patterns reducing error-prone promise rejection handling
- Enhanced type safety with TypeScript's strong support for async/await and Promise types
- Easier onboarding for new developers familiar with modern JavaScript/TypeScript patterns
- Simplified debugging with clearer stack traces compared to promise chains

Negative:
- Potential performance overhead in extremely tight loops or high-frequency operations due to Promise microtask scheduling
- Risk of unintentional sequential execution when parallel execution would be more efficient (requires explicit Promise.all)
- Learning curve for developers unfamiliar with async/await semantics and common pitfalls
- Existing callback-based or promise-chain code will need refactoring to maintain consistency
- May complicate interoperability with older libraries that expect callback patterns

## Alternatives

- Continue using raw Promises with .then() and .catch() chains (rejected)
  Rejected because: Promise chains lead to nested callback-like structures, reduced readability, and more complex error handling. The detected pattern shows the team has already moved away from this approach.
  When valid: Only when interfacing with legacy code that cannot be easily refactored
- Use callback-based patterns for all asynchronous operations (rejected)
  Rejected because: Callbacks lead to callback hell, poor error handling, and are considered outdated in modern JavaScript/TypeScript. No evidence of this pattern in the analyzed codebase.
  When valid: Never for new code; only when required by third-party APIs
- Mixed approach allowing developers to choose their preferred pattern (rejected)
  Rejected because: Inconsistent patterns increase cognitive load, make code reviews harder, and create maintenance burden. The detected pattern indicates a preference for standardization.
  When valid: Not recommended; consistency is more valuable than individual preference

## Risks

- Developers may accidentally create sequential bottlenecks by awaiting operations that could run in parallel
  Mitigation: Provide training on Promise.all() and Promise.allSettled() patterns; include examples in documentation; flag sequential awaits in code review
  Owner: Engineering team leads
- Performance degradation in high-frequency operations due to Promise overhead
  Mitigation: Establish performance benchmarks for critical paths; allow documented exceptions for proven performance issues; monitor performance metrics
  Owner: Performance engineering team
- Inconsistent error handling leading to unhandled promise rejections
  Mitigation: Enable strict linting rules for unhandled promises; require try-catch blocks in code review; implement global unhandled rejection handlers for monitoring
  Owner: Engineering team and DevOps

## Implementation Notes

- Use ESLint rules such as '@typescript-eslint/promise-function-async' and 'require-await' to enforce async/await patterns
- Configure TypeScript with 'strict' mode to ensure proper Promise type checking and return type declarations
- For parallel operations, use 'await Promise.all([op1(), op2()])' pattern; for error-tolerant parallel operations, use 'Promise.allSettled()'
- When refactoring existing code, start with test files and high-visibility modules to establish patterns before tackling legacy code
- Document any necessary exceptions (legacy API integration) with inline comments explaining the rationale

## Continuation Context


Verify commands:
- grep -r 'async.*function\|async.*=>\|async (' --include='*.ts' --include='*.js' packages/ | wc -l
- eslint --rule '@typescript-eslint/promise-function-async: error' packages/
- npm test -- --grep 'async' --reporter json | jq '.tests[] | select(.title | contains("async"))'

Accept when:
- All new asynchronous functions use async/await syntax with proper type annotations
- ESLint checks pass with no violations of async/await rules in new code
- Code review checklist confirms try-catch error handling around await statements
- Benchmark tests show no performance regressions in async operation handling

## Enforcement

- Verified by: Automated ESLint checks in CI pipeline enforcing async/await rules
- Verified by: TypeScript compiler strict mode checking Promise return types
- Verified by: Code review checklist requiring async/await pattern verification
- Verified by: Pre-commit hooks running linting rules on staged files
- Violation handling: CI pipeline fails on ESLint violations related to async/await patterns
- Violation handling: Code review blocks merge until async/await patterns are corrected
- Violation handling: Automated comments on pull requests highlighting non-compliant code
- Violation handling: Monthly audit reports identifying files with legacy patterns for refactoring prioritization
- Exception process: Developer documents exception rationale in code comments with reference to EX-001 or EX-002
- Exception process: Tech lead or architect reviews and approves exception during code review
- Exception process: Exception is logged in architecture decision log with justification
- Exception process: Exceptions are reviewed quarterly to determine if they can be eliminated through refactoring