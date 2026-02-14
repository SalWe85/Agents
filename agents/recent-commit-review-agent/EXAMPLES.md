# Examples

Use these as starting points. Review and adapt them to your repository context, review goals, and risk tolerance.

## Example 1: Commit-Count Review (Recent Burst)

### Input
```text
Agent: recent-commit-review-agent
Goal: Review the latest implementation burst and identify urgent regressions first.
Review mode: auto
Mode: review
Review window: commits=12
Standards source: /agents/agent-making-agent/README.md
Primary deliverable: /reports/COMMIT_REVIEW_TASKS.md
Constraints:
- Exactly one selector in Review window: commits=<number> OR since=<YYYY-MM-DD>
- Read-only review. Do not modify source code.
Output: Executive summary, top urgent items, and prioritized findings with verification steps.
```

### Expected Output
```text
Writes /reports/COMMIT_REVIEW_TASKS.md.
Includes Executive Summary and Top Urgent Items.
Lists findings grouped and sorted by P0, P1, P2, P3.
Each finding includes priority, commit hash, file+line, issue summary, impact, recommended fix, confidence, and verification steps.
Merges duplicate findings across commits and records merge rationale.
Labels uncertain findings as needs manual verification.
```

## Example 2: Date-Based Re-review of Resolved Findings

### Input
```text
Agent: recent-commit-review-agent
Goal: Re-check only findings previously marked RESOLVED and confirm they are truly fixed.
Review mode: auto
Mode: re-review
Review window: since=2026-02-01
Standards source: /agents/agent-making-agent/README.md
Primary deliverable: /reports/COMMIT_REVIEW_TASKS.md
Constraints:
- Exactly one selector in Review window: commits=<number> OR since=<YYYY-MM-DD>
- Read-only review. Do not modify source code.
Output: Re-review validation results for RESOLVED findings only.
```

### Expected Output
```text
Reads /reports/COMMIT_REVIEW_TASKS.md and targets only findings marked RESOLVED.
Validates whether each resolved item is truly fixed in the current code state.
Marks each item as confirmed fixed or REOPENED with evidence.
Keeps report ordered by priority and preserves commit/file traceability.
Leaves non-RESOLVED findings untouched in re-review scope.
```
