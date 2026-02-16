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
Inputs: linear_workflow_path: /Users/slobodan/Projects/Agents/agents/_shared/LINEAR_WORKFLOW.md
Inputs: worktree_policy_path: /Users/slobodan/Projects/Agents/agents/_shared/WORKTREE_POLICY.md
Inputs: linear_ready_for_test_status: Agent work DONE
Inputs: branch_name:
Inputs: tester_strategy: auto
Inputs: commit_mode: commit
Constraints:
- Implement backend and frontend changes directly when task requires both.
- Use `linear_workflow_path` as the default status source; override only when necessary.
- Use `worktree_policy_path` as the default worktree behavior source; never create new worktree without permission.
- Include task identifier in commit messages.
- Run relevant checks for all changed layers.
- Commit and push the task branch before updating Linear.
- Update task list status when task list exists.
- Update Linear issue to testing-ready status and include tester handoff with branch + commit.
Output:
- Fullstack code changes
- Task status update (`codex_dev_done` then tester/review handoff with branch reference)
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
Inputs: linear_workflow_path: /Users/slobodan/Projects/Agents/agents/_shared/LINEAR_WORKFLOW.md
Inputs: worktree_policy_path: /Users/slobodan/Projects/Agents/agents/_shared/WORKTREE_POLICY.md
Inputs: linear_ready_for_test_status: Agent work DONE
Inputs: branch_name: codex/ord-401-cancel-flow
Inputs: tester_strategy: both
Inputs: commit_mode: commit
Constraints:
- Implement backend and frontend changes directly when task requires both.
- Use `linear_workflow_path` as the default status source; override only when necessary.
- Use `worktree_policy_path` as the default worktree behavior source; never create new worktree without permission.
- Include task identifier in commit messages.
- Run relevant checks for all changed layers.
- Commit and push the task branch before updating Linear.
- Update task list status when task list exists.
- Update Linear issue to testing-ready status and include tester handoff with branch + commit.
Output:
- Fullstack code changes
- Task status update (`codex_dev_done` then tester/review handoff with branch reference)
- Summary of checks run and results
```
