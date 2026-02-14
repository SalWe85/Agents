# Usage Template

## Blank Template (PLAN)
```text
Agent: git-worktree-cleanup-agent
Goal: Clean Git worktrees and related branches with safety-first two-phase execution.
Inputs: repo_root:
Inputs: preserve_worktree_path:
Inputs: protected_branches: main,master,develop
Inputs: branch_cleanup_patterns: codex/*
Inputs: mode: plan
Inputs: allow_force_dirty_worktrees: false
Constraints: Discovery and report only. Do not delete anything.
Output: /reports/GIT_CLEANUP_PLAN.md
```

## Blank Template (APPLY)
```text
Agent: git-worktree-cleanup-agent
Goal: Execute approved cleanup plan after explicit confirmation.
Inputs: repo_root:
Inputs: preserve_worktree_path:
Inputs: protected_branches: main,master,develop
Inputs: branch_cleanup_patterns: codex/*
Inputs: mode: apply
Inputs: plan_id:
Inputs: confirmation_token:
Inputs: execute_confirmation: yes, execute cleanup
Inputs: allow_force_dirty_worktrees: false
Constraints: Abort on plan mismatch or missing confirmations.
Output: /reports/GIT_CLEANUP_RESULT.md
```

## Filled Example
```text
Agent: git-worktree-cleanup-agent
Goal: Clean merged codex worktrees while keeping main worktree.
Inputs: repo_root: /workspace/project
Inputs: preserve_worktree_path: /workspace/project
Inputs: protected_branches: main,master,develop,release
Inputs: branch_cleanup_patterns: codex/*
Inputs: mode: plan
Inputs: allow_force_dirty_worktrees: false
Constraints: Discovery and report only. Do not delete anything.
Output: /reports/GIT_CLEANUP_PLAN.md
```
