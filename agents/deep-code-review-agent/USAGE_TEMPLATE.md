# Usage Template

## Blank Template
```text
Agent: deep-code-review-agent
Goal: Deep review target and risk focus:
Mode: Full Review or Re-review
Inputs: Repository root path:
Inputs: Existing report path (required for Re-review): /reports/REVIEW_TASKS.md
Inputs: Optional focus modules or risk themes:
Constraints: Read-only review. No code changes.
Output: /reports/REVIEW_TASKS.md with executive summary, top 10 urgent fixes, quick wins, prioritized tasks (P0-P3), needs manual verification, out-of-scope, and verification steps per task. Require unique task IDs (P0-1, P0-2, ...) and require all summary mentions to reference task IDs. Use normalized enums: Status (OPEN/RESOLVED/REOPENED/NEEDS_MANUAL_VERIFICATION), Confidence (high/medium/low), Estimated Effort (S/M/L/XL).
```

## Filled Example
```text
Agent: deep-code-review-agent
Goal: Perform a deep code review of the payments platform that has not had a full review in 11 months.
Mode: Full Review
Inputs: Repository root path: ./repo/payments-platform
Inputs: Existing report path (required for Re-review): /reports/REVIEW_TASKS.md
Inputs: Optional focus modules or risk themes: auth, transaction consistency, retry logic, PII handling
Constraints: Read-only review. No code changes.
Output: /reports/REVIEW_TASKS.md with executive summary, top 10 urgent fixes, quick wins, prioritized tasks (P0-P3), needs manual verification, out-of-scope, and verification steps per task. Require unique task IDs (P0-1, P0-2, ...) and require all summary mentions to reference task IDs. Use normalized enums: Status (OPEN/RESOLVED/REOPENED/NEEDS_MANUAL_VERIFICATION), Confidence (high/medium/low), Estimated Effort (S/M/L/XL). Update if exists.
```
