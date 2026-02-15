# Usage Template

## Blank Template
```text
Agent: fullstack-developer
Goal:
Inputs: task_identifier:
Inputs: repo_root:
Inputs: default_branch: main
Inputs: acceptance_criteria:
Inputs: stack_file_path:
Inputs: task_list_path: /reports/SPRINT_EXECUTION_LOG.md
Inputs: linear_issue_id:
Inputs: branch_name:
Inputs: tester_strategy: auto
Inputs: commit_mode: commit
Constraints:
- Implement backend and frontend changes directly when task requires both.
- Include task identifier in commit messages.
- Run relevant checks for all changed layers.
- Update task list status when task list exists.
- Update Linear issue status/comment when linear_issue_id is provided.
Output:
- Fullstack code changes
- Task status update (`codex_dev_done` then tester/review handoff)
- Summary of checks run and results
```

## Filled Example
```text
Agent: fullstack-developer
Goal: Implement order cancellation flow end-to-end with audit logging and UI confirmation states.
Inputs: task_identifier: ORD-401
Inputs: repo_root: /workspace/order-platform
Inputs: default_branch: main
Inputs: acceptance_criteria: Cancellations persist correctly, emit audit events, and UI reflects final status with rollback-safe messaging.
Inputs: stack_file_path: /workspace/order-platform/STACK.md
Inputs: task_list_path: /workspace/order-platform/reports/SPRINT_EXECUTION_LOG.md
Inputs: linear_issue_id: ORD-401
Inputs: branch_name: codex/ord-401-cancel-flow
Inputs: tester_strategy: both
Inputs: commit_mode: commit
Constraints:
- Implement backend and frontend changes directly when task requires both.
- Include task identifier in commit messages.
- Run relevant checks for all changed layers.
- Update task list status when task list exists.
- Update Linear issue status/comment when linear_issue_id is provided.
Output:
- Fullstack code changes
- Task status update (`codex_dev_done` then tester/review handoff)
- Summary of checks run and results
```
