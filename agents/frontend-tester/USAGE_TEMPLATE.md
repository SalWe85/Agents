# Usage Template

## Blank Template
```text
Agent: frontend-tester
Goal: Frontend scope to test:
Inputs: Target URL/environment:
Inputs: Key user flows to validate:
Inputs: Credentials or test account details:
Inputs: linear_issue_id:
Inputs: linear_workflow_path: /Users/slobodan/Projects/Agents/agents/_shared/LINEAR_WORKFLOW.md
Inputs: worktree_policy_path: /Users/slobodan/Projects/Agents/agents/_shared/WORKTREE_POLICY.md
Inputs: linear_ready_statuses: Agent work DONE, Agent testing
Inputs: post_not_ready_comment: true
Inputs: branch_name:
Constraints: Use `linear_workflow_path` as the default status source; override only when necessary. Use `worktree_policy_path` as the default worktree behavior source; never create new worktree without permission. Check Linear status + latest developer handoff comment before browser testing when linear_issue_id is provided. If not ready, stop and return NOT_READY. Prefer branch from latest developer handoff comment; use Inputs: branch_name only if handoff comment lacks branch. Use Playwright skill and playwright-cli first. If missing, install both first. Use Chrome DevTools MCP only when deeper diagnostics are needed. No source code changes.
Output: /reports/FRONTEND_TEST_REPORT.md
```

## Filled Example
```text
Agent: frontend-tester
Goal: Validate login, dashboard loading, and billing page flow before release.
Inputs: Target URL/environment: https://staging.example.app
Inputs: Key user flows to validate: login, dashboard filters, billing invoice download.
Inputs: Credentials or test account details: use qa_user_staging account from team vault.
Inputs: linear_issue_id: WEB-88
Inputs: linear_workflow_path: /Users/slobodan/Projects/Agents/agents/_shared/LINEAR_WORKFLOW.md
Inputs: worktree_policy_path: /Users/slobodan/Projects/Agents/agents/_shared/WORKTREE_POLICY.md
Inputs: linear_ready_statuses: Agent work DONE, Agent testing
Inputs: post_not_ready_comment: true
Inputs: branch_name: codex/web-88-filter-drawer-a11y
Constraints: Use `linear_workflow_path` as the default status source; override only when necessary. Use `worktree_policy_path` as the default worktree behavior source; never create new worktree without permission. Check Linear status + latest developer handoff comment before browser testing when linear_issue_id is provided. If not ready, stop and return NOT_READY. Prefer branch from latest developer handoff comment; use Inputs: branch_name only if handoff comment lacks branch. Use Playwright skill and playwright-cli first. If missing, install both first. Use Chrome DevTools MCP if failures need console/network evidence. No source code changes.
Output: /reports/FRONTEND_TEST_REPORT.md
```
