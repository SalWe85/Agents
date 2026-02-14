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
Constraints: Use Playwright skill and playwright-cli. If missing, install both first. No source code changes.
Output: /reports/FRONTEND_TEST_REPORT.md
```

### Expected Output
```text
Preflight checks run first and report skill/CLI readiness.
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
Constraints: Use Playwright skill and playwright-cli. If missing, install both first. No source code changes.
Output: /reports/FRONTEND_TEST_REPORT.md
```

### Expected Output
```text
Creates /reports/FRONTEND_TEST_REPORT.md with preflight section plus scenario outcomes.
Failures include exact repro steps, evidence references, severity, and next action.
Blocked scenarios are clearly marked with reason.
```
