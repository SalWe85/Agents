# Examples

Use these as starting points. Review them carefully and adapt goals, inputs, and constraints to your own project.

## Example 1: Create a Testing Agent

### Input
```text
Agent: agent-making-agent
Goal: New agent to create: test-plan-agent
Inputs: Use /agents/agent-making-agent/README.md as the standards source.
Inputs: Additional context: focus test plans on API and DB changes.
Constraints: Documentation only, no code edits.
Output: three files in the new agent folder: README.md + USAGE_TEMPLATE.md + EXAMPLES.md
```

### Expected Output
```text
Creates /agents/test-plan-agent/README.md, /agents/test-plan-agent/USAGE_TEMPLATE.md, and /agents/test-plan-agent/EXAMPLES.md.
README.md includes required sections, hard gates, timestamp, and rubric.
USAGE_TEMPLATE.md is append-only and portable.
EXAMPLES.md has at least two diverse input/output examples and adaptation guidance.
```

## Example 2: Improve an Existing Agent

### Input
```text
Agent: agent-making-agent
Goal: Upgrade /agents/deployment-agent/ to match current standards.
Inputs: Existing files in /agents/deployment-agent/ and /agents/agent-making-agent/README.md.
Constraints: Keep original mission intact; only documentation changes.
Output: three-file compliant package for deployment-agent.
```

### Expected Output
```text
Updates deployment-agent to include README.md, USAGE_TEMPLATE.md, and EXAMPLES.md.
Adds missing hard-gate requirements and rubric visibility.
Rewrites usage template to append-only format with portable paths.
Provides diverse examples with user adaptation note.
```
