# Usage Template

## Blank Template
```text
Agent: agent-reviewing-agent
Goal: <what agent package should be reviewed>
Inputs: <target agent folder + standards to apply>
Constraints: <review-only limits, no-edit rules if needed>
Output: <desired format, e.g. findings + rubric>
Done when: <clear acceptance condition>
```

## Filled Example
```text
Agent: agent-reviewing-agent
Goal: Review /Users/slobodan/Projects/Agents/agents/new-agent/ for standard compliance.
Inputs: Use /Users/slobodan/Projects/Agents/guides/AGENT_MAKING_INSTRUCTIONS.md and /Users/slobodan/Projects/Agents/agents/agent-making-agent/README.md as the standard.
Constraints: Review only, no file edits.
Output: Missing-file check for README.md and USAGE_TEMPLATE.md, findings by severity, rubric scores (0-2 each), total score (X/16), PASS/FAIL, and top 3 improvements.
Done when: I can decide immediately whether to accept this agent.
```
