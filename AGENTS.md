<!-- actual-ai:adr-governance:start -->
# Project ADRs

This project's conventions are encoded as ADRs under `.actual/rules/`. **The ADRs ARE the pattern.** Follow them verbatim instead of reading existing implementations to figure out how to do something.

> **Note:** this directive is calibrated for one-shot tasks (a single discrete feature). For multi-task interactive sessions, consult the ADRs for each task transition rather than holding to the per-session caps below.

## Workflow (follow in order)

1. **Identify topic.** Match the files you'll edit against the path-glob table below. Pick the 1-3 topics that match. Do not pre-emptively pick "related" topics; pick only what the file paths actually match.

2. **Select ADRs by filename — the filename is the index.** Run `ls .actual/rules/`. Each filename is `<topic>-<aspect-slug>-<hash>.md`; the `<aspect-slug>` (middle segment) names the ADR's specific concern — e.g., `database-schema-defined`, `zod-input-validation`, `cache-key-format`.

   **Scan ALL filenames first, then pick only the ones whose aspect-slug directly names a noun or verb in your task.** Select by filename; never read a body to decide relevance. **Hard cap: read at most 5 ADR files total.** If more than 5 look relevant, you are over-matching — keep the 5 most specific.

   **If the path-glob table below is a single `**/*` → `cross-cutting-` row** (one big bucket, no per-area topics), this filename scan is your ONLY filter. Do **not** read the bucket exhaustively — treat the filenames as a menu, match aspect-slugs to your task, read ≤5, and ignore the rest. Reading every ADR in the bucket is the exact failure this directive exists to prevent.

3. **Locate insertion points (one read per file, max 3 files).** You may read source files ONLY to (a) find where to add code (which directory, which barrel export to update) or (b) look up an exact identifier you must import. **Do not read source files as pattern examples — the ADRs already encode the pattern.** If you find yourself reading a file because "I want to see how X is done elsewhere," stop. The ADR you already read tells you how.

4. **Implement.** Write the code following the rule statements verbatim. If two ADRs seem to conflict, follow the more specific one (longer topic prefix wins).

5. **Verify after implementing.** Only after the code is written, re-read the `verify_commands` or `accept_criteria` sections of the ADRs you applied and check your work against them. Run the verify commands if any.

## Anti-patterns to avoid

- Reading the first N rules alphabetically because they're cheap. Filter by aspect-slug first, then read only the relevant ones.
- Reading >5 ADR files for a single feature. If you're tempted, you're over-scoping the topic match.
- Reading the entire `cross-cutting-` bucket because "every rule is always active." Selection is by filename (step 2); you apply the ≤5 you selected, not all of them.
- Reading existing similar features to "see the pattern" — the ADRs encode the pattern. Trust them.
- Re-reading the same ADR multiple times. Cache it mentally.
- Continuing to browse the codebase after step 3. By step 4 you should be writing, not reading.

Each rule file at `.actual/rules/<topic>-<aspect>-<hash>.md` contains the full ADR with rule statements, verify commands, and accept criteria.

## Verification Protocol

These rules are ALWAYS ACTIVE. Apply every rule **from the ADRs you selected in step 2** that governs the files you touch — to all code generation, modification, and review. "Always active" does **not** mean read every ADR: you apply the handful you selected by filename, within the read cap above.

Every rule follows a **Verify → Fix → Repeat** loop. After generating or modifying code for any rule you MUST:

1. **RUN** the rule's `### Verify` command(s).
2. **CAPTURE** the full output (stdout + stderr).
3. **EVALUATE** the output against the rule's **Accept when** criteria.
4. **IF FAILING:** diagnose the root cause, apply a fix, and re-run from step 1.
5. **IF PASSING:** keep the passing output as evidence before moving on.
6. **MAX ITERATIONS:** 5 attempts per rule. If still failing after 5 attempts, STOP and report the failure with all captured output.

Compliance is not optional. Do not skip verification, assume correctness, or defer it to a later task. Every change to a governed area must be accompanied by a passing verification run.

## Mandatory Dependency Grounding

Before writing or modifying implementation code that uses an external dependency:

1. Identify every affected external dependency.
2. Locate the repository's manifest and lock or resolution artifact.
3. Determine the exact repository-resolved version from the lock artifact.
4. Verify that the active environment matches that version.
5. Verify each API being introduced or changed against evidence applicable to that exact version (official documentation or public API reference).
6. Produce a dependency-grounding record.
7. Stop if any version, environment, or API cannot be verified.

