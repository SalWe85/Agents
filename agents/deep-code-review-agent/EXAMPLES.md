# Examples

Use these as starting points. Review them carefully and adapt scope, module priorities, and constraints to your own repository and risk profile.

## Example 1: Full Deep Review of a Large Monorepo

### Input
```text
Agent: deep-code-review-agent
Goal: Run a deep code review of the monorepo after a long period without full-project review.
Mode: Full Review
Inputs: Repository root path: ./repo/commerce-monorepo
Inputs: Existing report path (required for Re-review): /reports/REVIEW_TASKS.md
Inputs: Optional focus modules or risk themes: checkout, inventory sync, shared auth middleware
Constraints: Read-only review. No code changes.
Output: /reports/REVIEW_TASKS.md with executive summary, top 10 urgent fixes, quick wins, prioritized tasks (P0-P3), needs manual verification, out-of-scope, and verification steps per task.
```

### Expected Output
```text
Creates /reports/REVIEW_TASKS.md.
Includes Executive Summary, Top 10 Urgent Fixes, Quick Wins, Tasks by Priority (P0-P3), Needs Manual Verification, and Out-of-Scope.
Findings are deduplicated by root cause and fix path.
Each task includes task ID, priority, title, impact, evidence (file + line), recommended fix, estimated effort (S/M/L/XL), confidence (high/medium/low), status (OPEN/RESOLVED/REOPENED/NEEDS_MANUAL_VERIFICATION), and verification steps.
Top 10 and Quick Wins reference tasks by ID (for example, [P0-1], [P1-2]) and those IDs match the detailed task blocks.
Large-repo chunking is visible in the report (module/phase review coverage).
```

### Sample Task List + Detail Snippet
```md
## Top 10 Urgent Fixes
1. [P0-1] Rotate exposed payment secret.
2. [P0-2] Enforce authorization on refund endpoint.

## Tasks by Priority

### P0

#### Task P0-1
- **Task ID:** P0-1
- **Priority:** P0
- **Title:** Rotate exposed payment secret
- **Impact:** Credential abuse can lead to fraudulent transactions.
- **Evidence:** `services/payments/config.ts:22`
- **Recommended Fix:** Rotate the secret and migrate to secure runtime secret injection.
- **Estimated Effort:** M
- **Confidence:** high
- **Status:** OPEN
- **Verification Steps:** Confirm old secret is revoked and related integration tests pass.
```

## Example 2: Re-review of Resolved Tasks Only

### Input
```text
Agent: deep-code-review-agent
Goal: Validate whether previously resolved high-priority tasks are truly fixed.
Mode: Re-review
Inputs: Repository root path: ./repo/commerce-monorepo
Inputs: Existing report path (required for Re-review): /reports/REVIEW_TASKS.md
Inputs: Optional focus modules or risk themes: only tasks marked RESOLVED in P0 and P1
Constraints: Read-only review. No code changes.
Output: /reports/REVIEW_TASKS.md updated with re-review outcomes for RESOLVED tasks.
```

### Expected Output
```text
Inspects only tasks marked RESOLVED in /reports/REVIEW_TASKS.md.
Marks each as RESOLVED, REOPENED, or NEEDS_MANUAL_VERIFICATION.
Attaches file+line evidence for each re-review decision.
References each re-reviewed item by its existing task ID (for example, P0-1, P1-4).
Preserves existing task IDs without renumbering.
Does not create new feature requests outside the RESOLVED-task validation scope.
Preserves read-only review behavior.
```
