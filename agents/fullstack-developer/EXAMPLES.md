# Examples

Use these as starting points. Review and adapt stack assumptions, test strategy, and task tracker paths for your project.

## Example 1: Coupled Server + UI Change (Thymeleaf-Style)

### Input
```text
Agent: fullstack-developer
Goal: Add invoice approval flow with role checks, backend state transitions, and server-rendered confirmation views.
Inputs: task_identifier: BILL-55
Inputs: repo_root: /workspace/billing-app
Inputs: default_branch: main
Inputs: acceptance_criteria: Only approvers can approve, state transitions are auditable, and UI confirmation reflects final state.
Inputs: stack_file_path: /workspace/billing-app/STACK.md
Inputs: task_list_path: /workspace/billing-app/reports/SPRINT_EXECUTION_LOG.md
Inputs: linear_issue_id: BILL-55
Inputs: tester_strategy: both
Inputs: commit_mode: commit
Constraints:
- Implement fullstack changes directly.
- Run checks for changed layers.
- Keep commits scoped to BILL-55.
Output:
- Code changes + status updates + validation summary.
```

### Expected Output
```text
Creates/switches task branch from main and implements backend + server-rendered UI updates.
Runs backend and frontend relevant checks.
Updates task list to codex_dev_done.
Hands off to backend-tester and frontend-tester.
After testing completion, marks codex_review_ready.
Updates Linear issue BILL-55 with status/comment.
Commits task-scoped changes with BILL-55 in commit messages.
```

## Example 2: Backend-Heavy Task with Minimal UI Impact

### Input
```text
Agent: fullstack-developer
Goal: Introduce new pricing rule engine and expose results in existing dashboard widget.
Inputs: task_identifier: PRC-90
Inputs: repo_root: /workspace/pricing-suite
Inputs: default_branch: develop
Inputs: acceptance_criteria: Rule engine computes expected totals; dashboard widget displays new total without layout regressions.
Inputs: stack_file_path:
Inputs: task_list_path: /workspace/pricing-suite/reports/SPRINT_EXECUTION_LOG.md
Inputs: tester_strategy: auto
Inputs: commit_mode: commit
Constraints:
- Ask for choice if stack ambiguity affects implementation.
- Run relevant checks for touched layers.
Output:
- Code changes + status updates + validation summary.
```

### Expected Output
```text
Inspects stack due to missing stack file; if ambiguity exists, proposes preferred route and asks user before edits.
Implements backend-heavy changes and limited UI update on a task branch from develop.
Runs full backend checks and scoped frontend checks.
Updates task list to codex_dev_done and hands off at least to backend-tester.
Moves to codex_review_ready after required tester outputs are complete.
Commits PRC-90 scoped changes with PRC-90 in commit messages.
```
