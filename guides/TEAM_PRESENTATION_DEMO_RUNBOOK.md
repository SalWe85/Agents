# Team Presentation Demo Runbook (Lecture-First Version)

This runbook supports a lecture-first session. Use it to run demonstrations after conceptual deep dives.

## 1) Session Flow Alignment
Use this order to match the new pace:
1. Lecture A: worktrees and parallel execution mechanics
2. Lecture B: Codex primitives and local agent model
3. Workflow lab demos

## 2) Lecture A Support: Worktree Deep Dive Evidence
Run these quick terminal snippets during the lecture to make concepts concrete.

### Command A1: Show current branch and worktrees
```bash
git -C /Users/slobodan/Projects/Agents rev-parse --abbrev-ref HEAD
git -C /Users/slobodan/Projects/Agents worktree list --porcelain
```

What to explain:
- One repo can drive multiple directories.
- Why this is safer for parallel tasks than one working tree.

### Command A2: Show branch and detached-head risk cues
```bash
git -C /Users/slobodan/Projects/Agents branch -a
git -C /Users/slobodan/Projects/Agents status --short --branch
```

What to explain:
- Detached vs named branch implications.
- Why agents should attach task branches before edits.

### Lecture A Reference Source
- `/Users/slobodan/Projects/Agents/guides/USING_WORKTREES_AND_AGENT_THREADS.md`

## 3) Lecture B Support: Codex Layers and Your Local Model
Use these references while speaking (no heavy demo needed here).

### Source refs
- `/Users/slobodan/Projects/Agents/guides/USING_WORKTREES_AND_AGENT_THREADS.md` (AGENTS.md vs Skills vs MCP section)
- `/Users/slobodan/Projects/Agents/guides/AGENT_MAKING_INSTRUCTIONS.md`
- `/Users/slobodan/Projects/Agents/guides/AGENT_USING_INSTRUCTIONS.md`

### Must-cover comparison
- `AGENTS.md`: policy and behavior rules in repo context.
- Skills: reusable capability workflows.
- MCP: external tool/context integration.
- Local `/agents`: your team’s workflow contracts for predictable execution.

## 4) Workflow Lab: Full-Agent Demo Order
After lectures, run demos in this sequence.

### Demo 1: Governance (`agent-making-agent`)
```text
Agent: agent-making-agent
Goal: Evaluate whether backend-developer package satisfies mandatory standards and hard gates.
Inputs: Candidate agent folder path under agents/: /Users/slobodan/Projects/Agents/agents/backend-developer
Inputs: Candidate README.md content: /Users/slobodan/Projects/Agents/agents/backend-developer/README.md
Inputs: Candidate USAGE_TEMPLATE.md content: /Users/slobodan/Projects/Agents/agents/backend-developer/USAGE_TEMPLATE.md
Inputs: Candidate EXAMPLES.md content: /Users/slobodan/Projects/Agents/agents/backend-developer/EXAMPLES.md
Output:
- PASS/FAIL
- rubric breakdown
- top 3 improvements
Constraints:
- Use /Users/slobodan/Projects/Agents/agents/agent-making-agent/README.md as canonical standard.
```

### Demo 2: Governance Cross-check (`agent-reviewing-agent`)
```text
Agent: agent-reviewing-agent
Goal: Review fullstack-developer package and report standards compliance.
Inputs: Target agent folder path: /Users/slobodan/Projects/Agents/agents/fullstack-developer
Inputs: Standards source: /Users/slobodan/Projects/Agents/agents/agent-making-agent/README.md
Output format:
- findings by severity
- file completeness
- rubric score
- total and PASS/FAIL
- top improvements
Constraints:
- evidence only from files
- no edits
```

### Demo 3: Orchestration (`sprint-orchestrator-agent`)
```text
Agent: sprint-orchestrator-agent
Goal: Build orchestrated sprint execution using all lanes and substatus handoffs.
Inputs: Sprint task source: /Users/slobodan/Projects/Agents/guides/presentation-assets/sprint-demo-backlog.md
Inputs: Agent root path: /Users/slobodan/Projects/Agents/agents
Inputs: Standards source: /Users/slobodan/Projects/Agents/agents/agent-making-agent/README.md
Inputs: Team capacity constraints: max 4 parallel forks, risk-first ordering.
Inputs: Merge mode: sequential
Inputs: Handoff policy: developer -> tester -> review-ready (skip tester only for no-test-surface tasks)
Constraints: Planning only. Do not execute implementation.
Output:
- /Users/slobodan/Projects/Agents/reports/SPRINT_PLAN.md
- /Users/slobodan/Projects/Agents/reports/SPRINT_AGENT_ACTIVATIONS.md
- /Users/slobodan/Projects/Agents/reports/SPRINT_EXECUTION_LOG.md
- /Users/slobodan/Projects/Agents/reports/SPRINT_MERGE_PLAN.md
- /Users/slobodan/Projects/Agents/reports/SPRINT_MERGE_RESULT.md
```

What to show:
- lane assignment logic
- `codex_dev_done` -> `codex_test_done` -> `codex_review_ready`

### Demo 4: Backend Lane (`backend-developer` -> `backend-tester`)
Use a real app repo when available (`DEMO_APP_REPO`).

