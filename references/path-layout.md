# Path Layout

Use this reference to create a private, collision-safe specifications package outside the project repository.

## Resolve the project root

Use this precedence:

1. A project directory explicitly supplied by the user.
2. The version-control repository root containing the current working directory.
3. The workspace root supplied by the coding environment.
4. The current working directory.

Canonicalize the selected path. Resolve `~`, relative components, symbolic links when supported, and platform separators. The canonical absolute path is the checkout identity.

## Select the global specifications root

Use this precedence:

1. A specifications root explicitly supplied by the user.
2. `AGENT_SPECS_ROOT`.
3. `AGENT_PLANS_ROOT` for compatibility with an existing planning setup.
4. `~/.agent/specs`.

Expand and canonicalize the selected root. Reject a root that is inside the project directory.

## Create the project specifications directory

Convert the canonical project path into a readable flat slug:

1. Replace separators and unsupported filename characters with `-`.
2. Collapse repeated hyphens.
3. Trim leading and trailing hyphens.
4. Preserve letter case for readability.
5. Compute SHA-256 over the complete canonical project path encoded as UTF-8.
6. Append the first 10 lowercase hexadecimal characters using exactly `--`.

```text
<specs-root>/<canonical-project-path-slug>--<path-hash>/
```

Hash the full canonical path. Do not hash a shortened or transformed path.

## Create the package directory

Use:

```text
YYYY-MM-DD-HHmmss-<outcome-slug>
```

- Generate the timestamp from current local time and include seconds.
- Use a short, descriptive lowercase kebab-case outcome slug.
- If the directory exists, append `-2`, `-3`, and so on.
- Never overwrite or reuse an unrelated package.

Create:

```text
<planning-package>/
├── plan.md
├── tasks.md
├── validation.md
└── task-details/
```

Only create task-detail files for actual tasks.

## Safety checks

Before writing:

- Confirm all resolved paths are absolute.
- Reject unresolved `..` components.
- Confirm the package remains beneath the selected specifications root.
- Confirm the specifications root and package are outside the project tree.
- Keep secrets and sensitive data out of directory names and files.
- Create missing parent directories safely.

## Metadata to record

Record in `plan.md`:

- Original and canonical project directories.
- Global specifications root.
- Project specifications root.
- Package directory.
- Creation time with timezone offset.
- Version-control branch and commit when available.

Use absolute paths only in package metadata. Use project-relative paths everywhere implementation work is described.
