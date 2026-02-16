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
Inputs: linear_workflow_path: /Users/slobodan/Projects/Agents/agents/_shared/LINEAR_WORKFLOW.md
Inputs: linear_ready_for_test_status: Agent work DONE
Inputs: branch_name:
Inputs: commit_mode: commit
Constraints:
- Implement changes directly.
- Use `linear_workflow_path` as the default status source; override only when necessary.
- Include task identifier in commit messages.
- Run lint/typecheck/test/build checks.
- Commit and push the task branch before updating Linear.
- Update task list status when task list exists.
- Update Linear issue to testing-ready status and include frontend-tester handoff with branch + commit.
Output:
- Frontend code changes
- Task status update (`codex_dev_done` then tester/review handoff with branch reference)
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
Inputs: linear_workflow_path: /Users/slobodan/Projects/Agents/agents/_shared/LINEAR_WORKFLOW.md
Inputs: linear_ready_for_test_status: Agent work DONE
Inputs: branch_name: codex/web-88-filter-drawer-a11y
Inputs: commit_mode: commit
Constraints:
- Implement changes directly.
- Use `linear_workflow_path` as the default status source; override only when necessary.
- Include task identifier in commit messages.
- Run lint/typecheck/test/build checks.
- Commit and push the task branch before updating Linear.
- Update task list status when task list exists.
- Update Linear issue to testing-ready status and include frontend-tester handoff with branch + commit.
Output:
- Frontend code changes
- Task status update (`codex_dev_done` then tester/review handoff with branch reference)
- Summary of checks run and results
```
