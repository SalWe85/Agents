# Agent Agent

Agent Agent exists to define quality standards for all future agents in this repository.

If a new agent does not satisfy this checklist, it is not ready.

## Required Components for Every Agent

## 1) Identity and Purpose

- Agent name
- One-sentence mission
- Problems it solves
- Problems it does **not** solve

## 2) Inputs and Context

- Required inputs (files, prompts, parameters)
- Optional inputs
- Context sources it can use
- Assumptions about environment/tools

## 3) Outputs

- Expected output format
- Output location (if writing files)
- Success criteria (what “good output” means)

## 4) Scope and Boundaries

- In-scope tasks
- Out-of-scope tasks
- Safety constraints
- Permission/escalation rules

## 5) Workflow

- Step-by-step execution plan
- Decision points and fallback behavior
- Stop conditions
- Handoff rules (if multiple agents are involved)

## 6) Quality Controls

- Validation checklist before completion
- Common failure modes and how to detect them
- Testing/verification commands
- Definition of done

## 7) Collaboration Rules

- How the agent communicates progress
- How it asks clarification questions
- How it reports blockers
- How it summarizes completed work

## 8) Maintenance

- Version history section
- Known limitations
- TODO improvements
- Owner/maintainer

## Agent Acceptance Checklist

Use this quick gate before adding any new agent:

- [ ] Purpose is clear and narrow
- [ ] Inputs and outputs are documented
- [ ] Safety boundaries are explicit
- [ ] Workflow is deterministic enough to follow
- [ ] Verification steps are defined
- [ ] Failure handling is documented
- [ ] New contributor can use it without tribal knowledge

## Minimal Template for Future Agents

Copy this into `agents/<new-agent>/README.md`:

```md
# <Agent Name>

## Mission
<One sentence about what this agent does.>

## In Scope
- ...

## Out of Scope
- ...

## Inputs
- Required:
- Optional:

## Outputs
- Format:
- Location:

## Workflow
1. ...
2. ...
3. ...

## Constraints
- ...

## Validation
- Command/check:
- Expected result:

## Failure Handling
- If X happens, do Y.

## Definition of Done
- ...
```
