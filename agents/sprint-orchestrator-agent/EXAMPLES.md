# Examples

Use these as starting points. Review them carefully and adapt sprint scope, constraints, and execution waves to your project.

## Example 1: Full Sprint Jira Orchestration

### Input
```text
Agent: sprint-orchestrator-agent
Goal: Plan Sprint 31 from Jira export and prepare agent activation prompts.
Inputs: Sprint task source: /inputs/jira/sprint-31.csv
Inputs: Agent root path: /agents
Inputs: Standards source: /agents/agent-making-agent/README.md
Inputs: Team capacity constraints: 8 engineers, max 5 parallel forks.
Inputs: Merge mode: sequential
Constraints: Planning only. Do not execute subagent implementation work.
Output: /reports/SPRINT_PLAN.md, /reports/SPRINT_AGENT_ACTIVATIONS.md, /reports/SPRINT_EXECUTION_LOG.md, /reports/SPRINT_MERGE_PLAN.md, and /reports/SPRINT_MERGE_RESULT.md
```

### Expected Output
```text
Creates /reports/SPRINT_PLAN.md with UOW-001..UOW-0NN, dependencies, priorities, and execution waves.
Creates /reports/SPRINT_AGENT_ACTIVATIONS.md with one filled activation prompt per UOW and FORK-UOW identifiers.
Creates /reports/SPRINT_EXECUTION_LOG.md with branch, owner, status, PR, base/head sha, and merge status per UOW.
Creates /reports/SPRINT_MERGE_PLAN.md with merge mode, merge order, and merge gate checks.
Creates /reports/SPRINT_MERGE_RESULT.md for merged/skipped/blocked tracking.
Includes warning that forked threads inherit context and recommends forking subagents from a lightweight launcher thread.
```

## Example 2: Partial Replan For Carry-Over Tickets

### Input
```text
Agent: sprint-orchestrator-agent
Goal: Replan unresolved tickets from previous sprint into a reduced two-week execution plan.
Inputs: Sprint task source: /inputs/backlog/carry-over.md
Inputs: Agent root path: /agents
Inputs: Standards source: /agents/agent-making-agent/README.md
Inputs: Team capacity constraints: 3 parallel forks max, risk-first ordering.
Inputs: Merge mode: batch
Constraints: Planning only. No task execution.
Output: /reports/SPRINT_PLAN.md, /reports/SPRINT_AGENT_ACTIVATIONS.md, /reports/SPRINT_EXECUTION_LOG.md, /reports/SPRINT_MERGE_PLAN.md, and /reports/SPRINT_MERGE_RESULT.md
```

### Expected Output
```text
Produces compact plan focused on high-priority carry-over units with explicit UOW IDs.
Maps each unit to the best-fit existing agent and marks unmapped work clearly.
Generates ready-to-use activation prompts with branch suggestions and confirmation checklist.
Includes batch merge waves and blocked-item tracking in merge reports.
```