```text
Agent: backend-developer
Goal: Implement API idempotency fix for webhook flow.
Inputs: task_identifier: DEMO-BE-01
Inputs: repo_root: DEMO_APP_REPO
Inputs: default_branch: main
Inputs: acceptance_criteria: duplicate deliveries do not duplicate side effects.
Inputs: stack_file_path: DEMO_APP_REPO/STACK.md
Inputs: task_list_path: DEMO_APP_REPO/reports/SPRINT_EXECUTION_LOG.md
Inputs: branch_name: codex/demo-be-01-idempotency
Inputs: commit_mode: commit
Constraints:
- implement directly
- include task id in commit messages
- run lint/test/build checks
- set codex_dev_done and hand off to backend-tester
```

```text
Agent: backend-tester
Goal: Validate DEMO-BE-01 with fullest feasible test suite.
Inputs: task_identifier: DEMO-BE-01
Inputs: repo_root: DEMO_APP_REPO
Inputs: default_branch: main
Inputs: test_target: changed backend modules/endpoints
Inputs: stack_file_path: DEMO_APP_REPO/STACK.md
Inputs: harness_mode: developer_handoff
Inputs: task_list_path: DEMO_APP_REPO/reports/SPRINT_EXECUTION_LOG.md
Inputs: commit_mode: commit
Constraints:
- run fullest feasible suite
- write /reports/BACKEND_TEST_REPORT.md
- set codex_test_done then codex_review_ready on pass
```

### Demo 5: Frontend Lane (`frontend-developer` -> `frontend-tester`)
```text
Agent: frontend-developer
Goal: Implement keyboard-accessible filter drawer and persistence.
Inputs: task_identifier: DEMO-FE-01
Inputs: repo_root: DEMO_APP_REPO
Inputs: default_branch: main
Inputs: acceptance_criteria: keyboard nav and persisted filters work without regressions.
Inputs: stack_file_path: DEMO_APP_REPO/STACK.md
Inputs: task_list_path: DEMO_APP_REPO/reports/SPRINT_EXECUTION_LOG.md
Inputs: branch_name: codex/demo-fe-01-filter-drawer
Inputs: commit_mode: commit
Constraints:
- implement directly
- run lint/typecheck/test/build checks
- set codex_dev_done and hand off to frontend-tester
```

```text
Agent: frontend-tester
Goal: Validate DEMO-FE-01 behavior with reproducible evidence.
Inputs: target URL/environment: <demo-url>
Inputs: test scope: keyboard nav, persistence, responsive behavior
Inputs: browser mode preferences: headed
Output: /reports/FRONTEND_TEST_REPORT.md
```

### Demo 6: Fullstack Lane (`fullstack-developer`)
```text
Agent: fullstack-developer
Goal: Implement cancellation flow across API and UI.
Inputs: task_identifier: DEMO-FS-01
Inputs: repo_root: DEMO_APP_REPO
Inputs: default_branch: main
Inputs: acceptance_criteria: state transitions are consistent and UI reflects terminal state.
Inputs: stack_file_path: DEMO_APP_REPO/STACK.md
Inputs: task_list_path: DEMO_APP_REPO/reports/SPRINT_EXECUTION_LOG.md
Inputs: tester_strategy: both
Inputs: branch_name: codex/demo-fs-01-cancel-flow
Inputs: commit_mode: commit
Constraints:
- implement backend and frontend directly
- run checks for touched layers
- set codex_dev_done and hand off to tester lanes
```

### Demo 7: Review Gates (`recent-commit-review-agent`, `deep-code-review-agent`)
```text
Agent: recent-commit-review-agent
Goal: Review recent commit window and produce prioritized findings.
Review mode: auto
Mode: review
Review window: commits=8
Primary deliverable: /Users/slobodan/Projects/Agents/reports/COMMIT_REVIEW_TASKS.md
Constraints:
- exactly one selector
- read-only
```

```text
Agent: deep-code-review-agent
Goal: Run full read-only review and produce remediation backlog.
Inputs: Repository root path to review: /Users/slobodan/Projects/Agents
Inputs: Review mode: Full Review
Output: /Users/slobodan/Projects/Agents/reports/REVIEW_TASKS.md
Constraints:
- read-only review
```

### Demo 8: Cleanup Safety (`git-worktree-cleanup-agent`)
```text
Agent: git-worktree-cleanup-agent
Goal: Produce plan-only cleanup for stale codex worktrees/branches.
Inputs: repo_root: /Users/slobodan/Projects/Agents
Inputs: preserve_worktree_path: /Users/slobodan/Projects/Agents
Inputs: protected_branches: main,master,develop
Inputs: branch_cleanup_patterns: codex/*
Inputs: mode: plan
Inputs: allow_force_dirty_worktrees: false
Constraints: report only, no deletions
Output: /Users/slobodan/Projects/Agents/reports/GIT_CLEANUP_PLAN.md
```

## 5) Lecture Interaction Prompts
- "What would break if two agents worked in the same tree and branch?"
- "Where should we enforce branch and commit policy: agent contract, repo policy, or both?"
- "What is our minimum evidence bar for moving to `codex_review_ready`?"

## 6) Fallback Plan
- If app-repo execution is unavailable, keep lectures full depth and run only repo-local demos.
- Use these artifacts as evidence:
  - `/Users/slobodan/Projects/Agents/reports/ALL_AGENTS_REVIEW.md`
  - `/Users/slobodan/Projects/Agents/reports/GIT_CLEANUP_PLAN.md`
  - `/Users/slobodan/Projects/Agents/reports/GIT_CLEANUP_RESULT.md`
