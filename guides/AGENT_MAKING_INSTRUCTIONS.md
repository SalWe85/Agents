# Agent Making Instructions

This guide teaches programmers who are new to agents how to design useful, reliable agents.

## What Is an Agent in This Repo?

In this project, an agent is a documented worker with:

- A clear mission
- Defined inputs
- Predictable outputs
- Boundaries and safety rules
- A repeatable workflow

If your agent cannot explain these five points, it is not ready.

## Design Principles

## 1) Keep Scope Narrow

Bad: “This agent does all backend tasks.”  
Good: “This agent writes migration plans for PostgreSQL schema changes.”

Small scope improves consistency and makes testing easier.

## 2) Prefer Deterministic Steps

Agents should follow explicit steps that can be reviewed.  
Avoid “figure it out dynamically” as a primary strategy.

## 3) Define Success Before Building

State what successful output looks like before writing instructions.

## 4) Make Failure Explicit

List known failure modes and fallback actions.

## 5) Design for New Contributors

Assume users do not know hidden team conventions.  
Write docs that are complete without extra chat context.

## Step-by-Step Workflow to Create a New Agent

## Step 1: Define Mission

Write a one-sentence mission:

- “This agent reviews pull requests for security regressions in Node.js APIs.”

Then define:

- In-scope tasks
- Out-of-scope tasks

If out-of-scope is missing, scope creep will happen.

## Step 2: Define Inputs and Outputs

Inputs should include:

- What the user provides
- What files are required
- What tools are allowed

Outputs should include:

- Format (markdown, patch, checklist, report)
- Location (stdout, specific file path)
- Quality bar (minimum required details)

## Step 3: Create Workflow

Write a numbered sequence:

1. Collect inputs
2. Validate prerequisites
3. Execute core task
4. Verify output
5. Report result and next steps

Include decision branches for common variations.

## Step 4: Add Constraints and Safety

Document:

- Commands/actions that require permission
- Prohibited/destructive operations
- Data handling limits

If the agent can produce side effects, this section is mandatory.

## Step 5: Add Validation Checks

Define how to verify result quality:

- Lint/test commands
- Manual review checklist
- Expected signs of correctness

No validation means no reliability.

## Step 6: Add Failure Handling

For each common failure:

- Failure signal
- Likely cause
- Recovery action

This prevents agents from failing silently.

## Recommended Agent README Structure

Every `agents/<name>/README.md` should include:

1. Mission
2. Scope (in/out)
3. Inputs
4. Outputs
5. Workflow
6. Constraints
7. Validation
8. Failure handling
9. Definition of done
10. Examples

## Quality Rubric (Score 0-2 Per Item)

- Purpose clarity
- Scope control
- Input completeness
- Output specificity
- Workflow determinism
- Safety coverage
- Validation quality
- Failure recovery clarity

Scoring:

- 0-7: Redesign required
- 8-13: Usable but weak
- 14-16: Good

## Common Mistakes and Fixes

- Mistake: Vague output (“provide summary”)
  Fix: define exact sections and minimum fields.
- Mistake: No out-of-scope definition
  Fix: add explicit exclusions.
- Mistake: No permission model
  Fix: list escalations and disallowed operations.
- Mistake: Overly broad tools
  Fix: constrain tools by task stage.
- Mistake: No examples
  Fix: add at least one input/output sample.

## Example Skeleton

```md
# API Security Review Agent

## Mission
Review API changes for authentication, authorization, and injection risks.

## In Scope
- Review changed routes and middleware
- Identify high-confidence security risks

## Out of Scope
- Infrastructure hardening
- Full penetration testing

## Inputs
- Pull request diff
- Relevant service configuration files

## Outputs
- Security findings report with severity, file, line, remediation

## Workflow
1. Collect changed files
2. Filter to API surface and auth logic
3. Evaluate security risk patterns
4. Produce findings with evidence
5. Summarize residual risk

## Constraints
- Do not suggest destructive commands
- Flag uncertain findings as “needs manual verification”

## Validation
- Ensure each finding has file path and concrete evidence

## Failure Handling
- If diff is missing, request it and stop

## Definition of Done
- Report includes prioritized findings and verification notes
```

## Publishing Checklist

Before finalizing a new agent:

- [ ] Passes Agent Agent acceptance checklist
- [ ] Has one realistic example
- [ ] Can be used by a new engineer without extra context
- [ ] Has clear stop conditions
- [ ] Includes at least one verification step
