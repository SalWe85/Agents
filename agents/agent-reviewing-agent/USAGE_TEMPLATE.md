# Usage Template

## Blank Template
```text
Agent: agent-reviewing-agent
Goal: Package to be reviewed:
Inputs: Use /agents/agent-making-agent/README.md as the standards source.
Constraints: Review only, no file edits.
Output: findings + rubric
```

## Filled Example
```text
Agent: agent-reviewing-agent
Goal: Review /agents/new-agent/ for standard compliance.
Inputs: Use /agents/agent-making-agent/README.md as the standards source.
Constraints: Review only, no file edits.
Output: Missing-file check for README.md, USAGE_TEMPLATE.md, and EXAMPLES.md; findings by severity; rubric scores (0-2 each); total score (X/16); PASS/FAIL; and top 3 improvements.
```
