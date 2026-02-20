# SPRINT PLAN — Ekotur Project Bootstrap
Generated: 2026-02-20
Agent: sprint-orchestrator-agent
tracking_mode: linear
pr_base_branch: main
review_required: false
merge_mode: sequential

---

## Sprint Goal
Set up the `ekotur` project in the **existing** repository (`H:\Projects\ekotur`) using the technology stack defined in `STACK.md`. The repo already exists with git history — this sprint installs and configures the full Nuxt 4 + Tailwind CSS + Nitro backend foundation so future feature development can begin immediately.

---

## Stack Reference (STACK.md)
- **Runtime:** Node 22.x, npm (or pnpm)
- **Frontend:** Nuxt 4 (latest), Tailwind CSS, Nuxt UI (recommended)
- **Backend:** Nitro (Nuxt built-in), SQLite + Prisma (or Nuxt Content)
- **Key dirs:** `/server`, `/content`, `/components`, `/pages`, `/layouts`, `/assets`
- **Commands:** `npm run lint` | `npm run test` | `npm run build` | `npm run dev`
- **Branch pattern:** `codex/<task-id>-<slug>`
- **Commit pattern:** `<task-id>: <summary>`

---

## Work Units

| UOW ID  | Title                                      | Agent               | Tester             | Priority | Wave |
|---------|--------------------------------------------|---------------------|--------------------|----------|------|
| UOW-001 | Add Nuxt 4 + Tailwind + Nuxt UI to existing repo | fullstack-developer | frontend-tester    | 1        | 1    |
| UOW-002 | Nuxt Content setup + health-check API route | fullstack-developer | frontend-tester    | 2        | 1    |
| UOW-003 | Base layout + navigation structure         | frontend-developer  | frontend-tester    | 3        | 2    |
| UOW-004 | Home page + placeholder content            | frontend-developer  | frontend-tester    | 4        | 2    |
| UOW-005 | Lint + test + build CI validation          | fullstack-developer | frontend-tester    | 5        | 3    |

---

## Agent Mapping
- UOW-001: `fullstack-developer` (install Nuxt 4 + Tailwind + Nuxt UI into existing repo)
- UOW-002: `fullstack-developer` (Nuxt Content v3 + Nitro health-check route, no DB/ORM)
- UOW-003: `frontend-developer` (Nuxt layouts/components)
- UOW-004: `frontend-developer` (Nuxt pages)
- UOW-005: `fullstack-developer` (cross-layer CI scripts)

## Handoff Policy
developer → frontend-tester → PR-ready
(No REVIEW_TASK — review_required=false)

## Dependencies
- UOW-002 depends on UOW-001 (project must exist before server layer)
- UOW-003 depends on UOW-001
- UOW-004 depends on UOW-003
- UOW-005 depends on UOW-001, UOW-002, UOW-003, UOW-004

## Risks
- Node 22.x must be available in developer environment
- Nuxt 4 is the latest stable release — confirm version availability before install
- Nuxt Content (Markdown) chosen as data layer — no database needed for a blog
- Repo already exists — do NOT git init or overwrite existing files carelessly

---

## Execution Waves
- **Wave 1 (parallel):** UOW-001, UOW-002 (UOW-002 starts after UOW-001 branch is created)
- **Wave 2 (parallel):** UOW-003, UOW-004 (after UOW-001 merged or available)
- **Wave 3:** UOW-005 (after all prior units merged)
