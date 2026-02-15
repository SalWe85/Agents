# Examples

Use these as starting points. Review and adapt stack constraints, test scope, and design references for your project.

## Example 1: Feature Delivery with Full Frontend Validation

### Input
```text
Agent: frontend-developer
Goal: Add bulk selection and bulk status update action to ticket table.
Inputs: task_identifier: UI-204
Inputs: repo_root: /workspace/support-portal
Inputs: default_branch: main
Inputs: acceptance_criteria: Users can select multiple rows, apply status update, and undo within 10 seconds.
Inputs: stack_file_path: /workspace/support-portal/STACK.md
Inputs: task_list_path: /workspace/support-portal/reports/SPRINT_EXECUTION_LOG.md
Inputs: linear_issue_id: UI-204
Inputs: commit_mode: commit
Constraints:
- Implement changes directly.
- Run lint/typecheck/tests/build.
- Keep commits task-scoped with UI-204 in message.
Output:
- Code changes and process updates.
```

### Expected Output
```text
Creates/switches task branch from main and implements UI/state changes.
Runs lint, typecheck, unit/component tests, and build checks.
Updates task list with codex_dev_done.
Hands off to frontend-tester for behavior verification and evidence capture.
Updates Linear issue UI-204 with completion summary.
Commits grouped changes with UI-204 in commit messages.
```

## Example 2: Stack Ambiguity Handling Before Implementation

### Input
```text
Agent: frontend-developer
Goal: Add client-side error boundary strategy for dashboard widgets.
Inputs: task_identifier: APP-52
Inputs: repo_root: /workspace/analytics-ui
Inputs: default_branch: develop
Inputs: acceptance_criteria: Widget failures do not crash page and show recoverable fallback state.
Inputs: stack_file_path:
Inputs: task_list_path: /workspace/analytics-ui/reports/SPRINT_EXECUTION_LOG.md
Inputs: commit_mode: commit
Constraints:
- If framework/tooling path is ambiguous, recommend and ask before coding.
- Run lint/typecheck/tests/build.
Output:
- Code changes and process updates.
```

### Expected Output
```text
Inspects repository and identifies ambiguous implementation path (framework-native boundary vs custom boundary wrapper).
Proposes preferred option and requests user decision before editing files.
After decision, implements selected pattern, runs checks, and updates task list to codex_dev_done.
If no UI test surface is meaningful, marks codex_review_ready directly; otherwise hands off to frontend-tester.
Commits APP-52 scoped changes with APP-52 in commit messages.
```
