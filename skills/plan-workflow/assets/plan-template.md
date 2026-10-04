# {{ID}}: {{Result}}

- Status: TODO
- Depends on: {{Prerequisite IDs, or none}}
- Planned at: {{Commit when available, date}}

## Goal

{{One bounded implementation result and its caller-visible behavior. Implement this step only.}}

## IDs

{{Project ID helper, reuse rules, retry keys, and runtime counter formats relevant to this step. Remove if not applicable.}}

## Starting point

{{Relevant live files, existing behavior, prerequisite contracts, and task/harness configuration.}}

Shared rules: [plan index](README.md) and [agent instructions](../AGENTS.md). {{Link relevant architecture documents.}}

## Files

- `{{Path to create or edit}}`
- `{{Path to existing harness or regression coverage when affected}}`

Also update this plan's status and `plans/README.md`. Include narrow fixture, binding, type, export, or task prerequisites when necessary;
record why. Other feature work is outside this step.

## Change

### 1. {{First concrete change}}

{{Inputs, outputs, validation, permission rules, and important contracts.}}

### 2. {{Next concrete change}}

{{Storage ownership, atomicity, retries, recovery, or integration boundaries when relevant.}}

## Out of scope

{{Later features and decisions excluded from this step. Link the owning later plan where useful.}}

## Verify

- {{Acceptance behavior observed through an actual caller interface.}}
- {{Relevant denial, isolation, concurrency, retry, or recovery case.}}
- {{Existing behavior that must remain covered.}}

{{If approved by project rules: record deferred behavior, why no caller exists, and the named later plan that owns coverage. Add the
obligation to that plan too. Otherwise remove this paragraph.}}

Run these commands. Each must exit 0; every required acceptance check must pass.

```sh
{{Actual affected-component build and compiler commands from live project configuration}}
{{Actual required behavioral/regression test command}}
{{Actual scoped formatting command}}
git diff --check
```

## Finish

- Compare live files and dependency APIs with the starting point before editing. Preserve unrelated local changes.
- Continue focused diagnosis until checks pass or a concrete blocker is identified. Record the blocker and validation evidence.
- {{Plan-specific invariant or unresolved decision that requires stopping.}}
- Mark DONE in this plan and the index only after its required checks pass; record actual results and any deferred coverage.
- Build and test locally. Deployment, pushing, and remote migrations require separate authorization.