Do not begin implementation until dependency grounding has passed.

The repository lock or resolution artifact is authoritative. A manifest range or model recollection is not sufficient.

### Integrated workflow

1. Stabilize the workspace.
2. Inspect the task and relevant architecture decisions.
3. Identify affected dependencies.
4. Run dependency grounding.
5. Produce the implementation plan.
6. Implement the change.
7. Validate grounding coverage, build, types, lint, and tests.
8. Report evidence, assumptions, and blockers.

## Path glob → topic

| You're editing | Topic prefix |
|---|---|
| `packages/docs/**` | `docs-` _(50 ADRs)_ |
| `packages/**/*` + `wiki/**/*`<br>`packages/**`<br>`**/*` | `cross-cutting-` _(41 ADRs)_ |
| `packages/zod/src/v4/core/**` | `zod-v4-core-` _(33 ADRs)_ |
| `packages/zod/src/**` | `zod-` _(26 ADRs)_ |
| `packages/bench/**` | `bench-` _(24 ADRs)_ |
| `packages/zod/src/v4/**` | `zod-v4-` _(22 ADRs)_ |
| `packages/docs/components/**` | `docs-components-` _(17 ADRs)_ |
| `packages/docs/loaders/**` | `docs-loaders-` _(14 ADRs)_ |
| `packages/zod/src/v3/**` | `zod-v3-` _(12 ADRs)_ |
| `packages/zod/src/v4/locales/**` | `zod-v4-locales-` _(6 ADRs)_ |
| `packages/zod/src/v4/classic/**` | `zod-v4-classic-` _(6 ADRs)_ |
| `packages/docs/app/**` | `docs-app-` _(6 ADRs)_ |
| `packages/resolution/**` | `resolution-` _(6 ADRs)_ |
| `packages/integration/fixtures/drizzle-zod/**` | `integration-fixtures-drizzle-zod-` _(5 ADRs)_ |
<!-- actual-ai:adr-governance:end -->

# AGENTS.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

The project uses pnpm workspaces. Key commands:

- `pnpm build` - Build all packages (runs recursive build command)
- `pnpm vitest run` - Run all tests with Vitest
- `pnpm vitest run <path>` - Run specific test file (e.g., `packages/zod/src/v4/classic/tests/string.test.ts`)
- `pnpm vitest run <path> -t "<pattern>"` - Run specific test(s) within a file (e.g., `-t "MAC"`)
- `pnpm vitest run --update` - Update all test snapshots
- `pnpm vitest run <path> --update` - Update snapshots for specific test file
- `pnpm test:watch` - Run tests in watch mode
- `pnpm vitest run --coverage` - Run tests with coverage report
- `pnpm dev` - Execute code with tsx under source conditions
- `pnpm dev <file>` - Execute `<file>` with tsx & proper resolution conditions. Usually use for `play.ts`.
- `pnpm dev:play` - Quick alias to run play.ts for experimentation
- `pnpm lint` - Run biome linter with auto-fix
- `pnpm format` - Format code with biome
- `pnpm fix` - Run both format and lint

## Rules

