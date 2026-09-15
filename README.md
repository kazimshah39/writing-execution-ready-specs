# Writing Execution-Ready Specs

An AI coding-agent skill for creating detailed, evidence-backed software implementation specifications that can be handed to a junior developer or limited-context AI agent.

The skill produces a complete zero-context handoff package before implementation begins. It is intended for complex, risky, cross-system, or delegated work where the executor should not need to make hidden architecture or product decisions.

## When to use it

Use this skill for work such as:

- Large or cross-system features
- Authentication, authorization, payments, or sensitive data changes
- Database and API migrations
- Architecture changes
- Multi-stage refactors
- Work delegated to junior developers
- Work delegated across multiple AI agents
- Long-running work where conversation context may be lost
- Tasks that require exact traceability from requirements to validation

For ordinary features, bug fixes, and refactors that only need `plan.md` and `tasks.md`, use the lighter `writing-project-plans` skill instead.

## What it creates

Each specification package contains:

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

### `plan.md`

The complete technical source of truth, including:

- Objective, scope, goals, and non-goals
- Requirements, constraints, and acceptance criteria
- Assumptions and blocking questions
- Current-state evidence from the project
- Architecture decisions and rejected alternatives
- Component responsibilities
- Control flow, data flow, and state transitions
- Interfaces, types, schemas, APIs, events, and configuration
- Errors, edge cases, retries, concurrency, and recovery
- Security, privacy, performance, reliability, and accessibility
- File and symbol impact
- Implementation workflow
- Testing strategy
- Migration, compatibility, rollout, and backout
- Documentation and operational changes
- Risks and mitigations
- Requirement-to-task-to-validation traceability
- Final implementation-readiness verdict

### `tasks.md`

A dependency-ordered task index. Every task includes:

- A stable task ID
- An observable goal
- Dependencies
- Affected files or areas
- Primary verification
- A link to its standalone task packet

### `task-details/TNN.md`

One standalone execution packet per task. Each packet contains:

- Goal and reason
- Preconditions and dependencies
- Verified current behavior
- Exact required behavior
- Files, areas, and symbols
- Contracts and technical details
- Ordered implementation steps
- Failure, edge, and recovery cases
- Tests expressed as setup, action, and expected result
- Exact verification commands or procedures
- Expected outputs
- Explicit non-scope
- Stop-and-escalate conditions
- A task-specific done checklist

### `validation.md`

A validation and traceability matrix covering:

- Project quality gates
- Positive and negative scenarios
- Boundary and failure cases
- Recovery and regression checks
- Compatibility and migration checks
- Security, performance, and accessibility checks when relevant
- Manual procedures where automation is insufficient
- Requirement and acceptance-criteria coverage
- File and generated-artifact coverage

## Zero-context handoff standard

A package is considered ready only when an executor who has not seen the original conversation can:

1. Understand the current and intended behavior.
2. Identify the exact project areas to change.
3. Follow the work in a safe dependency order.
4. Complete tasks without choosing new architecture or product behavior.
5. Handle the important edge and failure cases.
6. Run precise validation and recognize success.
7. Know when to stop and request a specification update.

If a missing owner decision prevents safe implementation, the package is marked `Blocked` rather than presenting guesses as facts.

## Evidence rules

The skill separates information into five categories:

- **User requirement:** Explicitly requested behavior or constraints
- **Verified evidence:** Information found in project code, tests, configuration, schemas, or documentation
- **Decision:** The selected implementation direction and its tradeoffs
- **Assumption:** A non-blocking belief that must be verified
- **Open question:** Missing information with an owner, impact, and resolution path

The skill does not invent project files, symbols, commands, dependencies, schemas, contracts, or product behavior.

## Output location

Specification packages are always stored outside the project repository.

The global specifications root is selected in this order:

1. A location explicitly supplied by the user
2. The `AGENT_SPECS_ROOT` environment variable
3. `AGENT_PLANS_ROOT`, for compatibility with an existing planning setup
4. `~/.agent/specs`

The generated layout is:

```text
<specs-root>/
└── <canonical-project-path-slug>--<path-hash>/
    └── YYYY-MM-DD-HHmmss-<outcome-slug>/
        ├── plan.md
        ├── tasks.md
        ├── validation.md
        └── task-details/
```

The project directory name includes the first 10 lowercase hexadecimal characters of the canonical project path's SHA-256 hash. This prevents collisions between different checkouts that produce the same readable path slug.

