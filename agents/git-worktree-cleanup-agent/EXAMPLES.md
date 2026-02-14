# Examples

Use these as starting points. Review them carefully and adapt paths, branch protections, and cleanup scope to your own repository and risk tolerance.

## Example 1: Plan-Only Cleanup for Multiple Codex Worktrees

### Input
```text
Agent: git-worktree-cleanup-agent
Goal: Produce cleanup plan for stale codex worktrees.
Inputs: repo_root: /workspace/project
Inputs: preserve_worktree_path: /workspace/project
Inputs: protected_branches: main,master,develop,release
Inputs: branch_cleanup_patterns: codex/*
Inputs: mode: plan
Inputs: allow_force_dirty_worktrees: false
Constraints: Discovery only; no deletions.
Output: /reports/GIT_CLEANUP_PLAN.md
```

### Expected Output
```text
Creates /reports/GIT_CLEANUP_PLAN.md with:
- timestamp and repo path
- all detected worktrees
- candidate codex/* branches
- exact keep/delete lists
- skipped actions with reasons (for example dirty worktree or protected branch)
- risk warning and generated plan_id
No destructive actions executed.
```

## Example 2: Apply Attempt Aborted by Plan Mismatch

### Input
```text
Agent: git-worktree-cleanup-agent
Goal: Execute previously approved cleanup.
Inputs: repo_root: /workspace/project
Inputs: preserve_worktree_path: /workspace/project
Inputs: protected_branches: main,master,develop,release
Inputs: branch_cleanup_patterns: codex/*
Inputs: mode: apply
Inputs: plan_id: 2026-02-14T1800Z-abc123
Inputs: confirmation_token: CLEANUP-2026-02-14
Inputs: execute_confirmation: yes, execute cleanup
Inputs: allow_force_dirty_worktrees: false
Constraints: Abort if repository state changed since plan.
Output: /reports/GIT_CLEANUP_RESULT.md
```

### Expected Output
```text
Creates /reports/GIT_CLEANUP_RESULT.md with:
- revalidation failure details (state mismatch from plan snapshot)
- no deletions performed
- skipped actions with reasons
- guidance to generate a fresh plan
- rollback guidance section (reflog-based recovery steps)
```
