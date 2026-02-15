# Team Presentation: Lecture + Workflow Lab (60-90 min)

Audience: engineers and tech leads who need enough technical depth to adopt this workflow safely.
Presenter goal: teach foundational mechanics first, then show practical execution flow with demos.

## 1) Session Outcomes
By the end, the team should be able to:
- Explain what Git worktrees are and why they matter for parallel Codex execution.
- Explain Codex primitives (`AGENTS.md`, Skills, MCP) and how your local `/agents` model fits with them.
- Understand the full lane model: developer -> tester -> review-ready.
- Apply the workflow in real sprint execution with orchestration and safety gates.

## 2) New Pace and Structure (3 Acts)

Act 1: Lecture Foundation
- Worktrees and thread isolation
- Failure modes and safety constraints

Act 2: Lecture Foundation
- Codex primitives (`AGENTS.md`, Skills, MCP)
- Your local agents compared to those primitives

Act 3: Workflow Lab
- End-to-end lane walkthrough using your agents
- Live demos and handoff states

## 3) Timing Options

### 60-minute version (foundation-heavy)
1. Intro and context: 5 min
2. Lecture A: Worktrees deep dive: 15 min
3. Lecture B: Agents vs Skills vs MCP deep dive: 15 min
4. Workflow map and lane model: 7 min
5. Demo sequence (compressed): 14 min
6. Q&A: 4 min

### 90-minute version (full depth)
1. Intro and context: 8 min
2. Lecture A: Worktrees deep dive: 22 min
3. Lecture B: Agents vs Skills vs MCP deep dive: 20 min
4. Workflow map and lane model: 10 min
5. Demo sequence (full): 22 min
6. Adoption plan + Q&A: 8 min

## 4) Presenter Setup
- Keep one narration thread.
- Keep one demo thread for background execution.
- If available, keep one app-repo thread for developer/tester lane demos.
- Open:
  - `/Users/slobodan/Projects/Agents/guides/USING_WORKTREES_AND_AGENT_THREADS.md`
  - `/Users/slobodan/Projects/Agents/guides/AGENT_MAKING_INSTRUCTIONS.md`
  - `/Users/slobodan/Projects/Agents/guides/AGENT_USING_INSTRUCTIONS.md`
  - `/Users/slobodan/Projects/Agents/guides/STACK_DESCRIPTION_FILE_STANDARD.md`
  - `/Users/slobodan/Projects/Agents/guides/TEAM_PRESENTATION_DEMO_RUNBOOK.md`

## 5) Slide Script

### Slide 1: Why This Session Starts with Infrastructure
Talking points:
- Adoption fails when people copy prompts without understanding execution context.
- We start with worktrees because parallel agent execution depends on clean isolation.
Interaction:
- Ask: "How many times have you seen parallel work collide in one branch/thread?"

### Slide 2: What a Git Worktree Actually Is
Talking points:
- One repository, multiple working directories tied to different branches/commits.
- Faster and safer than repeatedly stashing/switching in one folder.

### Slide 3: Why Worktrees Matter for Parallel Agents
Talking points:
- Each agent lane can run in isolated filesystem + branch context.
- Reduces cross-task file pollution and branch confusion.

### Slide 4: Thread-Worktree Pairing in Codex
Talking points:
- Prefer "Fork into new worktree" per parallel task.
- Forked threads inherit source context at fork time.
- Keep launcher thread lightweight to reduce context contamination.

### Slide 5: Detached HEAD and Orphan Commit Risk
Talking points:
- New worktrees may open detached.
- Detached is valid but risky for lost branch references.
- Attach a branch before edits: `git switch -c codex/<task-name>`.

### Slide 6: Cleanup and Lifecycle Safety
Talking points:
- Never delete worktree attached to active thread.
- Cleanup must happen after task completion and context move.
- Plan/apply model protects from accidental destructive cleanup.

### Slide 7: Transition to Codex Concepts
Talking points:
- Worktrees solve execution isolation.
- Next layer is behavioral control: what Codex is instructed to do and how.

### Slide 8: Codex Primitive 1 - `AGENTS.md`
Talking points:
- Defines repo-level behavior policy, constraints, and defaults.
- Controls how agent behaves inside this repository.

### Slide 9: Codex Primitive 2 - Skills
Talking points:
- Reusable capability packs (`SKILL.md`, scripts, assets).
- Great for repeatable workflows (Playwright, Linear, Figma, etc.).

