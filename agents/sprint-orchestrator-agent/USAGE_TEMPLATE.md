# Usage Template

## Blank Template
```text
Agent: sprint-orchestrator-agent
Goal: Sprint source to orchestrate:
Inputs: Sprint task source:
Inputs: Agent root path: /agents
Inputs: Standards source: /agents/agent-making-agent/README.md
Inputs: tracking_mode: linear
Inputs: tracking_contract_path: /Users/slobodan/Projects/Agents/agents/_shared/TRACKING_MODE_CONTRACT.md
Inputs: linear_comment_schema_path: /Users/slobodan/Projects/Agents/agents/_shared/LINEAR_COMMENT_SCHEMA.md
Inputs: linear_workflow_path: /Users/slobodan/Projects/Agents/agents/_shared/LINEAR_WORKFLOW.md
Inputs: worktree_policy_path: /Users/slobodan/Projects/Agents/agents/_shared/WORKTREE_POLICY.md
Inputs: Team capacity constraints:
Inputs: Merge mode: sequential
Inputs: review_required: false
Inputs: pr_base_branch: main
Inputs: Handoff policy: developer -> tester -> PR-ready (optional review only when requested)
Constraints: Planning/orchestration only. Do not execute subagent implementation work. Include `tracking_mode`, `linear_workflow_path`, `worktree_policy_path`, `tracking_contract_path`, and `linear_comment_schema_path` in all generated worker task packets. In `tracking_mode=linear`, post structured `DEV_TASK` / `TEST_TASK` comments on each issue and add `REVIEW_TASK` only when `review_required=true` or explicitly requested. In `tracking_mode=local`, write per-issue packet files under `/reports/issues/<ISSUE-ID>/`. Create PRs for done units and include task description plus expected outcome (from issue/task packet) in each PR body. PR body must be intent-only context and must not include git diff summaries.
Output: /reports/SPRINT_PLAN.md, /reports/SPRINT_ISSUE_PACKETS.md, /reports/SPRINT_MERGE_PLAN.md, and /reports/SPRINT_MERGE_RESULT.md (optional snapshot only: /reports/SPRINT_EXECUTION_LOG.md)
```

## Filled Example
```text
Agent: sprint-orchestrator-agent
Goal: Orchestrate Sprint 24 from Jira backlog export into executable parallel units.
Inputs: Sprint task source: /inputs/jira/sprint-24.csv
Inputs: Agent root path: /agents
Inputs: Standards source: /agents/agent-making-agent/README.md
Inputs: tracking_mode: linear
Inputs: tracking_contract_path: /Users/slobodan/Projects/Agents/agents/_shared/TRACKING_MODE_CONTRACT.md
Inputs: linear_comment_schema_path: /Users/slobodan/Projects/Agents/agents/_shared/LINEAR_COMMENT_SCHEMA.md
Inputs: linear_workflow_path: /Users/slobodan/Projects/Agents/agents/_shared/LINEAR_WORKFLOW.md
Inputs: worktree_policy_path: /Users/slobodan/Projects/Agents/agents/_shared/WORKTREE_POLICY.md
Inputs: Team capacity constraints: max 6 parallel forks, prioritize platform stability work first.
Inputs: Merge mode: sequential
Inputs: review_required: false
Inputs: pr_base_branch: main
Inputs: Handoff policy: developer -> tester -> PR-ready (optional review only when requested)
Constraints: Planning/orchestration only. Do not execute subagent implementation work. Include `tracking_mode`, `linear_workflow_path`, `worktree_policy_path`, `tracking_contract_path`, and `linear_comment_schema_path` in all generated worker task packets. In `tracking_mode=linear`, post structured `DEV_TASK` / `TEST_TASK` comments on each issue and add `REVIEW_TASK` only when `review_required=true` or explicitly requested. In `tracking_mode=local`, write per-issue packet files under `/reports/issues/<ISSUE-ID>/`. Create PRs for done units and include task description plus expected outcome (from issue/task packet) in each PR body. PR body must be intent-only context and must not include git diff summaries.
Output: /reports/SPRINT_PLAN.md, /reports/SPRINT_ISSUE_PACKETS.md, /reports/SPRINT_MERGE_PLAN.md, and /reports/SPRINT_MERGE_RESULT.md (optional snapshot only: /reports/SPRINT_EXECUTION_LOG.md)
```
