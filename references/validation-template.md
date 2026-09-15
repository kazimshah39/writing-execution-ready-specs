# `validation.md` Template

Use this file to prove coverage and define observable completion.

```markdown
# Validation Matrix: <Specification title>

- **Source specification:** [`plan.md`](./plan.md)
- **Execution index:** [`tasks.md`](./tasks.md)
- **Status:** `Ready`, `Blocked`, or `Passed`

## 1. Quality Gates

| ID | Purpose | Command or procedure | Expected result | Evidence source | When to run |
|---|---|---|---|---|---|
| QG1 | `<targeted tests>` | `<exact command>` | `<observable success>` | `<project path>` | After T01 |
| QG2 | `<full suite>` | `<exact command>` | `<observable success>` | `<project path>` | Final task |

Do not guess a command. Mark an unknown required command as a blocking execution prerequisite.

## 2. Behavioral Scenarios

| ID | Category | Requirement/criterion | Setup | Action | Expected result | Level | Task IDs |
|---|---|---|---|---|---|---|---|
| V01 | Positive | R1 / AC1 | `<setup>` | `<action>` | `<result>` | Unit/Integration/E2E/Manual | T01 |
| V02 | Negative | R1 | `<invalid setup>` | `<action>` | `<safe failure>` | Unit | T01 |

Use applicable categories:

- Positive
- Negative
- Boundary
- Failure
- Recovery
- Regression
- Compatibility
- Migration
- Security
- Performance
- Accessibility
- Manual

Do not create irrelevant scenarios merely to fill every category.

## 3. Requirement Coverage

| Requirement | Acceptance criteria | Design sections | Task IDs | Scenario IDs | Coverage status |
|---|---|---|---|---|---|
| R1 | AC1 | `plan.md` §7 | T01 | V01, V02 | Complete |

Every requirement must have tasks and validation unless it is explicitly blocked.

## 4. File and Artifact Coverage

| File, area, or artifact | Task IDs | Quality gates or scenarios | Expected final state |
|---|---|---|---|
| `<project-relative path>` | T01 | QG1, V01 | `<state>` |

Cover source, tests, fixtures, migrations, configuration, generated outputs, documentation, observability, and cleanup listed in the plan.

## 5. Manual Validation Procedures

### MV1 — `<observable workflow>`

- **Use when:** `<why automation is insufficient>`
- **Preconditions:** `<setup>`
- **Steps:**
  1. `<action>`
  2. `<action>`
- **Expected result:** `<observable behavior>`
- **Evidence to record:** `<safe screenshot, log event, response, or state>`

Write `None` when automation fully covers the acceptance criteria.

## 6. Final Acceptance Checklist

- [ ] Every required task is complete.
- [ ] Every quality gate passes.
- [ ] Every acceptance criterion has a passing scenario.
- [ ] Negative, edge, failure, recovery, regression, migration, security, performance, and accessibility cases pass where applicable.
- [ ] Generated artifacts and migrations are current.
- [ ] Documentation and operational guidance are current.
- [ ] Rollout, observability, and backout requirements are ready.
- [ ] No unresolved blocking question remains.
- [ ] The implemented scope matches the specification.
```

## Validation rules

- State the setup, action, and expected result for every scenario.
- Prefer automated validation, but do not pretend automation exists.
- Manual procedures must be reproducible and observable.
- Preserve requirement and acceptance IDs from `plan.md`.
- The final implementation task must run all applicable quality gates and confirm this checklist.