For example:

```text
~/.agent/specs/
└── Users-example-projects-customer-portal--a1b2c3d4e5/
    └── 2026-09-15-143025-add-team-permissions/
        ├── plan.md
        ├── tasks.md
        ├── validation.md
        └── task-details/
            ├── T01.md
            ├── T02.md
            └── T03.md
```

Planning files are never written into the project root, `docs/`, or another project subdirectory.

## Installation

Copy or clone this directory into the skills directory supported by your AI coding agent. The exact location depends on the agent or platform.

The installed skill should keep this structure:

```text
writing-execution-ready-specs/
├── SKILL.md
├── README.md
└── references/
    ├── package-reviewer.md
    ├── path-layout.md
    ├── plan-template.md
    ├── task-detail-template.md
    ├── tasks-template.md
    └── validation-template.md
```

Reload your AI coding agent if it does not detect the skill immediately.

## Usage

Explicitly name the skill when you want the detailed execution-ready workflow instead of a lighter planning workflow.

Example:

```text
Use $writing-execution-ready-specs to create an execution-ready specification for adding team-based permissions.
```

With an explicit project directory:

```text
Use $writing-execution-ready-specs to plan the billing migration for /path/to/project.
```

With a custom output root:

```text
Use $writing-execution-ready-specs to plan the billing migration for /path/to/project.
Store the specification under /path/to/private/specifications.
```

The skill creates and reviews the specification package, reports its paths and readiness status, and stops without implementing project changes.

## Workflow

The skill follows these phases:

1. Resolve the project and external specification paths.
2. Create a private, timestamped package directory.
3. Inspect relevant project code, guidance, tests, schemas, and tooling.
4. Normalize requirements, assumptions, constraints, and open questions.
5. Write and review `plan.md`.
6. Derive the dependency-ordered `tasks.md` index.
7. Create one standalone detail packet for every task.
8. Create the validation and traceability matrix.
9. Review the complete package for zero-context implementability.
10. Report the generated paths and stop before implementation.

## Safety and quality rules

- The specification package remains outside the project repository.
- Implementation does not begin unless separately requested.
- Commands must come from project scripts, CI, documentation, or contributor guidance.
- Absolute paths are used only for package metadata and file creation.
- Implementation paths are project-relative.
- Secrets, credentials, tokens, private keys, connection strings, and sensitive real data are excluded.
- Tasks cannot introduce designs, dependencies, files, or behavior absent from the reviewed plan.
- Each task must have exactly one matching standalone packet.
- Every acceptance criterion must map to implementation tasks and validation scenarios.
- A package with unresolved blocking decisions must be marked `Blocked`.

## Repository structure

```text
writing-execution-ready-specs/
├── SKILL.md
├── README.md
└── references/
    ├── package-reviewer.md
    ├── path-layout.md
    ├── plan-template.md
    ├── task-detail-template.md
    ├── tasks-template.md
    └── validation-template.md
```

| File | Purpose |
|---|---|
| `SKILL.md` | Main skill instructions and workflow |
| `references/path-layout.md` | External package path and naming rules |
| `references/plan-template.md` | Detailed specification structure |
| `references/tasks-template.md` | Dependency-ordered execution index format |
| `references/task-detail-template.md` | Standalone task-packet format |
| `references/validation-template.md` | Validation and traceability format |
| `references/package-reviewer.md` | Plan and complete-package review process |

## Validation

Validate the skill using the validation tools provided by your AI coding-agent platform. At minimum, verify that:

- `SKILL.md` has valid YAML frontmatter.
- The skill name matches the directory name.
- Every reference linked from `SKILL.md` exists.
- No scaffold placeholders remain.
- The instructions and templates use consistent task, requirement, and validation IDs.
- A realistic test request produces the expected package structure.

If your platform provides a skill validator, run it before publishing a release.

## Contributing

Keep changes focused on reducing implementation uncertainty. Avoid adding generic sections, repeated advice, or fixed steps that do not improve correctness.

When changing a template:

1. Update the related instructions in `SKILL.md` when necessary.
2. Keep IDs, terminology, and file relationships consistent.
3. Confirm every reference linked from `SKILL.md` still exists.
4. Run the skill validator.
5. Test the skill on a realistic software request before publishing a release.

## License

No license is included yet. Add a `LICENSE` file before publishing if you want others to reuse or modify the skill under defined terms.
