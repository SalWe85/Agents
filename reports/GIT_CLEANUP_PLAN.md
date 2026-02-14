# Git Cleanup Plan

- Timestamp: 2026-02-14 22:28 CET
- Plan ID: PLAN-20260214-0fc36553
- Repo Path: /Users/slobodan/Projects/Agents
- Mode: plan
- Preserve Worktree Path: /Users/slobodan/Projects/Agents
- Protected Branches: main, master, develop
- Branch Cleanup Patterns: codex/*
- allow_force_dirty_worktrees: false

## Risk Warning
This plan contains destructive actions for worktree and branch deletion. Do not execute apply mode unless this plan has been reviewed and explicitly confirmed.

## Detected Worktrees
- KEEP: /Users/slobodan/Projects/Agents (branch: main)
- CANDIDATE_DELETE: /Users/slobodan/.codex/worktrees/2028/Agents (branch: codex/worktree-ui-test)
- CANDIDATE_DELETE: /Users/slobodan/Projects/agents-eldertree (branch: codex/agents-eldertree)
- CANDIDATE_DELETE: /Users/slobodan/Projects/Agents-wt-recent-review (branch: codex/recent-commit-review-agent)

## Detected Candidate Branches (Local)
- CANDIDATE_DELETE: codex/agents-eldertree (merged into main)
- CANDIDATE_DELETE: codex/recent-commit-review-agent (merged into main)
- CANDIDATE_DELETE: codex/testing (merged into main)
- CANDIDATE_DELETE: codex/worktree-ui-test (merged into main)

## Protected Items
- Protected branches:
  - main
  - master
  - develop
- Preserved worktree:
  - /Users/slobodan/Projects/Agents

## Actions To Execute In Apply Mode
1. Remove worktrees:
   - git -C /Users/slobodan/Projects/Agents worktree remove /Users/slobodan/.codex/worktrees/2028/Agents
   - git -C /Users/slobodan/Projects/Agents worktree remove /Users/slobodan/Projects/agents-eldertree
   - git -C /Users/slobodan/Projects/Agents worktree remove /Users/slobodan/Projects/Agents-wt-recent-review
2. Delete local branches after successful worktree removal and revalidation:
   - git -C /Users/slobodan/Projects/Agents branch -d codex/agents-eldertree
   - git -C /Users/slobodan/Projects/Agents branch -d codex/recent-commit-review-agent
   - git -C /Users/slobodan/Projects/Agents branch -d codex/testing
   - git -C /Users/slobodan/Projects/Agents branch -d codex/worktree-ui-test

## Actions Skipped + Reason
- SKIP remote branch deletion (origin/codex/*): remote deletion not enabled in this plan; local cleanup only.
- SKIP preserved worktree /Users/slobodan/Projects/Agents: explicitly preserved.
- SKIP protected branches main, master, develop: protected branch policy.

## Revalidation Requirements For Apply
Apply must supply all of the following:
- plan_id = PLAN-20260214-0fc36553
- confirmation_token = <user-provided token>
- execute_confirmation = yes, execute cleanup

Abort apply if any mismatch is detected:
- worktree list changed
- branch merge status changed
- protected branch set changed
- preserve path no longer valid

## Notes
- Main worktree currently has untracked reports/ content, but this does not block cleanup because main worktree is preserved.
