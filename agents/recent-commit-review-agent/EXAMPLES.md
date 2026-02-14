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
Each finding includes finding ID, priority, commit hash, file+line, issue summary, impact, recommended fix, confidence, status, and verification steps.
Top Urgent Items reference findings by ID and IDs match detailed finding blocks.
Merges duplicate findings across commits and records merge rationale.
Labels uncertain findings as NEEDS_MANUAL_VERIFICATION.
```

### Sample Finding List + Detail Snippet
```md
## Top Urgent Items
1. [P0-1] Add authorization check to billing export endpoint.
2. [P1-1] Harden retry error handling for transient payment failures.

## Findings

### P0

#### Finding P0-1
- **Finding ID:** P0-1
- **Priority:** P0
- **Commit hash:** a1b2c3d
- **File + line:** `src/api/billing/export.ts:88`
- **Issue summary:** Missing role validation before exporting billing data.
- **Impact:** Unauthorized data export risk.
- **Recommended fix:** Require explicit admin role and add negative authorization test.
- **Confidence:** high
- **Verification steps:** Verify non-admin request returns 403 and admin path still succeeds.
- **Status:** OPEN
```

## Example 2: Date-Based Re-review of Resolved Findings

### Input
```text
Agent: recent-commit-review-agent
Goal: Re-check only findings previously marked RESOLVED and confirm they are truly fixed.
Review mode: auto
Mode: re-review
Review window: since=2026-02-01
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
References each re-reviewed item by finding ID.
Preserves existing finding IDs without renumbering.
Leaves non-RESOLVED findings untouched in re-review scope.
```
