# Usage Template

## Blank Template
```text
Agent: frontend-developer
Goal:
Inputs: task_identifier:
Inputs: repo_root:
Inputs: default_branch: main
Inputs: acceptance_criteria:
Inputs: stack_file_path:
Inputs: design_source:
Inputs: task_list_path: /reports/SPRINT_EXECUTION_LOG.md
Inputs: linear_issue_id:
Inputs: branch_name:
Inputs: commit_mode: commit
Constraints:
- Implement changes directly.
- Include task identifier in commit messages.
- Run lint/typecheck/test/build checks.
- Update task list status when task list exists.
- Update Linear issue status/comment when linear_issue_id is provided.
Output:
- Frontend code changes
- Task status update (`codex_dev_done` then tester/review handoff)
- Summary of checks run and results
```

## Filled Example
```text
Agent: frontend-developer
Goal: Implement keyboard-accessible filter drawer and persistent filter state on orders page.
Inputs: task_identifier: WEB-88
Inputs: repo_root: /workspace/orders-web
Inputs: default_branch: main
Inputs: acceptance_criteria: Drawer is fully keyboard navigable, filters persist on reload, and mobile layout remains usable.
Inputs: stack_file_path: /workspace/orders-web/STACK.md
Inputs: design_source: https://www.figma.com/design/example/orders-filters
Inputs: task_list_path: /workspace/orders-web/reports/SPRINT_EXECUTION_LOG.md
Inputs: linear_issue_id: WEB-88
Inputs: branch_name: codex/web-88-filter-drawer-a11y
Inputs: commit_mode: commit
Constraints:
- Implement changes directly.
- Include task identifier in commit messages.
- Run lint/typecheck/test/build checks.
- Update task list status when task list exists.
- Update Linear issue status/comment when linear_issue_id is provided.
Output:
- Frontend code changes
- Task status update (`codex_dev_done` then tester/review handoff)
- Summary of checks run and results
```
