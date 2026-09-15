# Standalone Task Packet Template

Create one file named `task-details/TNN.md` for every task in `tasks.md`.

```markdown
# TNN — <Exact task title>

## Task Metadata

- **Status:** `Not started`
- **Plan sections:** `<authorizing plan sections>`
- **Validation scenarios:** `<V IDs>`
- **Depends on:** `None` or `<earlier task IDs>`
- **Blocks:** `<later task IDs or None>`
- **Estimated scope:** `Small`, `Medium`, or `Large` based on repository impact, not time promises

## 1. Goal

State the single observable result this task must produce.

## 2. Why This Task Exists

Explain its role in the full change and why it occurs at this point in the dependency order.

## 3. Preconditions

- `<completed dependency or confirmed decision>`

List required environment, access, schema state, generated artifacts, or owner decisions. Do not list ordinary developer setup unless it is material.

## 4. Verified Current Behavior

Describe only the current behavior relevant to this task. Cite project-relative files and symbols.

## 5. Required Behavior

Define exact positive behavior, negative behavior, inputs, outputs, side effects, state changes, compatibility expectations, and user-visible results.

## 6. Files, Areas, and Symbols

| Path or area | Change | Symbols or sections | Required responsibility after this task |
|---|---|---|---|
| `<project-relative path>` | Add/Modify/Remove/Rename/Generate | `<symbol>` | `<responsibility>` |

## 7. Contracts and Technical Details

Include only details needed to avoid implementation-time design decisions:

- Function or method contracts.
- Types and data shapes.
- API or event contracts.
- Validation rules.
- State transitions.
- Persistence rules.
- Configuration behavior.
- Pseudocode for non-obvious algorithms.

Use examples when they clarify a boundary. Do not invent exact signatures that the repository does not support.

## 8. Step-by-Step Implementation

1. `<specific action in a named file or symbol>`
   - **Why:** `<reason>`
   - **Required result:** `<observable or structural result>`
2. `<next action>`

Order steps so the executor does not need to discover hidden prerequisites.

## 9. Failure, Edge, and Recovery Cases

| Case | Required behavior | Implementation note | Validation scenario |
|---|---|---|---|
| `<invalid/boundary/failure case>` | `<result>` | `<handling>` | V02 |

Consider only applicable cases such as invalid input, empty state, duplicate calls, partial failure, timeouts, retries, concurrency, ordering, stale data, legacy data, permission failure, cancellation, and rollback.

## 10. Tests to Add or Update

| Test | Level | Setup | Action | Expected result | Suggested location |
|---|---|---|---|---|---|
| `<name or behavior>` | Unit/Integration/Contract/E2E/Manual | `<setup>` | `<action>` | `<result>` | `<project-relative path>` |

## 11. Verification

1. **Command or procedure:** `<exact project-evidenced check>`
   - **Expected result:** `<observable success>`
   - **Evidence source:** `<script, CI, or guidance path>`
2. `<additional check when needed>`

Do not use “test it,” “check it,” or “make sure it works.”

## 12. Expected Outputs

- `<modified or created project file>`
- `<new behavior, generated artifact, migration state, documentation, log, or metric>`

## 13. Explicit Non-Scope

- `<nearby behavior this task must not change>`

## 14. Stop and Escalate When

Stop this task and update the specification when:

- `<discovery would require a new contract, architecture, dependency, migration, security decision, or product rule>`

Write `None beyond the package-wide conditions` only when no task-specific condition exists.

## 15. Done Checklist

- [ ] Required behavior is implemented.
- [ ] Named files and symbols match the packet or documented evidence-backed adjustments were synchronized back to the package.
- [ ] Applicable failure and edge cases are handled.
- [ ] Required tests are added or updated.
- [ ] Every verification check passes.
- [ ] Expected outputs exist.
- [ ] Explicit non-scope remains unchanged.
- [ ] Related validation scenarios are satisfied.
```

## Packet quality rules

- The packet must be usable after reading only this file and its completed dependency packets.
- Repeat a small amount of essential context; do not duplicate unrelated plan material.
- Prefer exact behavior and observable results over line-by-line code prescriptions when multiple correct implementations fit project conventions.
- Include pseudocode only when it prevents a real ambiguity.
- Never leave `TODO`, `TBD`, “as needed,” or unexplained placeholders in a ready packet.
