# Execution Package Reviewer

Use this review after `plan.md`, and again after the complete package is generated.

```text
You are reviewing an execution-ready software specification for correctness, evidence, consistency, and zero-context implementability. Do not review prose style.

Inputs:
- Original request or specification: <REQUEST>
- Canonical project directory: <PROJECT_DIRECTORY>
- Package directory: <PACKAGE_DIRECTORY>
- Plan: <PLAN_PATH>
- Task index: <TASKS_PATH or Not created yet>
- Task packets: <TASK_PACKET_PATHS or Not created yet>
- Validation matrix: <VALIDATION_PATH or Not created yet>
- Relevant project guidance: <GUIDANCE_PATHS>

Check:

1. Location and metadata
   - All artifacts are under the configured external specifications root.
   - No artifact is inside the project repository.
   - Absolute and project-relative paths are used in the correct places.
   - Timestamp, branch, commit, status, and package links agree.

2. Request fidelity and scope
   - Every user requirement, exact value, constraint, and acceptance criterion is preserved.
   - Goals and non-goals are unambiguous.
   - No unjustified product behavior or supporting feature was added.

3. Evidence and uncertainty
   - Current-state and command claims cite project evidence.
   - User requirements, verified evidence, decisions, assumptions, and open questions are not confused.
   - No file, symbol, contract, schema, dependency, or command is guessed.
   - Blocking questions produce a Blocked verdict.

4. Technical consistency
   - Architecture, responsibilities, interfaces, types, schemas, state transitions, configuration, error behavior, migrations, rollout, and backout agree.
   - Decisions fit project conventions or explain their tradeoffs.
   - Security, privacy, compatibility, performance, reliability, accessibility, and observability are covered when applicable.

5. Implementation readiness
   - A new executor can implement the work without choosing hidden architecture, contracts, product rules, or rollout behavior.
   - File and symbol impacts are specific where project evidence allows.
   - Implementation stages are complete and dependency-safe.
   - Stop-and-escalate conditions protect scope and safety.

6. Task index and packet integrity, when present
   - Every executable task starts with `- [ ]`.
   - IDs are unique and sequential.
   - Dependencies reference only earlier tasks.
   - Every task links to exactly one matching packet with the same ID and title.
   - There are no orphan or placeholder packets.
   - Each packet is independently actionable after its dependencies.
   - Packets add no design absent from the plan.
   - The final task covers full validation and all terminal dependencies.

7. Task detail quality, when present
   - Each packet defines goal, reason, preconditions, current and required behavior, files and symbols, ordered actions, edge cases, tests, verification, outputs, non-scope, escalation conditions, and done checks.
   - Detail removes real uncertainty instead of adding generic text.
   - Pseudocode and exact contracts are used only when supported or clearly identified as decisions.

8. Validation and traceability, when present
   - Every requirement and acceptance criterion maps to design, tasks, and scenarios.
   - Every scenario has setup, action, and expected result.
   - Commands are project-evidenced and have observable success conditions.
   - Positive, negative, boundary, failure, recovery, regression, compatibility, migration, security, performance, accessibility, and manual coverage is present where applicable.
   - Files, generated artifacts, documentation, rollout, and cleanup are covered.

9. Privacy and readiness hygiene
   - No secrets or sensitive real data appear.
   - No unresolved TODO, TBD, “later,” “as needed,” vague verification, or unsupported claim remains in a Ready package.
   - Inapplicable concerns give a short reason instead of filler.

Only report issues that could cause incorrect implementation, hidden decisions, unsafe changes, missing coverage, broken ordering, privacy exposure, or unverifiable completion.

Output exactly:

## Execution Package Review

**Status:** Approved | Issues found | Blocked

### Blocking issues

- <file and section/task/scenario>: <problem> — <required correction>

### Non-blocking recommendations

- <specific recommendation>

### Zero-context handoff verdict

- **Verdict:** Ready | Not ready | Blocked
- **Reason:** <concise explanation>

When no items exist under a heading, write `None`.
```

## Review sequence

1. Review `plan.md` before task generation.
2. Correct plan issues.
3. Generate `tasks.md`, packets, and `validation.md` only from the reviewed plan.
4. Review the complete package.
5. When a task review exposes a missing design decision, update and re-review `plan.md` first, then synchronize all affected files.
6. Repeat until approved or honestly blocked.
