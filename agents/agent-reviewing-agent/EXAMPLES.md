# Examples

Use these as starting points. Review them carefully and adapt paths, standards, and strictness to your own project.

## Example 1: Review a Brand-New Agent

### Input
```text
Agent: agent-reviewing-agent
Goal: Review /agents/new-agent/ for standards compliance.
Inputs: Use /agents/agent-making-agent/README.md as the standards source.
Constraints: Review only, no file edits.
Output: findings + rubric
```

### Expected Output
```text
Returns file completeness status for README.md, USAGE_TEMPLATE.md, and EXAMPLES.md.
Shows rubric criterion scores, total score, and PASS/FAIL.
Lists top 3 concrete improvements.
```

## Example 2: Strict Template Quality Review

### Input
```text
Agent: agent-reviewing-agent
Goal: Review /agents/api-security-agent/ focusing on template usability and portability.
Inputs: Use /agents/agent-making-agent/README.md as the standards source.
Constraints: Review only; fail if templates require replacement text or absolute local paths.
Output: findings + rubric + hard-gate failures
```

### Expected Output
```text
Flags placeholder-based templates that require user deletion/replacement.
Flags machine-specific absolute paths.
Verifies EXAMPLES.md has at least two diverse scenarios and adaptation guidance.
Produces PASS/FAIL with precise remediation steps.
```