- Node.js v24+ required (use nvm if needed); pnpm v10.12.1
- ES modules are used throughout (`"type": "module"`)
- All tests must be written in TypeScript - never use JavaScript
- Use `play.ts` for quick experimentation; use proper tests for all permanent test cases
- Features without tests are incomplete - every new feature or bug fix needs test coverage
- Don't skip tests due to type issues - fix the types instead
- Test both success and failure cases with edge cases
- Keep added tests as minimal and dense as possible without sacrificing comprehensiveness; avoid redundant assertions or broad fixtures when a focused case proves the behavior.
- No log statements (`console.log`, `debugger`) in tests or production code
- Ask before generating new files
- Use `util.defineLazy()` for computed properties to avoid circular dependencies
- Performance is critical - parameter reassignment is allowed for optimization
- ALWAYS use the `gh` CLI to fetch GitHub information (issues, PRs, etc.) instead of relying on web search or assumptions
- Keep JSDoc as minimal as possible. A self-explanatory type or symbol name needs no doc comment. When a comment is genuinely required, write one short sentence describing behavior — not history, rationale, or examples. Don't add interface-level JSDoc that just restates the interface name.
- When you've modified a PR (or opened/closed/commented on one), include the PR URL liberally in summary messages — at minimum once at the end of any reply that touched it
- When creating a PR, do not include a separate test plan section in the body. Link to any relevant issues under discussion, and use the same copywriting guidelines from "Commenting on issues and PRs": concise maintainer voice, prose over templates, and validation details only when they are material to the reader.
- NEVER bump the version in `packages/zod/package.json` (or any package's `package.json`). A version bump is the only thing that triggers a release; everything else (including direct pushes to `main`) is recoverable until that happens. If a version bump is genuinely needed, ask first.

## Cutting a release

Only do this when the user explicitly asks. Pushing a version bump to `main` triggers `.github/workflows/release.yml`, which publishes to npm + JSR and creates a `v<version>` GitHub release. There is no undo.

Three files must be bumped together — `pnpm check:semver` runs in pre-commit and `prepublishOnly`, and will fail the commit if they disagree:

- `packages/zod/package.json` — `version`
- `packages/zod/jsr.json` — `version`
- `packages/zod/src/v4/core/versions.ts` — `major` / `minor` / `patch`

Procedure:

```bash
# Make sure main is clean and up to date first.
git checkout main && git pull

# Bump all three files to the new x.y.z, then:
git add packages/zod/package.json packages/zod/jsr.json packages/zod/src/v4/core/versions.ts
git commit -m "<x.y.z>"   # commit message is just the version, e.g. "4.4.3"
git push origin main
```

The release workflow only fires on changes under `packages/zod/package.json`, `packages/zod/src/**`, or the workflow file itself, so the bump must include `package.json`. Watch the Actions tab to confirm `build_and_publish` succeeds.

## Iterating on a contributor PR in a worktree

When asked to make changes on top of an open PR (e.g. as a maintainer review suggestion), use a worktree so `main` stays clean:

```bash
# 1. Fetch the PR as a local branch and create a worktree for it
git fetch origin pull/<N>/head:pr-<N>
git worktree add ~/.cursor/worktrees/zod/pr-<N> pr-<N>
cd ~/.cursor/worktrees/zod/pr-<N>
pnpm install --frozen-lockfile   # fast, pnpm store is shared across worktrees

# 2. Look up the PR's head info — you'll need the contributor's fork URL
#    and the head ref name to push back.
gh pr view <N> --repo colinhacks/zod \
  --json headRefName,headRepositoryOwner,maintainerCanModify

# 3. If maintainerCanModify is true, add the fork as a remote and push to
#    the PR's head ref (NOT to your local branch name).
git remote add <contributor> git@github.com:<contributor>/zod.git
git push <contributor> pr-<N>:<headRefName>                 # first push
git push <contributor> pr-<N>:<headRefName> --force-with-lease   # for amends
```

Notes:
- Do NOT use `gh pr checkout --detach` for this — it moves your *current* working tree into detached HEAD instead of creating a worktree.
- Husky pre-commit runs biome format/lint via lint-staged; pre-push runs the full vitest suite. Both are fast and act as a safety net — don't bypass with `--no-verify` unless you have a specific reason.
- **Preserve contributor commits.** Never `git reset --hard` or otherwise rewrite history that erases the contributor's work, even if you're rewriting the actual change. They need to stay in the PR's commit list to get credit on the merged PR. If their approach was wrong, add a `Revert "..."` commit (or just a plain commit that undoes those lines) and then add your replacement commit on top. Force-pushing a single clobbering commit strips them from the GitHub contributors graph.
- When done, clean up: `git worktree remove ~/.cursor/worktrees/zod/pr-<N>` and `git branch -D pr-<N>` (and optionally `git remote remove <contributor>`).

## Commenting on issues and PRs

When posting on a maintainer's behalf via `gh` (PR comments, issue comments, reviews), match the house tone. The register is authoritative and friendly — concise, not bubbly, not over-explaining, not effusive. Comments come from a maintainer handing down decisions, not negotiating them. Friendly does not mean deferential.

- Exclamation points are fine in moderation, especially to soften a decline or close out a thread ("Thanks for looking into this!"). Don't stack them and don't sprinkle them through technical writeups.
- Skip effusive praise: "Great work", "Awesome", "Thanks so much for this", "Thanks for the careful writeup", "you clearly read the RFC". A short flat-affect affirmation walks the line well — "Good investigation." or "Solid catch." with a period, no exclamation, no superlatives. Warmth otherwise comes from a short closer ("Thanks for looking into this, though 👍"), not a preamble that butters up the contributor before the decision.
- No "PTAL", "WDYT", or sign-off flourishes asking the contributor to re-review changes the maintainer pushed on top. State what changed and the merge intent. ("LGTM" is fine as a literal verdict at the end of a substantive review, not as a sign-off.)
- When the user gives you exact wording for a comment, use it verbatim (fixing only obvious typos). Do not "improve" their phrasing to match this style guide — their direct instruction wins.
- Lead with the decision or action: "Going to merge as-is." "Closing this out." "I'd be open to a top-level utility but not as a method." Then the reasoning.
- First person, owned opinions. "I don't think this should be a method." "I'm hesitant to add this." Don't hide behind passive voice or "we could perhaps consider".
- Speak with authority. No hedging ("maybe", "I think perhaps", "if that's okay"), no apologizing for decisions, no asking permission to land changes the maintainer has already made. Decisions are stated as decisions.
- Be direct when declining, but not curt. "out of scope", "behaving as intended", "this is more complicated than it looks" — firm, with a concrete reason. A friendly closer ("thanks for looking into this") is fine.
- Cross-reference by number: `#4433`, `commit 2f8414bc`, `merged in #5718`. Concrete and verifiable.
- Length matches substance. Default to 1–4 sentences. Go long only when the content earns it (root-cause writeups, benchmark results, pointing to a canonical thread).
- Pick the one or two strongest reasons and write them as prose. Resist enumerating every objection in a bullet list — even when each point is fair, it reads as piling on. The strongest argument plus a concrete escape hatch (e.g. "`z.email().max(254)` already does this") is usually enough.
- Don't lift informal or coarse phrasing from external sources (blog posts, issues, comments) into the maintainer voice, even in quotes. Paraphrase the substance — quoted-in-context still reads as the maintainer talking.
- Use prose with inline backticks for symbols. Reach for fenced code blocks only when showing non-trivial code is genuinely clearer than describing it.
- Skip emojis in substantive technical writeups. A small `👍` in a casual closer is good — it keeps a decline or sign-off sounding warm and friendly without leaning on praise.
- Bot mentions are bare imperatives: `@pullfrog review`, `@pullfrog fix merge conflicts`, `@pullfrog re-review fresh.`
- When pushing a follow-up on top of a contributor's PR, state what changed, why it differs from the original approach, and that the maintainer is merging. Never ask the contributor to review the maintainer's changes — they are final, not a proposal. Don't thank them for "letting" the maintainer rewrite their work.
- When posting comments with code samples via `gh`, do NOT pass the body inline through a heredoc that requires escaping backticks. Backslash-escaped backticks (`` \` ``) inside a `$(cat <<'EOF' ... EOF)` body get sent to GitHub literally and break inline code and template literals inside fenced blocks. Instead, write the comment to a file and pass it via `--body-file <path>` (for `gh pr/issue comment`) or `-F body=@<path>` (for `gh api`). This preserves backticks and `${...}` exactly as written.

## Pushing to a new branch (don't accidentally push to main)

When the user asks for a "new PR" or "new branch", the work has to land on a non-`main` ref on the remote. The footgun: `git worktree add <path> -b <branch> origin/main` (and `git checkout -b <branch> origin/main`) silently set the new branch's upstream to `refs/heads/main` because the start point is a remote-tracking ref. A subsequent `git push -u origin <branch>` then pushes to `refs/heads/main`, not to a new remote branch. Two of these in a row have happened.

Avoid by being explicit on the first push:

```bash
# Always use a refspec on the initial push so the remote ref name is unambiguous.
git push -u origin <branch>:refs/heads/<branch>
```

Then verify the output. The line you want to see is:

```
* [new branch]      <branch> -> <branch>
```

If the right-hand side says `main`, the push went to main — abort or revert.

Use `git push origin HEAD:refs/heads/<branch>` for subsequent pushes if you didn't `-u` originally. Don't rely on `git push -u origin <branch>` alone — its behavior depends on the upstream config, which `worktree add -b ... origin/main` set wrong for you.