### Slide 10: Codex Primitive 3 - MCP
Talking points:
- Tool integration protocol for external systems and context.
- Powers integrations like browser tooling, issue trackers, design tools.

### Slide 11: Your Local `/agents` Model
Talking points:
- Project-scoped operational contracts under `/agents`.
- Each agent has mission/scope/inputs/outputs/workflow/constraints/validation.
- Explicit invocation gives predictable, auditable behavior.

### Slide 12: Comparison Matrix
Talking points:
- `AGENTS.md` = policy layer.
- Skills = capability layer.
- MCP = integration/tool layer.
- Local `/agents` = workflow-contract layer for your organization.
Interaction:
- Ask: "Which layer is currently weakest in our team setup?"

### Slide 13: Quality Governance Loop
Talking points:
- `agent-making-agent` defines acceptance quality.
- `agent-reviewing-agent` enforces hard gates and rubric.

### Slide 14: Full Workflow Map (All Agents)
Talking points:
- Governance: `agent-making-agent`, `agent-reviewing-agent`.
- Orchestration: `sprint-orchestrator-agent`.
- Execution lanes: backend/frontend/fullstack developers + testers.
- Review gates: recent-commit + deep-code review agents.
- Hygiene: git-worktree cleanup.

### Slide 15: Lane State Model
Talking points:
- `codex_dev_done` -> `codex_test_done` -> `codex_review_ready`.
- Direct `codex_review_ready` only when no meaningful test surface exists.
Interaction:
- Ask: "What evidence do you require before accepting `codex_test_done`?"

### Slide 16: Demo Overview
Talking points:
- Background demos run while you narrate decisions and tradeoffs.
- Demos follow same order as real operations.

### Slide 17: Demo A (Governance)
Talking points:
- `agent-making-agent` and `agent-reviewing-agent` in action.
- Show pass/fail logic and top improvements.

### Slide 18: Demo B (Orchestration)
Talking points:
- `sprint-orchestrator-agent` generates UOWs, activations, execution log, merge plan.
- Show handoff fields and substatus expectations.

### Slide 19: Demo C (Developer + Tester Lanes)
Talking points:
- Backend lane: `backend-developer` -> `backend-tester`.
- Frontend lane: `frontend-developer` -> `frontend-tester`.
- Coupled lane: `fullstack-developer` with tester strategy.

### Slide 20: Demo D (Review Gates)
Talking points:
- `recent-commit-review-agent` for bounded change window.
- `deep-code-review-agent` for full read-only risk backlog.

### Slide 21: Demo E (Cleanup Safety)
Talking points:
- `git-worktree-cleanup-agent` plan mode, `plan_id`, and apply gates.
- Why destructive actions are intentionally harder.

### Slide 22: Adoption Blueprint
Talking points:
- Week 1: worktree discipline + governance gate.
- Week 2: orchestrator + one execution lane.
- Week 3: full lane model + review + cleanup cadence.

### Slide 23: Common Failure Patterns
Talking points:
- Vague prompts and unclear acceptance criteria.
- Missing stack description.
- Skipping state transitions in execution log.
- Treating demos as proof without validation evidence.

### Slide 24: Close
Talking points:
- Understanding the technical substrate is prerequisite for adoption.
- Success metric: predictable flow and safer parallel delivery.

## 6) Mandatory Lecture Messages
- Worktree isolation is not optional for parallel agents.
- Branch hygiene and task-scoped commits are process controls, not preferences.
- `AGENTS.md`, Skills, and MCP are complementary layers, not alternatives.
- Your `/agents` definitions are organization-specific operational contracts.

## 7) Interactive Prompts for Lecture Segments
- "What is our current equivalent of a lightweight launcher thread?"
- "Where do we currently lose task traceability across parallel work?"
- "Which of the four layers (policy, capability, integration, workflow-contract) needs immediate investment?"

## 8) Backup Plan
- If live demos fail, use existing reports and example outputs:
  - `/Users/slobodan/Projects/Agents/reports/ALL_AGENTS_REVIEW.md`
  - `/Users/slobodan/Projects/Agents/reports/GIT_CLEANUP_PLAN.md`
  - `/Users/slobodan/Projects/Agents/reports/GIT_CLEANUP_RESULT.md`
- Keep lecture sections intact; they do not depend on live execution.
