# Usage Template

## Blank Template
```text
Agent: recent-commit-review-agent
Goal:
Review mode: auto
Mode: review
Review window:
Primary deliverable: /reports/COMMIT_REVIEW_TASKS.md
Constraints:
- Exactly one selector in Review window: commits=<number> OR since=<YYYY-MM-DD>
- Read-only review. Do not modify source code.
Output: Executive summary, top urgent items, findings sorted P0-P3, duplicate-merge notes, and verification steps per finding. Require unique finding IDs (P0-1, P0-2, ...) and require all summary mentions to reference finding IDs. Use normalized status enum values (OPEN/RESOLVED/REOPENED/NEEDS_MANUAL_VERIFICATION).
```

## Filled Example
```text
Agent: recent-commit-review-agent
Goal: Review recent commits for high-impact defects and produce prioritized remediation tasks.
Review mode: auto
Mode: review
Review window: commits=8
Primary deliverable: /reports/COMMIT_REVIEW_TASKS.md
Constraints:
- Exactly one selector in Review window: commits=<number> OR since=<YYYY-MM-DD>
- Read-only review. Do not modify source code.
Output: Executive summary, top urgent items, findings sorted P0-P3, duplicate-merge notes, and verification steps per finding. Require unique finding IDs (P0-1, P0-2, ...) and require all summary mentions to reference finding IDs. Use normalized status enum values (OPEN/RESOLVED/REOPENED/NEEDS_MANUAL_VERIFICATION).
```
