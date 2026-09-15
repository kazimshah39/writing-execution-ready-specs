# `tasks.md` Execution Index Template

Create this file only after `plan.md` passes its first review.

````markdown
# Execution Index: <Specification title>

- **Source specification:** [`plan.md`](./plan.md)
- **Validation matrix:** [`validation.md`](./validation.md)
- **Canonical project directory:** `<absolute path>`
- **Planning package:** `<absolute path>`
- **Status:** `Not started` or `Blocked`
- **Total tasks:** `<count>`

## Executor Rules

- Read `plan.md` once before starting the first task.
- Complete tasks in dependency order.
- Open the linked task packet before changing project files.
- Do not mark a task complete until all packet checks pass.
- Do not choose a new architecture, contract, dependency, or product behavior during execution.
- Stop and update the specification when a packet's escalation condition occurs.
- Keep the specification, task index, packets, and validation matrix synchronized.

## Dependency Overview

```text
T01
├── T02
│   └── T04
└── T03
    └── T04
```

Use a simple list instead when a graph would add no value.

## Tasks

- [ ] **T01 — <Specific outcome>**
  - **Packet:** [`task-details/T01.md`](./task-details/T01.md)
  - **Goal:** <Observable result produced by this task>
  - **Depends on:** `None` or `<earlier task IDs>`
  - **Files or areas:** `<project-relative paths or precise areas>`
  - **Primary verification:** `<exact evidenced command or procedure>` — <expected result>
  - **Produces:** `<code, schema, behavior, documentation, or other output>`

- [ ] **T02 — <Specific outcome>**
  - **Packet:** [`task-details/T02.md`](./task-details/T02.md)
  - **Goal:** <Observable result>
  - **Depends on:** `T01`
  - **Files or areas:** `<paths or areas>`
  - **Primary verification:** `<check>` — <expected result>
  - **Produces:** `<output>`

## Final Validation Task

The last task must validate the complete deliverable. It must depend on every terminal implementation task and cover all applicable project quality gates, generated artifacts, documentation, migration checks, and acceptance criteria.
````

## Task design rules

- IDs must be unique, sequential, and stable.
- Dependencies may reference only earlier tasks.
- Create one coherent, independently reviewable increment per task.
- Keep implementation and its most relevant tests together when practical.
- Split unrelated responsibilities or different rollback boundaries.
- Do not create trivial tasks for edits that have no independent validation value.
- The index summarizes; the matching task packet contains execution detail.
- Every index task must have exactly one packet with the same ID and title.
