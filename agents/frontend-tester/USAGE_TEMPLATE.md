# Usage Template

## Blank Template
```text
Agent: frontend-tester
Goal: Frontend scope to test:
Inputs: Target URL/environment:
Inputs: Key user flows to validate:
Inputs: Credentials or test account details:
Constraints: Use Playwright skill and playwright-cli first. If missing, install both first. Use Chrome DevTools MCP only when deeper diagnostics are needed. No source code changes.
Output: /reports/FRONTEND_TEST_REPORT.md
```

## Filled Example
```text
Agent: frontend-tester
Goal: Validate login, dashboard loading, and billing page flow before release.
Inputs: Target URL/environment: https://staging.example.app
Inputs: Key user flows to validate: login, dashboard filters, billing invoice download.
Inputs: Credentials or test account details: use qa_user_staging account from team vault.
Constraints: Use Playwright skill and playwright-cli first. If missing, install both first. Use Chrome DevTools MCP if failures need console/network evidence. No source code changes.
Output: /reports/FRONTEND_TEST_REPORT.md
```
