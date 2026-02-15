# Sprint Demo Backlog (All-Agent Workflow)

Use this input with `sprint-orchestrator-agent` to demonstrate complete handoff flow.

## Sprint Context
- Sprint Name: Agent Ops End-to-End Pilot
- Objective: demonstrate governance, orchestration, implementation lanes, testing lanes, review gates, and cleanup safety.
- Capacity hint: max 4 parallel forks.

## Tickets

### AG-201
- Title: Evaluate current agent set against mandatory standards
- Type: governance
- Priority: P1
- Primary lane: `agent-making-agent` + `agent-reviewing-agent`
- Desired output:
  - consolidated standards review result
- Acceptance criteria:
  - hard-gate status per agent
  - rubric + top improvements per agent
- Dependencies: none

### AG-202
- Title: Implement backend idempotency safeguard for webhook processing
- Type: backend implementation
- Priority: P0
- Primary lane: `backend-developer`
- Handoff lane: `backend-tester`
- Desired output:
  - backend code changes
  - backend test report
- Acceptance criteria:
  - developer marks `codex_dev_done`
  - tester marks `codex_test_done`
  - task reaches `codex_review_ready`
- Dependencies: none

### AG-203
- Title: Implement frontend filter drawer accessibility and persistence
- Type: frontend implementation
- Priority: P1
- Primary lane: `frontend-developer`
- Handoff lane: `frontend-tester`
- Desired output:
  - frontend code changes
  - frontend evidence-based test report
- Acceptance criteria:
  - keyboard navigation works
  - filters persist after reload
  - substatus transitions complete
- Dependencies: none

### AG-204
- Title: Implement end-to-end cancellation flow across API and UI
- Type: fullstack implementation
- Priority: P1
- Primary lane: `fullstack-developer`
- Handoff lane: `backend-tester` and/or `frontend-tester` based on scope
- Desired output:
  - backend + frontend integrated changes
  - test evidence and review-ready status
- Acceptance criteria:
  - no inconsistent terminal states
  - validations pass for changed layers
  - task reaches `codex_review_ready`
- Dependencies: AG-202, AG-203

### AG-205
- Title: Review recent commit burst for regressions before merge wave
- Type: review
- Priority: P0
- Primary lane: `recent-commit-review-agent`
- Desired output:
  - `/reports/COMMIT_REVIEW_TASKS.md`
- Acceptance criteria:
  - P0-P3 findings with IDs and verification steps
- Dependencies: AG-202, AG-203, AG-204

### AG-206
- Title: Run full deep code review for post-sprint remediation backlog
- Type: review
- Priority: P2
- Primary lane: `deep-code-review-agent`
- Desired output:
  - `/reports/REVIEW_TASKS.md`
- Acceptance criteria:
  - top urgent fixes, quick wins, and prioritized task list
- Dependencies: AG-205

### AG-207
- Title: Produce worktree cleanup plan for completed codex branches
- Type: maintenance
- Priority: P2
- Primary lane: `git-worktree-cleanup-agent`
- Desired output:
  - `/reports/GIT_CLEANUP_PLAN.md`
- Acceptance criteria:
  - plan_id present
  - keep/delete lists and skipped reasons explicit
- Dependencies: AG-206

### AG-208
- Title: Ensure stack description file exists and is current
- Type: enablement
- Priority: P1
- Primary lane: `backend-developer` or `fullstack-developer` (project-dependent)
- Desired output:
  - `/STACK.md` or `/docs/STACK.md` aligned to team tooling
- Acceptance criteria:
  - validation commands and branch/commit policy documented
  - status policy includes `codex_dev_done`, `codex_test_done`, `codex_review_ready`
- Dependencies: none

## Additional Constraints
- Orchestrator remains planning-only.
- Every implementation ticket should route developer -> tester -> review-ready unless no meaningful test surface exists.
- Track handoff state transitions explicitly in execution log.
- Prefer risk-first sequencing for merge readiness.
