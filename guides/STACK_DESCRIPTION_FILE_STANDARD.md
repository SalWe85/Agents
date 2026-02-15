# Stack Description File Standard

Use this standard in any project where developer/tester agents run.

## Recommended Path
- Primary: `/STACK.md`
- Optional fallback: `/docs/STACK.md`

## Why This Exists
Developer and tester agents are repo-agnostic. A stack file removes guesswork and makes command/tool selection deterministic.

## Required Sections
1. Runtime and language versions
2. Backend framework and structure
3. Frontend framework and structure (if present)
4. Test strategy and required command set
5. Build/compile commands
6. Lint/static analysis commands
7. Branch policy and commit message convention
8. Task tracking conventions (`codex_dev_done`, `codex_test_done`, `codex_review_ready`)
9. Issue tracking integration rules (for example Linear status/comment expectations)

## Minimal Template
```md
# STACK

## Runtime
- Node: 22.x
- Python: 3.12

## Backend
- Framework:
- Key directories:

## Frontend
- Framework:
- Key directories:

## Validation Commands
- Lint:
- Test:
- Build:

## Branch and Commit Policy
- Default branch:
- Task branch pattern: codex/<task-id>-<slug>
- Commit message pattern: <task-id>: <summary>

## Task Status Policy
- codex_dev_done:
- codex_test_done:
- codex_review_ready:

## Issue Tracker Policy
- Linear state mapping:
- Required completion comment format:
```

## Notes
- Keep this file updated when toolchains change.
- If your repo has multiple services with different stacks, include per-service subsections.
