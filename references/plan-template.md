# Detailed `plan.md` Template

Use this structure as the source of truth. Adapt sections to the project, but do not silently omit a material concern. For an irrelevant concern, write `Not applicable — <specific reason>`.

```markdown
# <Observable outcome> — Execution-Ready Specification

## Package Metadata

- **Created:** `<ISO-8601 timestamp with timezone>`
- **Original project directory:** `<absolute path or Same as canonical>`
- **Canonical project directory:** `<canonical absolute path>`
- **Global specifications root:** `<absolute path>`
- **Project specifications root:** `<absolute path>`
- **Package directory:** `<absolute path>`
- **Version-control branch:** `<branch or Unavailable>`
- **Version-control commit:** `<full commit or Unavailable>`
- **Specification status:** `Ready` or `Blocked`

## 1. Executive Handoff Summary

Explain the problem, requested outcome, chosen direction, affected users or systems, main implementation stages, and expected result. State whether implementation can start immediately.

## 2. Request Normalization

### 2.1 Original Intent

Preserve the user's request without changing its meaning.

### 2.2 Observable Objective

Define the final result in behavior that can be observed or tested.

### 2.3 Goals

- **G1:** `<required outcome>`

### 2.4 Non-Goals

- **NG1:** `<explicitly excluded work>`

### 2.5 Definitions and Glossary

| Term | Meaning in this specification |
|---|---|
| `<term>` | `<unambiguous definition>` |

## 3. Requirements, Constraints, and Acceptance

### 3.1 Functional Requirements

| ID | Requirement | Source | Priority | Verification summary |
|---|---|---|---|---|
| R1 | `<exact behavior>` | User requirement / `<evidence path>` | Must | `<observable check>` |

### 3.2 Non-Functional Requirements

Cover applicable security, privacy, performance, scalability, reliability, accessibility, maintainability, compatibility, and operational requirements.

### 3.3 Technical and Product Constraints

| ID | Constraint | Source | Design impact |
|---|---|---|---|
| C1 | `<constraint>` | `<source>` | `<impact>` |

### 3.4 Acceptance Criteria

| ID | Observable criterion | Related requirements |
|---|---|---|
| AC1 | `<measurable completed behavior>` | R1 |

## 4. Assumptions and Open Questions

### 4.1 Assumptions

| ID | Assumption | Evidence or reason | Risk if false | Verification owner and step |
|---|---|---|---|---|
| A1 | `<assumption>` | `<reason>` | `<impact>` | `<who/how>` |

### 4.2 Open Questions

| ID | Question | Why it matters | Owner | Resolution path | Blocking? |
|---|---|---|---|---|---|
| Q1 | `<question>` | `<impact>` | `<owner>` | `<how to resolve>` | Yes/No |

Write `None` when there are no open questions.

## 5. Current-State Evidence

### 5.1 Relevant Architecture

Describe the current components and boundaries. Cite project-relative paths and symbols.

### 5.2 Current Control and Data Flow

Describe the current happy path and relevant failure paths step by step.

### 5.3 Existing Interfaces and Contracts

List current APIs, functions, types, schemas, events, configuration, persistence, and external contracts.

### 5.4 Existing Tests and Tooling

List relevant tests and the project-evidenced commands used to run them.

### 5.5 Current Limitations

Explain the exact gap between current and requested behavior.

## 6. Decisions and Alternatives

### 6.1 Decision Summary

| ID | Decision | Reason | Requirements served |
|---|---|---|---|
| D1 | `<selected direction>` | `<reason>` | R1 |

### 6.2 Alternatives Considered

For each material alternative, record its benefits, costs, risks, and reason for rejection. Do not create fake alternatives for obvious local edits.

### 6.3 Tradeoffs and Consequences

State new maintenance costs, compatibility effects, operational costs, or limitations introduced by the selected design.

## 7. Target Design

### 7.1 Design Overview

Describe the final architecture and why it fits project conventions.

### 7.2 Component Responsibilities

| Component or layer | Inputs | Responsibility | Outputs | Dependencies | Failure behavior |
|---|---|---|---|---|---|
| `<component>` | `<inputs>` | `<responsibility>` | `<outputs>` | `<dependencies>` | `<behavior>` |

### 7.3 Target Control Flow

Provide ordered flows for important operations. Include authentication, validation, persistence, external calls, response generation, and recovery where applicable.

### 7.4 Target Data Flow and State Transitions

Define data origins, transformations, ownership, persistence, lifecycle, state transitions, invalid transitions, and concurrency behavior.

### 7.5 Interfaces and Contracts

Specify exact known signatures, types, schemas, endpoints, status codes, events, configuration keys, CLI behavior, and UI contracts. Clearly mark values that must still be confirmed.

### 7.6 Validation and Error Contract

For each important failure, define detection, internal handling, user-visible result, logging, retryability, and recovery.

### 7.7 Security and Privacy

Cover authorization, authentication, trust boundaries, input handling, secrets, sensitive data, auditability, abuse controls, and data retention.

### 7.8 Performance, Scalability, and Reliability

Cover expected load, complexity, database access, caching, batching, timeouts, retries, idempotency, rate limits, resource limits, and degraded behavior when applicable.

### 7.9 Accessibility and User Experience

Cover keyboard access, focus, semantics, announcements, loading, empty, error, success, and responsive states when user interfaces are affected.

## 8. Detailed File and Symbol Impact

| Path or area | Change | Symbols or sections | Current responsibility | Required modification | Related tasks | Validation |
|---|---|---|---|---|---|---|
| `<project-relative path>` | Add/Modify/Remove/Rename/Generate | `<symbols>` | `<current role>` | `<exact change>` | T01 | `<checks>` |

Include source, tests, fixtures, schemas, migrations, configuration, generated artifacts, documentation, observability, deployment, and cleanup when relevant.

## 9. Implementation Workflow

### Stage 1 — `<foundation>`

- **Purpose:** `<why this stage exists>`
- **Prerequisites:** `<decisions or earlier stages>`
- **Files and symbols:** `<project-relative paths and symbols>`
- **Detailed behavior:** `<exact changes>`
- **Failure and edge behavior:** `<cases>`
- **Outputs:** `<artifacts or observable behavior>`
- **Validation:** `<evidenced command or procedure and expected result>`

Repeat in dependency order. The workflow must agree with task IDs and dependencies.

## 10. Testing and Validation Strategy

### 10.1 Test Levels

Define unit, integration, contract, end-to-end, system, migration, security, performance, accessibility, and regression coverage as applicable.

### 10.2 Test Data and Fixtures

Describe required valid, invalid, boundary, legacy, concurrent, and failure data without including sensitive real data.

### 10.3 Quality Commands

| Purpose | Command | Expected successful result | Evidence source |
|---|---|---|---|
| `<purpose>` | `<exact command>` | `<result>` | `<script, CI, or guidance path>` |

### 10.4 Manual Validation

Use only where automation is unavailable or insufficient. Give exact setup, action, and observable result.

## 11. Data, Migration, and Compatibility

Describe schema changes, migrations, backfills, upgrade order, backward and forward compatibility, serialization, generated artifacts, feature flags, mixed-version behavior, downgrade behavior, and cleanup.

## 12. Rollout, Observability, and Backout

- **Rollout sequence:** `<ordered steps>`
- **Feature controls:** `<flags or configuration>`
- **Logs:** `<events and safe fields>`
- **Metrics:** `<signals>`
- **Alerts:** `<conditions>`
- **Success window:** `<how long and what to observe>`
- **Backout trigger:** `<condition>`
- **Backout procedure:** `<safe reversal>`
- **Post-rollout cleanup:** `<temporary elements to remove>`

## 13. Documentation and Communication

List project-relative documentation, API references, runbooks, release notes, operator instructions, and developer communication that must change.

## 14. Risks and Mitigations

| ID | Risk | Likelihood | Impact | Prevention or mitigation | Detection | Recovery |
|---|---|---|---|---|---|---|
| RK1 | `<risk>` | Low/Medium/High | Low/Medium/High | `<mitigation>` | `<signal>` | `<recovery>` |

## 15. Traceability Matrix

| Requirement | Acceptance criterion | Decision/design section | Files or areas | Task IDs | Validation scenario IDs |
|---|---|---|---|---|---|
| R1 | AC1 | D1 / 7.x | `<paths>` | T01 | V01 |

## 16. Implementation Readiness

### 16.1 Preconditions

List environment, access, owner decisions, dependency versions, data backups, or external coordination required before implementation.

### 16.2 Stop-and-Escalate Conditions

List discoveries that require revising this specification rather than making an implementation-time decision.

### 16.3 Completion Definition

The work is complete only when all required behavior, tests, quality gates, migrations, documentation, rollout controls, observability, and acceptance criteria are verified.

### 16.4 Readiness Verdict

- **Verdict:** `Ready` or `Blocked`
- **Reason:** `<concise evidence-based explanation>`
- **Blocking questions:** `<IDs or None>`
```

## Writing checks

Before review, confirm that:

- Detail is concentrated on affected behavior rather than generic advice.
- Current-state claims cite evidence.
- Decisions include reasons and real tradeoffs.
- File impacts name symbols when the repository makes them knowable.
- Workflows include important negative and recovery paths.
- Commands come from project evidence.
- Requirements, tasks, and validation remain traceable.
- The readiness verdict is honest.
