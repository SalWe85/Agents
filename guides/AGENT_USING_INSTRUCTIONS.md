# Agent Using Instructions

This guide explains how programmers new to agents should run agents effectively and get high-quality results.

## Core Idea

Agents are force multipliers, not magic.  
Quality depends on the quality of your task definition, constraints, and feedback loop.

## Before You Use an Agent

Prepare these five things first:

1. Goal: what outcome you need
2. Context: what files/systems matter
3. Constraints: what the agent must not do
4. Output format: how results should be delivered
5. Validation: how you will check correctness

If any are missing, results become noisy and unreliable.

## Prompting Pattern for Reliable Results

Use this structure:

```text
Goal:
<What you need done and why>

Context:
<Relevant files, stack, constraints, assumptions>

Task:
<Explicit requested actions>

Output Format:
<Exact format/sections>

Validation:
<Tests/checks the agent must run or criteria to satisfy>

Limits:
<Forbidden actions, time/space/tool constraints>
```

## Practical Example Prompt

```text
Goal:
Create onboarding docs for the new logging pipeline.

Context:
Repo uses Node.js 22, TypeScript, and pino.
Relevant files: src/logging.ts, docs/architecture.md

Task:
Draft docs with setup steps, examples, and troubleshooting.

Output Format:
Markdown with sections:
1) Purpose
2) Setup
3) Common Tasks
4) Troubleshooting

Validation:
Must include at least 2 runnable command examples.

Limits:
Do not change source code. Documentation changes only.
```

## How to Iterate with an Agent

Use short loops:

1. Ask for first draft
2. Review for correctness and omissions
3. Provide targeted feedback
4. Ask for revision
5. Approve or repeat

Targeted feedback example:

- “Section 3 needs concrete commands.”
- “Limit recommendations to tools already in package.json.”

Avoid vague feedback like “make it better.”

## Choosing the Right Agent

Pick based on scope:

- Planning agent for architecture and task breakdown
- Implementation agent for code changes
- Review agent for bug/risk detection
- Documentation agent for guides and onboarding material

Do not ask one agent to do everything in a single pass.

## Safety and Control Rules

Always specify:

- What it can edit
- What it cannot edit
- Whether network access is allowed
- Whether destructive actions are forbidden
- Whether approval is needed for privileged operations

If the task has production impact, require a dry-run plan first.

## Validation Checklist for Agent Output

Before accepting output:

- [ ] Task requirements were fully addressed
- [ ] Claims are supported by files or evidence
- [ ] Edge cases were considered
- [ ] Output format matches request
- [ ] Safety constraints were respected
- [ ] Verification steps were executed (if applicable)

## Common Failure Modes (and Fixes)

- Failure: Hallucinated files/functions
  Fix: require file references and check existence.
- Failure: Partial completion
  Fix: request checklist-based completion report.
- Failure: Ignored constraints
  Fix: restate constraints and require compliance section.
- Failure: Overly broad changes
  Fix: constrain files and expected diff size.
- Failure: No validation
  Fix: require explicit tests/checks and results.

## Beginner Workflow for Daily Use

1. Start with one clear task
2. Provide exact context paths
3. Ask for a plan if task is large
4. Approve the plan
5. Execute in small increments
6. Validate each increment
7. Commit only reviewed outputs

## Definition of a Good Agent Session

A good session ends with:

- Correct result
- Transparent reasoning
- Clear evidence or validation
- Minimal surprises
- Reusable output

## Quick Reference Card

- Be specific about goal and files
- Define output format up front
- Enforce constraints explicitly
- Iterate with precise feedback
- Validate before accepting
