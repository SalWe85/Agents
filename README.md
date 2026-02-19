# Agents Repository

This repository is a documentation-first project for building and organizing software agents.

There is no application code here.  
Instead, this repo stores:

- Agent definitions and plans
- Reusable instructions and templates
- Tutorials for creating and using agents effectively

## Project Goals

- Keep agent work structured and easy to browse
- Make onboarding simple for programmers new to agents
- Capture standards so future agents are consistent and useful

## Folder Structure

```text
.
├── agents/
│   ├── agent-making-agent/
│   │   └── README.md
│   └── agent-reviewing-agent/
│       └── README.md
└── guides/
    ├── AGENT_MAKING_INSTRUCTIONS.md
    └── AGENT_USING_INSTRUCTIONS.md
```

## First Agent: Agent Making Agent

The first agent in this repository is **Agent Making Agent**.

Its purpose is to define what all future agents should include:

- Clear purpose
- Well-scoped responsibilities
- Inputs and outputs
- Constraints and safety boundaries
- Verification and quality checks

See `/agents/agent-making-agent/README.md` for the full checklist.

## Getting Started

1. Initialize git:
   ```bash
   git init
   ```
2. Add files:
   ```bash
   git add .
   ```
3. Create first commit:
   ```bash
   git commit -m "Initialize agents documentation repository"
   ```

## How to Work in This Repo

1. Define a new agent folder under `/agents`.
2. Use the guide in `/guides/AGENT_MAKING_INSTRUCTIONS.md`.
3. Document how the agent should be used and validated.
4. Keep changes small and commit frequently.

## Shared Linear Workflow

If you use Linear, keep workflow statuses in one place:

- `/Users/slobodan/Projects/Agents/agents/_shared/LINEAR_WORKFLOW.md`

Agents that synchronize Linear state should receive:

- `Inputs: linear_workflow_path: /Users/slobodan/Projects/Agents/agents/_shared/LINEAR_WORKFLOW.md`

Update that single file when your Linear status names change (for example `Agent work DONE`, `Agent testing`, `Agent test DONE`), then rerun agents without editing each agent definition.

## Shared Worktree Policy

If you run agents in parallel worktrees, keep worktree behavior in one place:

- `/Users/slobodan/Projects/Agents/agents/_shared/WORKTREE_POLICY.md`

Agents should receive:

- `Inputs: worktree_policy_path: /Users/slobodan/Projects/Agents/agents/_shared/WORKTREE_POLICY.md`

Default behavior:
- Never create a new worktree without explicit user permission.
- If branch switch is blocked and a safe checkpoint commit resolves it, commit with a clear message and continue.
- If safe commit is unclear, stop and ask the user how to proceed.

## Recommended Naming Conventions

- Agent folders: lowercase-kebab-case (example: `bug-finder-agent`)
- Docs: UPPER_SNAKE_CASE for top-level guides, `README.md` inside each agent folder
- Checklists: `CHECKLIST.md` when needed per agent

## Next Step

Use **Agent Making Agent** to create a standard template, then build your second agent using that template.

## Credits

- Made by Slobodan Margetic
- Contact: slobodanmargetic988@gmail.com
