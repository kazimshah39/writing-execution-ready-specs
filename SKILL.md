---
name: writing-execution-ready-specs
description: Creates exhaustive, evidence-backed implementation specifications and standalone task packets for complex software work. Use when a junior developer or limited-context AI agent must implement independently without making hidden design decisions. For ordinary implementation planning, use writing-project-plans instead.
metadata:
  version: "1.0.0"
  category: "development"
  tags: "planning,implementation-specification,zero-context-handoff,task-packets"
---

# Writing Execution-Ready Specifications

Create a zero-context implementation package before changing project code.

This skill is intentionally more detailed than an ordinary implementation plan. Use it when the implementation will be handed to a junior developer, a limited-context AI agent, multiple executors, or anyone who must work without relying on the original conversation.

For routine features, bug fixes, and refactors where a capable implementer can make small local decisions, use `writing-project-plans` instead.

## Required outputs

Create one planning package containing:

```text
<planning-package>/
├── plan.md
├── tasks.md
├── validation.md
└── task-details/
    ├── T01.md
    ├── T02.md
    └── ...
```

- `plan.md`: the complete technical and product source of truth.
- `tasks.md`: the dependency-ordered execution index.
- `task-details/TNN.md`: a standalone execution packet for one task.
- `validation.md`: the test, requirement, and acceptance-criteria matrix.

The number of task-detail files is determined by the work. Do not create placeholder task files.

## Hard boundaries

- Do not implement project changes unless the user separately requests implementation.
- Never write the planning package inside the project repository.
- Always use absolute paths when creating planning-package files.
- Use project-relative paths when describing implementation files.
- Do not invent files, symbols, commands, contracts, schemas, dependencies, or product behavior.
- Do not hide unresolved decisions inside implementation tasks.
- Do not use length as a substitute for useful detail. Every section must reduce implementation uncertainty.
- Do not include secrets, credentials, tokens, private keys, connection strings, sensitive customer data, or private URL parameters.

## Zero-context handoff standard

The package is ready only when an executor who has not seen the original request can:

1. Understand the current and intended behavior.
2. Know exactly which project areas to inspect and change.
3. Follow the work in a safe dependency order.
4. Implement each task without choosing a new architecture or product rule.
5. Handle the important failure and edge cases.
6. Run precise validation and recognize success.
7. Know when to stop and escalate a discovery instead of silently changing scope.

Do not claim zero-context readiness when material open questions remain. Mark the package `Blocked` when unresolved decisions prevent safe implementation.

## Evidence model

Separate facts from decisions and uncertainty:

- **User requirement:** explicitly stated by the user or supplied specification.
- **Verified evidence:** observed in project files, configuration, tests, schemas, history, or documented tooling.
- **Decision:** selected implementation direction with its reason and tradeoffs.
- **Assumption:** a non-blocking belief that must be verified during implementation.
- **Open question:** missing information with an owner, impact, resolution path, and blocking status.

Cite project evidence with project-relative paths and, when useful, symbol names. Do not add noisy citations to obvious prose. Cite the evidence that supports behavior, architecture, commands, contracts, and file-impact claims.

## Required workflow

Follow these phases in order.

### Phase 1: Resolve paths and create the package

Read [references/path-layout.md](references/path-layout.md).

Resolve the project root, canonical project path, global specifications root, collision-safe project directory, and timestamped package directory. Create the package directory and `task-details/` before writing outputs.

### Phase 2: Inspect relevant project evidence

Inspect only the areas needed to design this change, including when relevant:

- Repository instructions and contributor guidance.
- Current entry points, callers, callees, components, types, and schemas.
- Similar implementations that establish conventions.
- Tests, fixtures, mocks, snapshots, and generated artifacts.
- Configuration, environment variables, migrations, deployment, and CI.
- Actual scripts for tests, linting, formatting, type checking, builds, and generation.
- Compatibility boundaries, public interfaces, security controls, logs, and metrics.

When CodeGraph is configured, use it before grep or broad file reading. Start with likely entry points and follow the relevant call and data paths. Do not scan the entire repository merely to make the plan look comprehensive.

