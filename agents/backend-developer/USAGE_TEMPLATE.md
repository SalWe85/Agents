# Usage Template

## Blank Template
```text
Agent: backend-developer
Goal:
Inputs: task_identifier:
Inputs: repo_root:
Inputs: default_branch: main
Inputs: acceptance_criteria:
Inputs: stack_file_path:
Inputs: task_list_path: /reports/SPRINT_EXECUTION_LOG.md
Inputs: linear_issue_id:
Inputs: linear_workflow_path: /Users/slobodan/Projects/Agents/agents/_shared/LINEAR_WORKFLOW.md
Inputs: linear_ready_for_test_status: Agent work DONE
Inputs: branch_name:
Inputs: commit_mode: commit
Constraints:
- Implement changes directly.
- Use `linear_workflow_path` as the default status source; override only when necessary.
- Include task identifier in commit messages.
- Run lint/test/build checks before completion.
- Commit and push the task branch before updating Linear.
- Update task list status when task list exists.
- Update Linear issue to testing-ready status and include backend-tester handoff with branch + commit.
Output:
- Backend code changes
- Task status update (`codex_dev_done` then tester/review handoff with branch reference)
- Summary of checks run and results
```

## Filled Example
```text
Agent: backend-developer
Goal: Implement idempotent retry handling for payment webhook processing.
Inputs: task_identifier: UOW-014
Inputs: repo_root: /workspace/payments-service
Inputs: default_branch: main
Inputs: acceptance_criteria: Duplicate webhook deliveries do not create duplicate ledger entries; retries are safe.
Inputs: stack_file_path: /workspace/payments-service/STACK.md
Inputs: task_list_path: /workspace/payments-service/reports/SPRINT_EXECUTION_LOG.md
Inputs: linear_issue_id: PAY-221
Inputs: linear_workflow_path: /Users/slobodan/Projects/Agents/agents/_shared/LINEAR_WORKFLOW.md
Inputs: linear_ready_for_test_status: Agent work DONE
Inputs: branch_name: codex/uow-014-webhook-idempotency
Inputs: commit_mode: commit
Constraints:
- Implement changes directly.
- Use `linear_workflow_path` as the default status source; override only when necessary.
- Include task identifier in commit messages.
- Run lint/test/build checks before completion.
- Commit and push the task branch before updating Linear.
- Update task list status when task list exists.
- Update Linear issue to testing-ready status and include backend-tester handoff with branch + commit.
Output:
- Backend code changes
- Task status update (`codex_dev_done` then tester/review handoff with branch reference)
- Summary of checks run and results
```
