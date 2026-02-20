# SPRINT MERGE PLAN — Ekotur Project Bootstrap
Generated: 2026-02-20
Agent: sprint-orchestrator-agent
merge_mode: sequential
pr_base_branch: main

---

## Merge Mode
**sequential** — merge one unit at a time, in wave order, to avoid conflicts on a greenfield repo.

---

## Merge Order & Waves

### Wave 1
| Order | UOW ID  | Branch                          | Issue  | Gate Checklist                                                                 |
|-------|---------|---------------------------------|--------|--------------------------------------------------------------------------------|
| 1     | UOW-001 | codex/uow-001-nuxt4-scaffold    | EKO-6  | ☐ DEV handoff comment exists  ☐ TEST_TASK passed  ☐ npm run build: pass        |
| 2     | UOW-002 | codex/uow-002-nitro-prisma-sqlite | EKO-7 | ☐ DEV handoff comment exists  ☐ TEST_TASK passed  ☐ GET /api/health: 200      |

> UOW-002 starts after UOW-001 branch is created. Both can be in-flight simultaneously but UOW-001 merges first.

### Wave 2
| Order | UOW ID  | Branch                          | Issue  | Gate Checklist                                                                 |
|-------|---------|---------------------------------|--------|--------------------------------------------------------------------------------|
| 3     | UOW-003 | codex/uow-003-base-layout-nav   | EKO-8  | ☐ DEV handoff comment exists  ☐ TEST_TASK passed  ☐ Layout visible on all pages |
| 4     | UOW-004 | codex/uow-004-home-page         | EKO-9  | ☐ DEV handoff comment exists  ☐ TEST_TASK passed  ☐ Home page renders at /     |

> Wave 2 starts after UOW-001 is merged into main. UOW-003 and UOW-004 can be in-flight in parallel but merge in order (003 before 004).

### Wave 3
| Order | UOW ID  | Branch                          | Issue  | Gate Checklist                                                                 |
|-------|---------|---------------------------------|--------|--------------------------------------------------------------------------------|
| 5     | UOW-005 | codex/uow-005-ci-validation     | EKO-10 | ☐ DEV handoff comment exists  ☐ TEST_TASK passed  ☐ All 4 scripts exit 0      |

> Wave 3 starts after all Wave 1 + Wave 2 units are merged.

---

## Done Gates (per unit)
A unit is merge-ready when ALL of the following are true:
1. Developer has posted `AGENT_EVENT_V1` handoff comment with `event: handoff`, `decision: ready_for_testing`
2. Tester has posted `AGENT_EVENT_V1` outcome comment with `decision: ready_for_review`
3. Linear issue status is `Agent test DONE` (or equivalent passing state)
4. `npm run build` exits 0 on the task branch
5. No open blockers recorded in tester report

---

## PR Creation
- PRs are created by the orchestrator after tester confirms done
- Each PR body includes: task description + expected outcome from issue (no git diff summary)
- PR target: `main`
- PRs are NOT auto-merged — human confirmation required

---

## Blocked Unit Policy
- If a unit is blocked (tester `decision: blocked`), it stays in its current status
- Developer is notified via Linear comment
- Blocked unit does not hold up other independent units
- Blocker resolution re-triggers the test → PR flow

---

## Status: All units PENDING (not yet started)
