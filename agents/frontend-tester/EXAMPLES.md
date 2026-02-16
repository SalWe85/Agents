# Examples

Use these as starting points. Review them carefully and adapt target flows, credentials, and severity thresholds to your own project.

## Example 1: First-Time User Setup + Test Run

### Input
```text
Agent: frontend-tester
Goal: Validate authentication and checkout flows for first-time project setup.
Inputs: Target URL/environment: https://staging.shop.example
Inputs: Key user flows to validate: sign in, add to cart, checkout confirmation.
Inputs: Credentials or test account details: use qa_checkout_user from team vault.
Inputs: linear_issue_id: SHOP-301
Inputs: linear_workflow_path: /Users/slobodan/Projects/Agents/agents/_shared/LINEAR_WORKFLOW.md
Inputs: worktree_policy_path: /Users/slobodan/Projects/Agents/agents/_shared/WORKTREE_POLICY.md
Constraints: Use Playwright skill and playwright-cli first. If missing, install both first. Use Chrome DevTools MCP only when deeper diagnostics are needed. No source code changes.
Output: /reports/FRONTEND_TEST_REPORT.md
```

### Expected Output
```text
Preflight checks run first and report skill/CLI readiness.
When Linear issue context is provided, readiness gate (status + developer handoff comment) is checked before browser testing.
If missing, Playwright skill and CLI are installed before tests continue.
Report includes pass/fail per scenario, evidence links, severity, and recommended next actions.
```

## Example 2: Regression Smoke Before Release

### Input
```text
Agent: frontend-tester
Goal: Run smoke checks on critical user journeys before release candidate signoff.
Inputs: Target URL/environment: https://rc.app.example
Inputs: Key user flows to validate: login, dashboard load, profile update, log out.
Inputs: Credentials or test account details: use qa_release_candidate account.
Inputs: linear_issue_id: APP-52
Inputs: linear_workflow_path: /Users/slobodan/Projects/Agents/agents/_shared/LINEAR_WORKFLOW.md
Inputs: worktree_policy_path: /Users/slobodan/Projects/Agents/agents/_shared/WORKTREE_POLICY.md
Constraints: Use Playwright skill and playwright-cli first. If missing, install both first. Use Chrome DevTools MCP when failures need console/network evidence. No source code changes.
Output: /reports/FRONTEND_TEST_REPORT.md
```

### Expected Output
```text
Creates /reports/FRONTEND_TEST_REPORT.md with preflight section plus scenario outcomes.
If issue is not in testing-ready state, exits early as NOT_READY before executing flows.
Failures include exact repro steps, evidence references, severity, and next action.
Blocked scenarios are clearly marked with reason.
```

## Example 3: Deep Diagnostics for Intermittent UI Failure

### Input
```text
Agent: frontend-tester
Goal: Investigate intermittent checkout button freeze observed in staging.
Inputs: Target URL/environment: https://staging.shop.example
Inputs: Key user flows to validate: cart update, checkout submit, payment redirect.
Inputs: Credentials or test account details: use qa_checkout_user from team vault.
Inputs: linear_issue_id: SHOP-342
Inputs: linear_workflow_path: /Users/slobodan/Projects/Agents/agents/_shared/LINEAR_WORKFLOW.md
Inputs: worktree_policy_path: /Users/slobodan/Projects/Agents/agents/_shared/WORKTREE_POLICY.md
Constraints: Use Playwright skill and playwright-cli first. If flow fails or is flaky, use Chrome DevTools MCP to capture console and network diagnostics. No source code changes.
Output: /reports/FRONTEND_TEST_REPORT.md
```

### Expected Output
```text
Standard Playwright run is attempted first.
If Linear readiness checks fail, run is skipped and marked NOT_READY.
If failure is reproduced, report includes DevTools console/network findings tied to the exact failed step.
Flaky results are labeled clearly and include suggested next debugging action.
```
