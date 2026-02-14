# Usage Template

## Blank Template
```text
Agent: <agent-folder-name>
Goal: <desired outcome>
Inputs: <files/paths/context>
Constraints: <limits/safety/rules>
Output: <two files: README.md and USAGE_TEMPLATE.md>
Done when: <acceptance condition>
```

## Filled Example
```text
Agent: agent-making-agent
Goal: Define a new agent that drafts release notes from merged pull requests.
Inputs: /Users/slobodan/Projects/Agents/guides/AGENT_MAKING_INSTRUCTIONS.md and repository standards.
Constraints: Documentation only, no code edits.
Output: New agent package with README.md (required sections, hard gates, visible rubric) and USAGE_TEMPLATE.md (blank + filled templates).
Done when: New agent includes both files, scores at least 14/16, and passes all hard gates.
```
