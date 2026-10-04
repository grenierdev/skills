---
name: plan-workflow
description: "Set up a project's agent-driven development workflow by creating a project-specific AGENTS.md, plans/README.md, a source vision, and small numbered implementation plans with statuses and dependencies. Use when a user asks to replicate this planning setup in another project or bootstrap a repository's agent instructions and implementation roadmap."
---

# Set Up a Project Plan Workflow

Create the documentation that lets a fresh agent work through a project in small, verifiable steps. The deliverable is a project-specific
`AGENTS.md` and a coordinated `plans/*.md` set. Carry the structure and workflow into the target repository, adapting architecture, tooling,
commands, and domain rules to that project.

This skill sets up the workflow. Creating the setup does not implement its plans; subsequent agents follow the generated `AGENTS.md` and
plan documents when the user requests execution.

## Output contract

Create or reconcile these files in the target project:

```text
AGENTS.md
plans/
  README.md
  000_the_big_picture.md
  001_descriptive_step.md
  002_next_step.md
  ...
```

- `AGENTS.md`: persistent project decisions and agent execution rules.
- `plans/README.md`: the coordination index, dependencies, statuses, shared boundaries, and live starting point.
- `plans/000_the_big_picture.md`: the user's product vision, target architecture, priorities, and exclusions. It is a source document, not
  an executable dependency. If a maintained vision already exists, preserve it and make this file a concise linked summary.
- Numbered plans: small implementation steps, each executable alone after its dependencies complete or as part of an authorized workflow.

The number of plans follows the work; the filenames above are examples. Keep IDs stable in existing projects and use suffixes such as `006a`
for inserted prerequisites rather than renumbering completed history.

## Establish the target and evidence

1. Use the repository requested by the user, or the current repository when no other target is specified. Inspect that repository's
   applicable `AGENTS.md`, root `README.md`, existing `plans/*.md`, task/build/compiler configuration, tests, important code, and linked
   dependency APIs where relevant. Review Git status and relevant diffs when the target is a Git repository.
2. Extract the product goal and requested remaining work from the user and current documentation. Distinguish implemented behavior, explicit
   requirements, historical assumptions, and proposed defaults. Do not assume a README fully describes the desired product.
3. Discover project-specific commands, component boundaries, test harnesses, ID conventions, trust rules, and migration requirements from
   live files. Do not copy Deno, Cloudflare, Auth Dance, Durable Channel, KSUID prefixes, or disposable-schema policies into another project
   unless its own requirements support them. Do not require access to the original grenier.ai checkout to use this skill.
4. Ask for a missing product objective or consequential unresolved decision when evidence cannot supply it. Continue independent inspection
   and documentation preparation while waiting. Record optional decisions as open questions instead of inventing features or presenting
   suggestions as requirements.
5. Preserve existing instructions, useful plans, completed history, and unrelated local edits. Merge the setup into existing documents
   rather than replacing established project policy wholesale. Current user instructions take precedence over older project documents.

## Generate the setup

Use the bundled templates as the output structure. Replace every placeholder with grounded project content, remove inapplicable optional
sections, and verify paths and commands. Do not create empty examples or generic numbered plans for features the user did not request.

### 1. Write the source vision

Use [the vision template](assets/vision-template.md). Capture the product purpose, intended users, requested experience, technology choices,
architecture and data ownership, immediate priorities, explicit exclusions, and unresolved decisions where relevant. Link maintained
requirements rather than copying long source documents. Treat unconfirmed defaults as proposals.

### 2. Create the project instructions

Use [the AGENTS.md template](assets/agents-template.md). Keep the reference project's organizing sections: project/source of truth,
scope/workflow, authentication/trust, IDs/migrations, architecture boundaries, integration testing, and build/validation. Populate domain
sections only where applicable; omit unsupported constraints instead of guessing.

The generated instructions must make these workflow rules concrete:

- Read the plan index and selected plan before implementation; compare the recorded baseline with live code and prerequisite changes.
- Implement only the requested scope. A single-plan request stops at that plan; an explicitly requested workflow may continue through its
  selected plans in dependency order, one validated checkpoint at a time.
