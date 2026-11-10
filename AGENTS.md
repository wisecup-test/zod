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
| `packages/docs/app/blog/**` + `packages/docs/app/og.png/**` + `packages/docs/components/**` + `packages/docs/loaders/**` + `packages/docs/pages/api/**`<br>`packages/bench/**` + `packages/integration/fixtures/**` + `packages/resolution/src/**` + `packages/treeshake/**` + `play.ts`<br>`packages/docs/**` + `packages/resolution/**` + `packages/zod/**` + `scripts/**` + `vitest.config.ts`<br>`scripts/**` + `vitest.compile.config.ts` + `vitest.config.ts` + `vitest.root.mjs`<br>`packages/resolution/**` + `scripts/**` + `vitest.config.ts` + `vitest.root.mjs`<br>`packages/integration/fixtures/ai-sdk/**` + `packages/integration/fixtures/drizzle-zod/**` + `packages/integration/fixtures/internal-types/**`<br>`packages/docs/app/**` + `packages/docs/components/**` + `packages/docs/loaders/**`<br>`packages/bench/**` + `packages/resolution/src/**` + `packages/treeshake/**`<br>`packages/docs/app/llms-full.txt/**` + `packages/docs/loaders/**`<br>`packages/docs/app/blog/**` + `packages/docs/components/**`<br>`packages/zod/src/mini/**` + `packages/zod/src/v4-mini/**`<br>`packages/docs/components/**` + `packages/docs/loaders/**`<br>`packages/docs/app/**` + `packages/docs/components/**`<br>`packages/zod/src/v3/**` + `packages/zod/src/v4/**`<br>`packages/tsc/bench/**` + `packages/tsc/bisect.ts`<br>`.claude/skills/triage/scripts/**` + `scripts/**`<br>`packages/tsc/**` + `scripts/**`<br>`play.ts` + `scripts/**`<br>`packages/integration/fixtures/internal-types/**`<br>`packages/integration/fixtures/drizzle-zod/**`<br>`packages/docs/app/llms-full.txt/**`<br>`packages/zod/src/v3/benchmarks/**`<br>`packages/zod/src/v4/locales/**`<br>`packages/zod/src/v4/core/**`<br>`packages/docs/components/**`<br>`packages/resolution/src/**`<br>`packages/docs/loaders/**`<br>`packages/zod/src/v3/**`<br>`packages/zod/src/v4/**`<br>`packages/treeshake/**`<br>`packages/tsc/bench/**`<br>`packages/docs/app/**`<br>`packages/zod/src/**`<br>`packages/bench/**`<br>`packages/docs/**`<br>`packages/mini/**`<br>`packages/zod/**`<br>`scripts/**`<br>`**` | `cross-cutting-` _(432 ADRs)_ |
<!-- actual-ai:adr-governance:end -->

# AGENTS.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

Use Nub exclusively for dependency management, scripts, and TypeScript execution. The root `package.json` declares the workspaces and pins Nub; `.nvmrc` selects Node. Nub reads and writes the existing `pnpm-lock.yaml` without requiring pnpm.

Run scripts with `nub run`, repository TypeScript with `nub <file>`, and installed tools with `nub exec --node <tool>`. Keep third-party tools and built-package compatibility probes on plain Node; Nub's augmentation must not mask resolution errors or change test behavior. Use `nub install --frozen-lockfile` for reproducible installs and `nub add` / `nub remove` to manage dependencies.

Key commands:

- `nub run build` - Build all packages (runs recursive build command)
- `nub exec --node vitest run` - Run all tests with Vitest. Includes the compile-mode project, which re-runs the zod tests with global AOT compilation enabled (see `wiki/compile.md`).
- `nub exec --node vitest run <path>` - Run specific test file (e.g., `packages/zod/src/v4/classic/tests/string.test.ts`)
- `nub exec --node vitest run <path> -t "<pattern>"` - Run specific test(s) within a file (e.g., `-t "MAC"`)
- `nub exec --node vitest run --update` - Update all test snapshots
- `nub exec --node vitest run <path> --update` - Update snapshots for specific test file
- `nub run test:watch` - Run tests in watch mode
- `nub exec --node vitest run --coverage` - Run tests with coverage report
- `nub run test:compile` - Focused alias for just the compile-mode project. Already covered by `nub run test`; use this when iterating on compile-related changes.
- `nub run dev` - Execute TypeScript with Nub under source conditions
- `nub run dev <file>` - Execute `<file>` with Nub & proper resolution conditions. Usually use for `play.ts`.
- `nub run dev:play` - Quick alias to run play.ts for experimentation
- `nub run check:comments` - Fail on stacked `//` comment lines (`--fix` joins them)
- `nub run lint` - Run biome linter with auto-fix
- `nub run format` - Format code with biome
- `nub run fix` - Run both format and lint

