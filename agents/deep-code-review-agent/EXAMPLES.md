# Examples

Use these as starting points. Review them carefully and adapt scope, module priorities, and constraints to your own repository and risk profile.

## Example 1: Full Deep Review of a Large Monorepo

### Input
```text
Agent: deep-code-review-agent
Goal: Run a deep code review of the monorepo after a long period without full-project review.
Mode: Full Review
Inputs: Repository root path: ./repo/commerce-monorepo
Inputs: Standards source: /agents/agent-making-agent/README.md
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
Each task includes priority, title, impact, evidence (file + line), recommended fix, estimated effort, confidence, and verification steps.
Large-repo chunking is visible in the report (module/phase review coverage).
```

## Example 2: Re-review of Resolved Tasks Only

### Input
```text
Agent: deep-code-review-agent
Goal: Validate whether previously resolved high-priority tasks are truly fixed.
Mode: Re-review
Inputs: Repository root path: ./repo/commerce-monorepo
Inputs: Standards source: /agents/agent-making-agent/README.md
Inputs: Existing report path (required for Re-review): /reports/REVIEW_TASKS.md
Inputs: Optional focus modules or risk themes: only tasks marked RESOLVED in P0 and P1
Constraints: Read-only review. No code changes.
Output: /reports/REVIEW_TASKS.md updated with re-review outcomes for RESOLVED tasks.
```

### Expected Output
```text
Inspects only tasks marked RESOLVED in /reports/REVIEW_TASKS.md.
Marks each as Verified Resolved, Still Open, or Needs Manual Verification.
Attaches file+line evidence for each re-review decision.
Does not create new feature requests outside the RESOLVED-task validation scope.
Preserves read-only review behavior.
```
