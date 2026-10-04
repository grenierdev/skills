# Agent instructions

These instructions capture {{Project}} decisions as of {{Date}}, checked against {{Relevant live repository baseline}}.

## Project and source of truth

- Build {{Product purpose, target users, and established technology choices}}.
- Read [the plan index](plans/README.md) and the selected plan before implementation. Compare the starting point and prerequisite changes
  with live files and relevant dependency APIs.
- Current user instructions take precedence. Use these instructions and the reconciled index over superseded historical plan text.
- Consult the index for current progress. Completed plans are historical implementation records; do not restore obsolete code.
- {{Relevant dependency checkouts/documentation and their edit boundaries, if any.}}

## Scope and workflow

- Implement only the requested plan or explicitly requested workflow, in dependency order. Do not implement later features early.
- Run one plan at a time. Standalone execution stops after its checks pass; workflow execution continues only within its selected scope.
- Every prerequisite must be DONE and its necessary contracts present before the dependent plan begins. For a workflow target, include its
  unfinished prerequisites unless the user restricts the allowed set; use dependency order rather than numeric order.
- Mark the plan IN PROGRESS in its file and the index when implementation starts. Resume partial work from live evidence.
- Treat the file list as intended scope. Include narrow fixture, binding, type, export, or task prerequisites when necessary; explain them.
  Refresh stale baselines and dependency contracts. Put substantial missing prerequisites into separate plans.
- Preserve unrelated local edits. Review Git status and the relevant diff before and after changes when this is a Git repository.
- Continue focused diagnosis until required checks pass or a concrete blocker or unresolved product decision prevents progress. Record the
  evidence and what would unblock it; do not stop after an arbitrary number of attempted fixes.
- Mark DONE only after required checks pass. Update both the plan and [the index](plans/README.md), record implementation results and
  limitations, and refresh the index's current starting point before continuing a workflow.
- Use TODO, IN PROGRESS, DONE, or BLOCKED consistently. A BLOCKED plan and its index row include a short reason; the plan records detail.
  Planned dependencies alone do not make untouched future work BLOCKED. Never execute dependents of an unfinished plan.
- Keep every `plans/*.md` file under 300 lines.
- Build and test locally. Do not deploy, push, or apply remote migrations unless the user explicitly requests it.

## Authentication and trust

- {{Authentication contracts, verified principal source, and guard/access-check responsibilities.}}
- {{Authorization authority, trusted internal boundaries, and forged-input handling.}}
- {{Origin/CORS policy and credential handling, if applicable.}}

## IDs and migrations

- {{Established ID helper, ownership/reuse rules, and prefixes when applicable.}}
- {{Retry-key generation/reuse and runtime counter rules when relevant.}}
- {{Protected migrations, allowed schema changes, compatibility requirements, and local validation/reset policy.}}

## Architecture boundaries

- {{Entrypoints, services/components, and shared-code ownership.}}
- {{Data ownership, partitioning, privacy, and permission authority.}}
- {{Transaction boundaries, projections, recovery/outbox rules, and lifecycle responsibilities where relevant.}}

## Integration testing

- {{Existing test location/harness and required test types from this project's policy.}}
- Exercise real caller interfaces and assert observable behavior, permissions, isolation, retries, and recovery where relevant.
- {{Permitted fixture setup/failure injection and forbidden inspection shortcuts, according to project requirements.}}
- If project rules allow deferring internal helper coverage until its caller exists, name the later owning plan and record the obligation in
  both plans. Do not claim deferred checks passed or weaken current acceptance requirements.
- {{Fixture cleanup and lifecycle requirements where applicable.}}

## Build and validation

- Use live project tasks and compiler/formatter configuration. {{Exact component build, compiler, type-generation, and formatting
  commands.}}
- {{Required behavioral/regression test commands and component/harness registration rules.}}
- {{Generated artifacts and secrets that must remain untracked.}}
- Documentation-only changes require formatting, valid links, plan/status/dependency consistency, line limits, and whitespace checks; they
  do not require an unrelated backend test run. {{Actual documentation formatter and whitespace commands.}}
- Report resulting behavior, validation, narrow extra scope, and remaining limitations or explicitly deferred coverage.