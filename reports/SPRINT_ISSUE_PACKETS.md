# SPRINT ISSUE PACKETS — Ekotur Project Bootstrap
Generated: 2026-02-20
Agent: sprint-orchestrator-agent
tracking_mode: linear
packet_version: 1

---

## Packet Manifest

| UOW ID  | Linear Issue | Title                                        | DEV Agent           | TEST Agent       | DEV Comment ID                               | TEST Comment ID                              |
|---------|--------------|----------------------------------------------|---------------------|------------------|----------------------------------------------|----------------------------------------------|
| UOW-001 | EKO-6        | Nuxt 4 scaffold + Tailwind + Nuxt UI         | fullstack-developer | frontend-tester  | 5b7d751e-9200-4e20-a91e-c486b28524ba         | 164aac08-1057-426b-b587-bf73e7a03b13         |
| UOW-002 | EKO-7        | Nitro server + Prisma + SQLite               | fullstack-developer | frontend-tester  | d0ac9be8-6708-45dc-a30c-2044a2e1885d         | c8bba778-25aa-45e7-a2ae-b735c911c053         |
| UOW-003 | EKO-8        | Base layout + navigation                     | frontend-developer  | frontend-tester  | 35737f96-2428-4efc-9b30-9f7e258e5b61         | 72fc63af-4a03-4239-9bfc-1ff77e09a5fb         |
| UOW-004 | EKO-9        | Home page + placeholder content              | frontend-developer  | frontend-tester  | 4fd17780-ae98-4a56-ad97-2a4c33a76b72         | 76f52950-ce98-44de-a19e-71d99579f835         |
| UOW-005 | EKO-10       | Lint + test + build CI validation            | fullstack-developer | frontend-tester  | 998ccb6b-4371-4829-b17d-2c8a3e79c1d8         | a39bb88f-efbc-46dd-a65b-6df05552bd11         |

---

## UOW-001 — EKO-6

**Title:** Add Nuxt 4 + Tailwind CSS + Nuxt UI to existing ekotur repo
**Linear URL:** https://linear.app/ekotur/issue/EKO-6/uow-001-nuxt-4-project-scaffold-tailwind-css-nuxt-ui
**Branch:** `codex/uow-001-nuxt4-scaffold`
**Wave:** 1
**Status:** Todo

### DEV_TASK (packet_version: 2) ← supersedes v1
- Role: `fullstack-developer`
- Goal: Install Nuxt 4 + Tailwind CSS + Nuxt UI into the EXISTING ekotur repo (do not git init or create from scratch)
- Handoff to: `frontend-tester`

### TEST_TASK (packet_version: 1)
- Role: `frontend-tester`
- Readiness gate: status = "Agent work DONE" + developer handoff comment
- Test scope: dev server, Tailwind active, Nuxt UI loaded, build passes
- Evidence: screenshot, build output, console log

---

## UOW-002 — EKO-7

**Title:** Nuxt Content setup + health-check API route
**Linear URL:** https://linear.app/ekotur/issue/EKO-7/uow-002-nuxt-content-setup-health-check-api-route
**Branch:** `codex/uow-002-nuxt-content`
**Wave:** 1 (sequential after UOW-001 branch exists)
**Depends on:** UOW-001
**Status:** Todo

### DEV_TASK (packet_version: 2) ← supersedes v1
- Role: `fullstack-developer`
- Goal: Install Nuxt Content v3 (Markdown-based, no DB/ORM) + Nitro health-check route. Prisma/SQLite dropped.
- Handoff to: `frontend-tester`

### TEST_TASK (packet_version: 2) ← supersedes v1
- Role: `frontend-tester`
- Readiness gate: status = "Agent work DONE" + developer handoff comment
- Test scope: GET /api/health, @nuxt/content in package.json, /content/ dir with .md file, dev server, build
- Evidence: curl /api/health response, dev server screenshot, /content/ directory listing

---

## UOW-003 — EKO-8

**Title:** Base layout + navigation structure
**Linear URL:** https://linear.app/ekotur/issue/EKO-8/uow-003-base-layout-navigation-structure
**Branch:** `codex/uow-003-base-layout-nav`
**Wave:** 2
**Depends on:** UOW-001
**Status:** Todo

### DEV_TASK (packet_version: 1)
- Role: `frontend-developer`
- Goal: Create default.vue layout + AppHeader.vue navigation
- Handoff to: `frontend-tester`

### TEST_TASK (packet_version: 1)
- Role: `frontend-tester`
- Readiness gate: status = "Agent work DONE" + developer handoff comment
- Test scope: layout file, header component, responsive at 375px + 1280px
- Evidence: mobile + desktop screenshots, console log

---

## UOW-004 — EKO-9

**Title:** Home page + placeholder content
**Linear URL:** https://linear.app/ekotur/issue/EKO-9/uow-004-home-page-placeholder-content
**Branch:** `codex/uow-004-home-page`
**Wave:** 2
**Depends on:** UOW-003
**Status:** Todo

### DEV_TASK (packet_version: 1)
- Role: `frontend-developer`
- Goal: Create /pages/index.vue with hero section + tours placeholder
- Handoff to: `frontend-tester`

### TEST_TASK (packet_version: 1)
- Role: `frontend-tester`
- Readiness gate: status = "Agent work DONE" + developer handoff comment
- Test scope: route /, hero section, placeholder section, responsive
- Evidence: desktop + mobile screenshots, console log

---

## UOW-005 — EKO-10

**Title:** Lint + test + build CI validation scripts
**Linear URL:** https://linear.app/ekotur/issue/EKO-10/uow-005-lint-test-build-ci-validation-scripts
**Branch:** `codex/uow-005-ci-validation`
**Wave:** 3
**Depends on:** UOW-001, UOW-002, UOW-003, UOW-004
**Status:** Todo

### DEV_TASK (packet_version: 1)
- Role: `fullstack-developer`
- Goal: Configure ESLint, Vitest, and all four npm scripts
- Handoff to: `frontend-tester`

### TEST_TASK (packet_version: 1)
- Role: `frontend-tester`
- Readiness gate: status = "Agent work DONE" + developer handoff comment
- Test scope: npm run lint, test, build, dev — all must exit 0
- Evidence: full stdout of each command

---

## Handoff Chain (per unit)
```
developer → [handoff comment posted] → frontend-tester → [test report + done comment] → PR-ready
```

## Canonical State
- All packets: `tracking_mode=linear`
- Source of truth: Linear issue status + newest `AGENT_EVENT_V1` comment on each issue
- Worker agents must read from Linear comments, not from this file
