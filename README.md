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
│   └── agent-agent/
│       └── README.md
└── guides/
    ├── AGENT_MAKING_INSTRUCTIONS.md
    └── AGENT_USING_INSTRUCTIONS.md
```

## First Agent: Agent Agent

The first agent in this repository is **Agent Agent**.

Its purpose is to define what all future agents should include:

- Clear purpose
- Well-scoped responsibilities
- Inputs and outputs
- Constraints and safety boundaries
- Verification and quality checks

See `/agents/agent-agent/README.md` for the full checklist.

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

## Recommended Naming Conventions

- Agent folders: lowercase-kebab-case (example: `bug-finder-agent`)
- Docs: UPPER_SNAKE_CASE for top-level guides, `README.md` inside each agent folder
- Checklists: `CHECKLIST.md` when needed per agent

## Next Step

Use **Agent Agent** to create a standard template, then build your second agent using that template.
