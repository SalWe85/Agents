# Usage Template

## Blank Template
```text
Agent: sprint-orchestrator-agent
Goal: Sprint source to orchestrate:
Inputs: Sprint task source:
Inputs: Agent root path: /agents
Inputs: Standards source: /agents/agent-making-agent/README.md
Inputs: Team capacity constraints:
Inputs: Merge mode: sequential
Inputs: Handoff policy: developer -> tester -> review-ready (skip tester only for no-test-surface tasks)
Constraints: Planning only. Do not execute subagent implementation work.
Output: /reports/SPRINT_PLAN.md, /reports/SPRINT_AGENT_ACTIVATIONS.md, /reports/SPRINT_EXECUTION_LOG.md, /reports/SPRINT_MERGE_PLAN.md, and /reports/SPRINT_MERGE_RESULT.md
```

## Filled Example
```text
Agent: sprint-orchestrator-agent
Goal: Orchestrate Sprint 24 from Jira backlog export into executable parallel units.
Inputs: Sprint task source: /inputs/jira/sprint-24.csv
Inputs: Agent root path: /agents
Inputs: Standards source: /agents/agent-making-agent/README.md
Inputs: Team capacity constraints: max 6 parallel forks, prioritize platform stability work first.
Inputs: Merge mode: sequential
Inputs: Handoff policy: developer -> tester -> review-ready (skip tester only for no-test-surface tasks)
Constraints: Planning only. Do not execute subagent implementation work.
Output: /reports/SPRINT_PLAN.md, /reports/SPRINT_AGENT_ACTIVATIONS.md, /reports/SPRINT_EXECUTION_LOG.md, /reports/SPRINT_MERGE_PLAN.md, and /reports/SPRINT_MERGE_RESULT.md
```