Record enough evidence to explain the current state and justify the proposed design.

### Phase 3: Normalize the request

Before designing the solution:

1. Restate the objective as an observable outcome.
2. Preserve every explicit requirement, constraint, exact value, and acceptance criterion.
3. Separate goals from non-goals.
4. Define important terms that could be interpreted differently.
5. Identify assumptions and open questions.
6. Ask the user only about decisions that block a safe design when interaction is possible.
7. Mark non-blocking uncertainty as assumptions with a verification step.

Do not silently resolve product, security, data-retention, compatibility, or rollout decisions that require owner input.

### Phase 4: Write and review `plan.md`

Read [references/plan-template.md](references/plan-template.md), then write `<planning-package>/plan.md`.

The plan must define the current state, intended behavior, requirements, decisions, alternatives, architecture, contracts, workflows, errors, edge cases, security, performance, file and symbol impact, implementation sequence, migration, rollout, testing, and completion conditions when applicable.

Use concise `Not applicable — <reason>` entries rather than generic filler for irrelevant areas.

Review the plan using [references/package-reviewer.md](references/package-reviewer.md). Correct all blocking issues before creating tasks. If the plan remains blocked by a user decision, document the blocker clearly and do not pretend downstream task packets are executable.

### Phase 5: Create the execution index

Read [references/tasks-template.md](references/tasks-template.md), then write `<planning-package>/tasks.md`.

Derive tasks only from the reviewed plan. Each task must:

- Have a stable sequential ID such as `T01`.
- Produce one coherent, reviewable increment.
- Depend only on earlier task IDs.
- Link to its matching `task-details/TNN.md` file.
- State its goal, files or areas, dependencies, and primary verification.
- Avoid adding design decisions that are absent from `plan.md`.

### Phase 6: Write standalone task packets

Read [references/task-detail-template.md](references/task-detail-template.md).

Create exactly one detail file for each task in `tasks.md`. A packet must contain all context needed to execute that task after its listed dependencies are complete. It must include:

- Goal and reason.
- Preconditions and dependencies.
- Relevant verified current behavior.
- Exact required behavior.
- Files, areas, and symbols.
- Ordered implementation steps.
- Contracts, data shapes, pseudocode, or state rules when useful.
- Failure, boundary, concurrency, retry, compatibility, and security cases when relevant.
- Tests to add or update, expressed as setup, action, and expected result.
- Exact verification commands supported by project evidence.
- Expected outputs.
- Explicit non-scope.
- Stop-and-escalate conditions.
- A task-specific done checklist.

A packet may repeat a small amount of plan context intentionally so it remains usable on its own. Do not copy large unrelated sections of the plan.

### Phase 7: Write `validation.md`

Read [references/validation-template.md](references/validation-template.md), then write `<planning-package>/validation.md`.

Map every requirement and acceptance criterion to:

- Relevant design sections.
- Implementing task IDs.
- Positive, negative, edge, failure, recovery, regression, migration, security, performance, or manual scenarios as applicable.
- Exact validation commands or procedures.
- Observable expected results.

Do not guess commands. If a required quality command cannot be established from project evidence, record it as an execution prerequisite and explain how it must be resolved.

### Phase 8: Cross-file review and finish

Review the complete package using [references/package-reviewer.md](references/package-reviewer.md). Use a separate reviewer when available and permitted; otherwise perform the same review yourself.

Correct blocking issues and re-review until approved or explicitly blocked by unresolved owner decisions.

Before reporting completion, verify:

1. `plan.md`, `tasks.md`, and `validation.md` exist in the package.
2. Every task in `tasks.md` has exactly one matching `task-details/TNN.md` file.
3. There are no orphan or placeholder task files.
4. IDs, dependencies, paths, terminology, contracts, and acceptance criteria agree across all files.
5. No planning artifact was created inside the project repository.
6. Implementation has not started.

Report the absolute package path, each main output path, the number of task packets, review status, and any blocking questions. Do not paste the full package unless the user asks.
