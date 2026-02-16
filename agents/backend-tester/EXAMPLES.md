# Examples

Use these as starting points. Review and adapt test targets, harness mode, and report expectations to your service architecture.

## Example 1: Developer Handoff with Full Practical Coverage

### Input
```text
Agent: backend-tester
Goal: Validate inventory reservation logic implemented by backend-developer and close testing handoff.
Inputs: task_identifier: INV-118
Inputs: repo_root: /workspace/inventory-service
Inputs: default_branch: main
Inputs: test_target: src/reservations/*, src/api/reservations_controller.*, tests/reservations/*
Inputs: stack_file_path: /workspace/inventory-service/STACK.md
Inputs: harness_mode: developer_handoff
Inputs: extra_test_focus: contract
Inputs: task_list_path: /workspace/inventory-service/reports/SPRINT_EXECUTION_LOG.md
Inputs: linear_issue_id: INV-118
Inputs: linear_workflow_path: /Users/slobodan/Projects/Agents/agents/_shared/LINEAR_WORKFLOW.md
Inputs: worktree_policy_path: /Users/slobodan/Projects/Agents/agents/_shared/WORKTREE_POLICY.md
Inputs: branch_name: codex/inv-118-reservation-fixes
Inputs: commit_mode: commit
Constraints:
- In developer_handoff mode run fullest feasible backend suite.
- Add missing tests if coverage gaps are found.
- Update task status on completion.
Output:
- /reports/BACKEND_TEST_REPORT.md and status updates.
```

### Expected Output
```text
Runs broad backend validation for changed reservation scope (lint, unit/integration, build).
Checks Linear status/comments first and only proceeds when issue is in testing-ready state with a developer handoff comment.
Adds/updates backend tests if uncovered behavior is detected.
Writes /reports/BACKEND_TEST_REPORT.md with evidence and pass/fail outcomes.
Updates task list to codex_test_done and codex_review_ready when checks pass.
Updates Linear issue INV-118 with test summary comment.
Commits test-only task-scoped changes with INV-118 in commit message.
```

## Example 2: Targeted Regression Check for Hotfix

### Input
```text
Agent: backend-tester
Goal: Run targeted regression tests for authentication hotfix before review.
Inputs: task_identifier: SEC-90
Inputs: repo_root: /workspace/auth-service
Inputs: default_branch: release
Inputs: test_target: src/auth/token_service.*, tests/auth/token_service_spec.*
Inputs: stack_file_path:
Inputs: harness_mode: targeted
Inputs: extra_test_focus: security-smoke
Inputs: task_list_path: /workspace/auth-service/reports/SPRINT_EXECUTION_LOG.md
Inputs: commit_mode: no-commit
Constraints:
- Keep testing focused to auth token scope.
- Do not mark review-ready if critical failures remain.
Output:
- /reports/BACKEND_TEST_REPORT.md and status recommendation.
```

### Expected Output
```text
Inspects stack because stack file is missing and selects best-available backend test commands.
If Linear issue is not in testing-ready state, exits early as NOT_READY before any test execution.
Runs targeted auth regression checks plus requested security-smoke tests.
Writes /reports/BACKEND_TEST_REPORT.md with explicit blocker details if failures remain.
Sets codex_test_done and codex_review_ready only if all critical checks pass.
Skips commit creation due to commit_mode=no-commit.
```
