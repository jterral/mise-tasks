# Mise Tasks

Shared task catalog for `mise`. It centralizes reusable task scripts, their
prerequisites and their documentation, so workflows run consistently via
`mise task run`.

## Task architecture

- Tasks live under `tasks/<task-name>/<task-name>/` and are namespaced as
  `<task-name>:<script>`.
- Every task collection must include `check-prerequisites.sh`.
- Keep each script focused on a single action and keep dependencies explicit.
- Do not introduce undocumented environment variables or required tools.

## Shell scripting

- Use `#!/usr/bin/env bash` and `set -euo pipefail` unless portability needs
  are explicitly stated.
- Validate inputs and fail fast with clear error messages.
- Prefer `jq` or `yq` for structured data; avoid fragile text parsing.
- Keep output concise and user-oriented.
- Detailed guidelines: `.claude/rules/shell.md`.

## Documentation

- Update the task README when behavior, inputs or outputs change.
- Document usage with `mise task run <task>:<script>` examples.
- Add new task collections to the root README.

## Language

All instructions, prompts, comments and contributor-facing documentation are
written in English.

## Commits, branches and PRs

Follow the skills in `.claude/skills/`: `git-conventional-commit` (scope is
mandatory), `git-branch-naming` and `git-pull-request-formatting` (use
`.github/PULL_REQUEST_TEMPLATE.md`).