- Keep plan statuses and dependencies synchronized with the index. `DONE` prerequisites and necessary live contracts establish readiness;
  numeric order alone does not. Resume partial work without redoing finished plans.
- Treat the file list as intended scope. Include and explain narrow harness, binding, type, export, or task prerequisites; put substantial
  prerequisites into separate plans. Preserve unrelated local changes.
- Diagnose relevant failures until required checks pass or a concrete blocker/product decision remains. There is no arbitrary retry cap.
- Mark `DONE` only after required checks pass, record results and limitations, and refresh the index's current starting point.
- Keep every file under `plans/` below 300 lines. Use linked shared documentation or split substantial steps to stay within that limit.
- Build and test locally. Implementation requests alone do not authorize deployment, pushing, or remote migrations.

Record actual formatting, build, compiler, generated-type, and test commands. Explain the permitted test interfaces and fixture boundaries
for this project. Keep current progress in the index so `AGENTS.md` does not acquire a stale hardcoded "next plan" claim.

### 3. Decompose the implementation work

Use [the plan template](assets/plan-template.md) for each step. Preserve these core headings: `Goal`, `Starting point`, `Files`, `Change`,
`Verify`, and `Finish`. Include `IDs` when relevant. Put `Status`, `Depends on`, and `Planned at` near the top. Append an implementation
result after execution, not while merely planning future work.

Each plan should deliver one coherent result with bounded files and meaningful acceptance checks. Include the context a fresh agent needs:
existing behavior, prerequisite contracts, exact changes, inputs/outputs, important invariants, exclusions, and runnable check commands.
Link shared project rules to avoid repeating them at length. Do not reference unknown paths or invent test/build tasks.

Declare actual dependencies as a directed acyclic graph. A standalone plan assumes all its prerequisites are complete; it must not silently
absorb them. For an internal prerequisite with no real caller yet, follow project testing rules: if deferral is allowed, name the later
consumer plan responsible for behavioral coverage and record the obligation in both plans. All checks required now must still pass.

New implementation work starts `TODO`. Represent existing completed work as `DONE` only when implementation and validation evidence support
it. Preserve existing `IN PROGRESS` and `BLOCKED` states, reconciling conflicts from evidence. Record the reason and unblocking condition
for a blocked plan. Do not manufacture historical implementation results or passing checks.

### 4. Write the coordination index

Use [the index template](assets/index-template.md). Link the source vision and `../AGENTS.md`. Create a table with `Plan`, `Result`,
`Needs`, and `Status`, using the actual plan filenames and IDs. Include the shared architectural boundaries, current live starting point,
known defaults/open decisions, working rules, and caller-facing verification policy where relevant.

Define the four statuses: `TODO`, `IN PROGRESS`, `DONE`, and `BLOCKED`. Make status updates apply to both the plan and its index row. A
blocked row carries a short reason; the plan holds detailed evidence. Unfinished future work does not become blocked merely because it
awaits a planned prerequisite.

Include instructions for standalone and workflow execution. For a requested workflow target, select its necessary unfinished dependency
closure unless the user restricts the allowed plan set. Topologically order selected plans, skip `DONE` plans, and use index order to break
readiness ties. Never start a plan whose prerequisites are incomplete. A blocked dependency prevents its dependents; unrelated ready plans
may continue only within the authorized workflow. Do not imply authorization to delegate to other agents.

## Validate and deliver

- Check that `AGENTS.md`, the index, the vision, and every indexed plan exist; links resolve and plan IDs are unique.
- Check each dependency exists, matches the plan/index entries, and introduces no self-reference or cycle. Confirm statuses match and
  `BLOCKED` entries have reasons. Exclude the vision from executable dependency checks.
- Check that every numbered plan has the core sections, a bounded result, a grounded file list, and project-appropriate verification.
- Remove template placeholders and unsupported source-project details. Check all `plans/*.md` files are below 300 lines.
- Use the target repository's documentation formatter and whitespace checks. Do not add a toolchain or run backend tests just to validate
  documentation setup. Preserve unrelated files and review the final scoped diff.
- Report the generated file paths, the ready starting plan or missing prerequisite, and any unresolved product decision. Give a short
  invocation example such as "Implement plan 001" or "Run the workflow through plan 004."