## Rules

- Nub v0.8.3 and Node.js v24+ required; Nub provisions Node from `.nvmrc`
- ES modules are used throughout (`"type": "module"`)
- All tests must be written in TypeScript - never use JavaScript
- Use `play.ts` for quick experimentation; use proper tests for all permanent test cases
- Features without tests are incomplete - every new feature or bug fix needs test coverage
- Don't skip tests due to type issues - fix the types instead
- Test both success and failure cases with edge cases
- Keep added tests as minimal and dense as possible without sacrificing comprehensiveness; avoid redundant assertions or broad fixtures when a focused case proves the behavior.
- No log statements (`console.log`, `debugger`) in tests or production code
- Never stack prose across consecutive `//` lines. Lines have no maximum width here — the editor wraps for display — so a paragraph split across several `//` lines is just a hard-wrapped line, and hard wrapping breaks search, diffs and editing. Write one long `//` instead. `nub run check:comments` enforces this in pre-commit and CI; `--fix` joins the offenders. Commented-out code, `@ts-`/`@__NO_SIDE_EFFECTS__`-style pragmas, bullet lists, and blocks separated by a bare `//` are exempt. When two adjacent comments describe two different statements, separate them with a blank line rather than joining them.
- Keep comments SHORT AND TIGHT — one lowercase sentence fragment, one clause, no trailing period. Never a capitalized full sentence, and never two of them. Extreme concision: say only what the code cannot say, and cut the setup sentence, the recap, and the same point restated in different words; a comment that needs three sentences usually means the code should be clearer. Identifiers keep their real casing (`Error`, `parse()`), only the prose is lowercase.
- Ask before generating new files
- Use `util.defineLazy()` for computed properties to avoid circular dependencies
- Never branch on specific schema types in shared code. No `def.type === "optional"` conditionals, no hardcoded lists of wrapper type names, no walks up the wrapper chain hunting for a particular type. Every schema type added later silently falls through such a check, and the list is wrong the moment someone writes a new wrapper. When a shared path needs to know something about a schema, express it as a structural property on the internals — `optin`/`optout`, `values`, `pattern`, `propValues` — and let each type declare its own answer. This is not negotiable in the parse paths; a PR that adds edge-case conditional logic keyed on schema types will be rejected regardless of how well it is tested.
- Performance is critical - parameter reassignment is allowed for optimization
- Any change to `packages/zod/src` must be weighed on **all three axes: runtime performance, memory consumption, and bundle size** — see "The three axes" below. A change that improves one and is only checked on that one is not finished.
- ALWAYS use the `gh` CLI to fetch GitHub information (issues, PRs, etc.) instead of relying on web search or assumptions
- Keep JSDoc as minimal as possible. A self-explanatory type or symbol name needs no doc comment. When a comment is genuinely required, write one short sentence describing behavior — not history, rationale, or examples. Don't add interface-level JSDoc that just restates the interface name.
- When you've modified a PR (or opened/closed/commented on one), include the PR URL liberally in summary messages — at minimum once at the end of any reply that touched it
- When creating a PR, do not include a separate test plan section in the body. Link to any relevant issues under discussion, and use the same copywriting guidelines from "Commenting on issues and PRs": concise maintainer voice, prose over templates, and validation details only when they are material to the reader.
- Format validators (`z.iso.*`, `z.email()`, `z.url()`, `z.uuid()`, …) are deliberately narrower than the specs they're named after. "The spec allows X" is not a reason to accept X — see "Format validators: spec compliance is not the bar" below.
- NEVER bump the version in `packages/zod/package.json` (or any package's `package.json`), and NEVER run `gh workflow run release.yml`. Publishing is a maintainer-only dispatch behind an approval. If a version bump is genuinely needed, ask first.

## The three axes

Zod is judged on **runtime performance**, **memory consumption**, and **bundle size** at once, and they trade against each other constantly. Optimizing one in isolation is how regressions land: a change that buys bundle bytes can cost construction speed, and one that saves memory can cost both. Any non-trivial change to `packages/zod/src` — and any change to `core/` at all, since every build ships it — needs a number on all three before it is done. Report them together, including the ones that got worse.

`zod/mini` deserves its own line on the bundle axis: it is sold on size, so a fixed cost lands very differently there (~200 B is 6% of the smallest mini bundle and 1% of classic's).

| axis    | how to measure                                                                                                                                    |
| ------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| runtime | `packages/bench/*.ts` via `nub run bench <name>`, plus construction cost — parse and construction move independently                                 |
| memory  | `packages/bench/memory/schema-footprint.ts` and `realworld.ts` (retained bytes per schema; run under `--expose-gc`)                               |
| bundle  | bundle a `packages/treeshake` fixture with esbuild `--minify` under `--conditions=@zod/source` and gzip it, for both a classic and a mini fixture |

### Benchmarking traps

These produced hours of wrong conclusions; check them before believing a number.

- **Check `uptime` first.** A loaded machine invents effects of ±16%. Numbers taken above a load average of ~8 are worthless.
- **Interleave the two revisions.** Running all of A then all of B puts any drift entirely on whichever ran second. Alternating round-by-round took per-side spread from 2.5x to 4%.
- **Loading two zod revisions into one process makes call sites polymorphic.** It is fine for comparing construction, unreliable for tight leaf parses.
- **Allocating benchmarks can't be timed by a fixed-duration loop.** `z.array().parse()` allocates per call, so a time-boxed harness samples whatever the collector is doing — it gave +8.2% and −17.3% on consecutive identical runs. Use a fixed iteration count with `gc()` between samples and take the minimum.
- **Make sure the work isn't optimized away.** If a micro-benchmark reports ~1e9 ops/sec, V8 eliminated the loop; consume the result.

### Property placement, specifically

Most of the memory in a schema is its own-property count, not its closures. V8 sizes an instance's backing store in steps and `$constructor` assigns nothing itself, so instances get no in-object slots: **≤12 own properties cost 128 bytes, 13–20 cost 848, ≥21 cost 1616** (`packages/bench/memory/prop-slack.ts` measures this). Members therefore live on the prototype and materialize per instance on first read.

If you touch that machinery, three things bite:

- **Moving a property between definition sites changes its descriptor**, and writability/enumerability/configurability are part of the public contract. `packages/bench/memory/` has a surface-diff approach for this: dump every descriptor, alias and assign/delete semantic on both revisions and diff them. It caught four real regressions that tests did not.
- **Redefining an accessor demotes the object to dictionary mode**, which cost 2x on `z.object().parse` once. Run `packages/bench/memory/dict-mode.ts` after any change here — every instance must report `fast`.
- **A bound function pays a call-time trampoline.** Fine for cold builder methods, measurably not fine on the parse path.

## Format validators: spec compliance is not the bar

Zod's format validators — `z.iso.*`, `z.email()`, `z.url()`, `z.uuid()`, and the rest — are named after specs but do not implement them. Each one matches the profile that real producers emit and real consumers accept, which is almost always far narrower than what the grammar permits. That narrowness is the product, not a gap in it.

So **"the spec allows X, therefore Zod must accept X" is not an argument**, and a PR that widens a format regex on that basis alone will be closed. The question is never what the spec permits; it's whether accepting the wider form helps more people than rejecting it hurts. A form that shows up in real payloads and breaks real integrations is worth fixing. A form that only appears when someone reads the grammar and constructs a string from it is not — when one of those reaches a validator in production it's a bug or an attack, and rejecting it is the useful behavior.

Three things make a widening request an automatic no:

- **The spec permits the form only "by mutual agreement" of the two parties.** A general-purpose validator is never party to that agreement, so it can't honor the clause. ISO 8601 expanded years (`+010000-01-01T00:00:00.000Z`) are the canonical case: the standard also requires the parties to agree the digit count, and runtimes disagree — JavaScript emits six digits, Java's `Instant` emits five, Python rejects both. Declined in #6154.
- **The wider form breaks the JSON Schema output.** `z.iso.datetime()` and `z.iso.date()` emit `format: "date-time"` and `format: "date"`, which mean RFC 3339 — four-digit years, no sign. Widening those regexes makes `z.toJSONSchema()` emit a pattern that conformant consumers reject.
- **The cost lands on everyone.** These regexes live in `core/regexes.ts`, so every added alternation is bytes in every bundle including `zod/mini`, plus more backtracking on a hot parse path. Weigh it on all three axes above before you argue for it at all.

For calibration on how narrow these already are: `z.iso.datetime()` rejects basic format (`20200101T061500Z`), week dates (`2020-W01-1`), ordinal dates (`2020-001`), comma decimal separators, and `24:00`. Every one of those is valid ISO 8601. None of them are going in either.

Point anyone who genuinely needs a wider format at `z.string().regex()` or `z.string().refine()`. That escape hatch is the answer, not a wider default.

## Triaging issues and PRs

Follow the `triage` skill at [`.claude/skills/triage/SKILL.md`](.claude/skills/triage/SKILL.md) whenever you're asked to investigate, triage, or form an opinion on an issue or PR. It is the single source of truth for the procedure. Claude and Codex both auto-discover it (Codex via the `.codex/skills` symlink); read it directly if your agent doesn't.

For a draft **security advisory** — a GHSA id, the Security tab, a private vulnerability report — use the `security-advisory` skill at [`.claude/skills/security-advisory/SKILL.md`](.claude/skills/security-advisory/SKILL.md) instead. It shares the conventions above but reorders the work: the fix lands on `main` before any reporter comment is drafted, since the comment's whole value is the PR it links to.

Write-ups live in the gitignored `.triage/` tree — one directory per ticket, `.triage/issues/NNNN/results.md` and `.triage/prs/NNNN/results.md`, with scratch files and repros alongside. When investigating a PR from its worktree, resolve the root repo first (`git worktree list | head -1`) and write results back there; a relative write lands in the worktree's own ignored `.triage/` where nobody will find it.

## Iterating on a contributor PR in a worktree

When asked to make changes on top of an open PR (e.g. as a maintainer review suggestion), use a worktree so `main` stays clean:

```bash
# 1. Fetch the PR as a local branch and create a worktree for it
git fetch origin pull/<N>/head:pr-<N>
git worktree add ~/.cursor/worktrees/zod/pr-<N> pr-<N>
cd ~/.cursor/worktrees/zod/pr-<N>
nub install --frozen-lockfile   # fast, Nub's store is shared across worktrees

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

- Do NOT use `gh pr checkout --detach` for this — it moves your _current_ working tree into detached HEAD instead of creating a worktree.
- Husky pre-commit runs biome format/lint via lint-staged; pre-push runs the full vitest suite. Both are fast and act as a safety net — don't bypass with `--no-verify` unless you have a specific reason.
- **Preserve contributor commits.** Never `git reset --hard` or otherwise rewrite history that erases the contributor's work, even if you're rewriting the actual change. They need to stay in the PR's commit list to get credit on the merged PR. If their approach was wrong, add a `Revert "..."` commit (or just a plain commit that undoes those lines) and then add your replacement commit on top. Force-pushing a single clobbering commit strips them from the GitHub contributors graph.
- When done, clean up: `git worktree remove ~/.cursor/worktrees/zod/pr-<N>` and `git branch -D pr-<N>` (and optionally `git remote remove <contributor>`).

## Commenting on issues and PRs

When posting on a maintainer's behalf via `gh` (PR comments, issue comments, reviews), match the house tone. Load the `prose-writing` skill before you write any of it — it is the general copy guide, and this section layers on top of it. The register is authoritative and friendly — concise, not bubbly, not over-explaining, not effusive. Comments come from a maintainer handing down decisions, not negotiating them. Friendly does not mean deferential.

- Exclamation points are fine in moderation, especially to soften a decline or close out a thread ("Thanks for looking into this!"). Don't stack them and don't sprinkle them through technical writeups.
- Skip effusive praise: "Great work", "Awesome", "Thanks so much for this", "Thanks for the careful writeup", "you clearly read the RFC". A short flat-affect affirmation walks the line well — "Good investigation." or "Solid catch." with a period, no exclamation, no superlatives. Warmth otherwise comes from a short closer ("Thanks for looking into this, though 👍"), not a preamble that butters up the contributor before the decision.
- No "PTAL", "WDYT", or sign-off flourishes asking the contributor to re-review changes the maintainer pushed on top. State what changed and the merge intent. ("LGTM" is fine as a literal verdict at the end of a substantive review, not as a sign-off.)
- When the user gives you exact wording for a comment, use it verbatim (fixing only obvious typos). Do not "improve" their phrasing to match this style guide — their direct instruction wins.
- Lead with the decision or action: "Going to merge as-is." "Closing this out." "I'd be open to a top-level utility but not as a method." Then the reasoning.
- First person, owned opinions. "I don't think this should be a method." "I'm hesitant to add this." Don't hide behind passive voice or "we could perhaps consider".
- Speak with authority. No hedging ("maybe", "I think perhaps", "if that's okay"), no apologizing for decisions, no asking permission to land changes the maintainer has already made. Decisions are stated as decisions.
- Be direct when declining, but not curt. "out of scope", "behaving as intended", "this is more complicated than it looks" — firm, with a concrete reason. A friendly closer ("thanks for looking into this") is fine.
- Cross-reference by number: `#4433`, `commit 2f8414bc`, `merged in #5718`. Concrete and verifiable.
- Length matches substance, and substance is almost never as much as you think. Two or three sentences closes most threads. How long you spent investigating has nothing to do with how long the reply should be — a week of benchmarking still closes in three sentences. The `triage` skill works this through against a real decline.
- No file paths, line numbers, or symbol names unless the reader has to open that file. They turn a two-line decision into a report, and nobody asked you to show your work. Say what the code does instead — "the parse context is per-call state now", not "`core/memoizer.ts:133` writes onto the context". The detail belongs in the `.triage/` write-up.
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
