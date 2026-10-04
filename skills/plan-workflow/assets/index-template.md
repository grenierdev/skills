# {{Project}} plans

Source: [The Big Picture](000_the_big_picture.md). Reconciled with {{Date and relevant live baseline}}. Read
[agent instructions](../AGENTS.md) before implementing a plan.

Each executable plan owns one result, scope, dependencies, and checks. Read this index and the selected plan before implementation. Execute
one plan at a time. Standalone execution stops after that plan; an authorized workflow continues within its selected scope after each
validated checkpoint. Do not implement later features early.

## Order

| Plan                              | Result                         | Needs    | Status |
| --------------------------------- | ------------------------------ | -------- | ------ |
| [001](001_foundation.md)          | {{Foundation result}}          | —        | TODO   |
| [002](002_first_feature.md)       | {{First feature result}}       | 001      | TODO   |
| [003](003_independent_feature.md) | {{Independent feature result}} | 001      | TODO   |
| [004](004_combined_feature.md)    | {{Combined feature result}}    | 002, 003 | TODO   |

Statuses: TODO, IN PROGRESS, DONE, BLOCKED. Keep this table and each plan's status synchronized. Record a short reason for BLOCKED in the
status cell and the plan; record detailed evidence and the unblocking condition in the plan. All prerequisites must be DONE before a plan
starts. Explicit dependencies determine readiness, including independent branches; IDs alone do not.

{{Replace sample rows with links to actual plan files; ensure IDs and dependency lists match those files.}}

## Execution

- Standalone: execute the selected plan only after its prerequisites are DONE; stop after its checks pass or a concrete blocker remains.
- Workflow: select the requested plans and necessary unfinished dependencies unless the user restricts the allowed set. Skip DONE plans,
  execute in dependency order, and complete each plan's checks and documentation checkpoint before continuing.
- Use this table's order to break ties between ready plans. Recheck the live baseline at each step and resume partially implemented work.
- An unfinished dependency prevents its dependents from starting. Continue independent ready plans only within the authorized workflow.
- Append implementation results after execution, and keep current progress here. Completed plans remain historical records.

## Shared boundaries

{{Architecture, ownership, trust boundaries, stable contracts, IDs, and explicit exclusions that apply across plans. Link existing
maintained documents when possible.}}

## Current starting point

{{What is already implemented, important live APIs, relevant dependency checkouts, and current validation evidence. Refresh as plans
complete. Distinguish verified behavior from historical assumptions and deferred coverage.}}

## Working rules

- Keep executable plans below 300 lines. Split substantial prerequisites and update affected dependencies.
- Review live files and scoped diffs before implementation; preserve unrelated local edits.
- Refresh stale baselines and dependency contracts before coding. Completed plans remain historical records.
- Include and explain narrow harness, binding, type, export, or task prerequisites. Keep unrelated features in their own plans.
- Use the project's live build, compiler, formatting, test, and migration configuration. {{Add project-specific rules or links.}}
- Continue focused fixes until required checks pass or a concrete blocker is established. Never mark DONE with failing required checks.
- Update the plan result, both status locations, and this starting point before continuing a workflow.
- Build and test locally. Deployment, pushing, and remote migrations require separate authorization.

## Verification boundaries

{{Project test harness and permitted caller interfaces. State the meaningful observable behavior each test should prove.}}

If project rules allow deferring an internal helper's behavioral checks until a production caller exists, name the owning later plan in both
documents and retain its obligation until fulfilled. Current required static, build, formatting, and regression checks must pass.

{{Optional project-specific migration policy, external references, and unresolved decisions. Remove unused sections and placeholders.}}