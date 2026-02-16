# Usage Template

## Blank Template
```text
Agent: backend-tester
Goal:
Inputs: task_identifier:
Inputs: repo_root:
Inputs: default_branch: main
Inputs: test_target:
Inputs: stack_file_path:
Inputs: harness_mode: developer_handoff
Inputs: extra_test_focus:
Inputs: task_list_path: /reports/SPRINT_EXECUTION_LOG.md
Inputs: linear_issue_id:
Inputs: linear_workflow_path: /Users/slobodan/Projects/Agents/agents/_shared/LINEAR_WORKFLOW.md
Inputs: worktree_policy_path: /Users/slobodan/Projects/Agents/agents/_shared/WORKTREE_POLICY.md
Inputs: linear_ready_statuses: Agent work DONE, Agent testing
Inputs: post_not_ready_comment: true
Inputs: branch_name:
Inputs: commit_mode: commit
Constraints:
- Use `linear_workflow_path` as the default status source; override only when necessary.
- Use `worktree_policy_path` as the default worktree behavior source; never create new worktree without permission.
- Check Linear status + latest developer handoff comment before running any test command.
- If task is not ready, stop early and report NOT_READY without executing tests.
- Prefer branch from latest developer handoff comment; use Inputs: branch_name only if handoff comment lacks branch.
- Run configurable backend checks with evidence.
- In developer_handoff mode, run fullest feasible suite for changed backend scope.
- Add/adjust tests when coverage gaps are found.
- Update task list status when task list exists.
- Update Linear issue status/comment when linear_issue_id is provided.
Output:
- /reports/BACKEND_TEST_REPORT.md
- Optional test code changes
- Task status update (`NOT_READY` early exit, or `codex_test_done` and `codex_review_ready` on pass)
```

## Filled Example
```text
Agent: backend-tester
Goal: Validate recent webhook idempotency implementation and close backend testing phase.
Inputs: task_identifier: UOW-014
Inputs: repo_root: /workspace/payments-service
Inputs: default_branch: main
Inputs: test_target: src/webhooks/payment_handler.*, tests/webhooks/*
Inputs: stack_file_path: /workspace/payments-service/STACK.md
Inputs: harness_mode: developer_handoff
Inputs: extra_test_focus: contract
Inputs: task_list_path: /workspace/payments-service/reports/SPRINT_EXECUTION_LOG.md
Inputs: linear_issue_id: PAY-221
Inputs: linear_workflow_path: /Users/slobodan/Projects/Agents/agents/_shared/LINEAR_WORKFLOW.md
Inputs: worktree_policy_path: /Users/slobodan/Projects/Agents/agents/_shared/WORKTREE_POLICY.md
Inputs: linear_ready_statuses: Agent work DONE, Agent testing
Inputs: post_not_ready_comment: true
Inputs: branch_name: codex/uow-014-webhook-idempotency
Inputs: commit_mode: commit
Constraints:
- Use `linear_workflow_path` as the default status source; override only when necessary.
- Use `worktree_policy_path` as the default worktree behavior source; never create new worktree without permission.
- Check Linear status + latest developer handoff comment before running any test command.
- If task is not ready, stop early and report NOT_READY without executing tests.
- Prefer branch from latest developer handoff comment; use Inputs: branch_name only if handoff comment lacks branch.
- Run configurable backend checks with evidence.
- In developer_handoff mode, run fullest feasible suite for changed backend scope.
- Add/adjust tests when coverage gaps are found.
- Update task list status when task list exists.
- Update Linear issue status/comment when linear_issue_id is provided.
Output:
- /reports/BACKEND_TEST_REPORT.md
- Optional test code changes
- Task status update (`NOT_READY` early exit, or `codex_test_done` and `codex_review_ready` on pass)
```
