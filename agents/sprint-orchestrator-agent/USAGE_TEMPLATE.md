# Usage Template

## Blank Template
```text
Agent: sprint-orchestrator-agent
Goal: Sprint source to orchestrate:
Inputs: Sprint task source:
Inputs: Agent root path: /agents
Inputs: Standards source: /agents/agent-making-agent/README.md
Inputs: Team capacity constraints:
Constraints: Planning only. Do not execute subagent implementation work.
Output: /reports/SPRINT_PLAN.md and /reports/SPRINT_AGENT_ACTIVATIONS.md
```

## Filled Example
```text
Agent: sprint-orchestrator-agent
Goal: Orchestrate Sprint 24 from Jira backlog export into executable parallel units.
Inputs: Sprint task source: /inputs/jira/sprint-24.csv
Inputs: Agent root path: /agents
Inputs: Standards source: /agents/agent-making-agent/README.md
Inputs: Team capacity constraints: max 6 parallel forks, prioritize platform stability work first.
Constraints: Planning only. Do not execute subagent implementation work.
Output: /reports/SPRINT_PLAN.md and /reports/SPRINT_AGENT_ACTIVATIONS.md
```
