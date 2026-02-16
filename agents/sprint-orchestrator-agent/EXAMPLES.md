# Examples

Use these as starting points. Adapt sprint scope, dependencies, and merge policy to your repository.

## Example 1: Linear-First Sprint Orchestration

### Input
```text
Agent: sprint-orchestrator-agent
Goal: Orchestrate Sprint 31 from Jira export and publish role packets directly to Linear issues.
Inputs: Sprint task source: /inputs/jira/sprint-31.csv
Inputs: Agent root path: /agents
Inputs: Standards source: /agents/agent-making-agent/README.md
Inputs: tracking_mode: linear
Inputs: tracking_contract_path: /Users/slobodan/Projects/Agents/agents/_shared/TRACKING_MODE_CONTRACT.md
Inputs: linear_comment_schema_path: /Users/slobodan/Projects/Agents/agents/_shared/LINEAR_COMMENT_SCHEMA.md
Inputs: linear_workflow_path: /Users/slobodan/Projects/Agents/agents/_shared/LINEAR_WORKFLOW.md
Inputs: worktree_policy_path: /Users/slobodan/Projects/Agents/agents/_shared/WORKTREE_POLICY.md
Inputs: Team capacity constraints: max 5 active units, risk-first ordering.
Inputs: Merge mode: sequential
Inputs: review_required: false
Inputs: pr_base_branch: main
Inputs: Handoff policy: developer -> tester -> PR-ready (optional review only when requested)
Constraints: Planning/orchestration only. Do not execute task implementation. Publish `DEV_TASK` and `TEST_TASK` packets as `AGENT_EVENT_V1` comments on each Linear issue. Publish `REVIEW_TASK` only when explicitly requested. Create pull requests for done units and include task description + expected outcome from issue/task packet in PR body. Keep PR body intent-only and do not include git diff summaries.
Output: /reports/SPRINT_PLAN.md, /reports/SPRINT_ISSUE_PACKETS.md, /reports/SPRINT_MERGE_PLAN.md, /reports/SPRINT_MERGE_RESULT.md
```

### Expected Output
```text
Creates /reports/SPRINT_PLAN.md with UOW IDs, dependencies, priorities, and mapped agents.
Posts structured `DEV_TASK`/`TEST_TASK` packets to each issue with packet_version, and `REVIEW_TASK` only when requested.
Creates /reports/SPRINT_ISSUE_PACKETS.md manifest containing packet routing and versions.
Creates pull requests for done units and ensures PR body includes task description and expected outcome, without git diff summaries.
Creates /reports/SPRINT_MERGE_PLAN.md with deterministic merge order and gate checks.
Creates /reports/SPRINT_MERGE_RESULT.md for merge progress tracking.
```

## Example 2: Local Fallback Orchestration (No Linear)

### Input
```text
Agent: sprint-orchestrator-agent
Goal: Plan carry-over sprint work without Linear connectivity.
Inputs: Sprint task source: /inputs/backlog/carry-over.md
Inputs: Agent root path: /agents
Inputs: Standards source: /agents/agent-making-agent/README.md
Inputs: tracking_mode: local
Inputs: tracking_contract_path: /Users/slobodan/Projects/Agents/agents/_shared/TRACKING_MODE_CONTRACT.md
Inputs: linear_comment_schema_path: /Users/slobodan/Projects/Agents/agents/_shared/LINEAR_COMMENT_SCHEMA.md
Inputs: linear_workflow_path: /Users/slobodan/Projects/Agents/agents/_shared/LINEAR_WORKFLOW.md
Inputs: worktree_policy_path: /Users/slobodan/Projects/Agents/agents/_shared/WORKTREE_POLICY.md
Inputs: Team capacity constraints: max 3 parallel units.
Inputs: Merge mode: batch
Inputs: review_required: true
Inputs: pr_base_branch: main
Inputs: Handoff policy: developer -> tester -> review -> PR-ready
Constraints: Planning/orchestration only. Write packet files under `/reports/issues/<ISSUE-ID>/` and initialize local state/event files. Create pull requests for done units and include task description + expected outcome from local issue packet in PR body. Keep PR body intent-only and do not include git diff summaries.
Output: /reports/SPRINT_PLAN.md, /reports/SPRINT_ISSUE_PACKETS.md, /reports/SPRINT_MERGE_PLAN.md, /reports/SPRINT_MERGE_RESULT.md
```

### Expected Output
```text
Creates /reports/SPRINT_PLAN.md with UOW IDs and routing.
Creates per-issue packet files (`DEV_TASK.yaml`, `TEST_TASK.yaml`, and optional `REVIEW_TASK.yaml` when requested) under /reports/issues/<ISSUE-ID>/.
Initializes /reports/issues/<ISSUE-ID>/state.yaml and /reports/issues/<ISSUE-ID>/events.jsonl.
Creates pull requests for done units with task description and expected outcome in PR body, without git diff summaries.
Creates /reports/SPRINT_ISSUE_PACKETS.md manifest and merge plan/result reports.
```
